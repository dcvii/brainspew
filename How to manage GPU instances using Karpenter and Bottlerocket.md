---
title: "How to manage GPU instances using Karpenter and Bottlerocket"
source: "https://omniarcs.notion.site/How-to-manage-GPU-instances-using-Karpenter-and-Bottlerocket-d0b3cae1c3074068bff13b098536638a"
author:
  - "[[omniarcs on Notion]]"
published:
created: 2025-05-02
description: "A new tool that blends your everyday work apps into one. It's the all-in-one workspace for you and your team"
tags:
  - "clippings"
---
![](https://omniarcs.notion.site/images/page-cover/nasa_fingerprints_of_water_on_the_sand.jpg)

✏️

@ August 3, 2023

@ Eduardo Lugo

AI tools are everywhere now and in order to have them do their thing with acceptable performance they need to use the power of GPU enabled instances, in this article I'll tell you how we are achieving this.

The Omniarcs team is building and supporting the The little AI assistant that could \- Locus Extension.So to see how the application of this post is running in production, please download and try [Locus](https://chrome.google.com/webstore/detail/locus-%E2%80%94-smart-ctrl-%20-f/eppedlbobmdflmhleafebmahnbphgipb)!

![](https://omniarcs.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F579f52ea-ce7e-4c06-98c9-0f87db7b517e%2Fgpu_boat_meme.png?table=block&id=2059ff3b-ad73-4fe2-9ae6-1601738e9e93&spaceId=38208651-d046-4612-8de8-61c0cc8017cf&width=1420&userId=&cache=v2)

#### What is Karpenter?

> “Karpenter is an open-source node provisioning project built for Kubernetes. Adding Karpenter to a Kubernetes cluster can dramatically improve the efficiency and cost of running workloads on that cluster”

The idea of [Karpenter](https://karpenter.sh/preview/) in short is that instead of having a node group for your Kubernetes Cluster you let Karpenter manage that by giving it options of what type of instances and resources can it use for that node group that can scale depending on the requirements of your pods.

Here is a [terraform example of setting an EKS cluster with Karpenter](https://github.com/aws-ia/terraform-aws-eks-blueprints/blob/main/examples/karpenter/README.md) enabled

The interesting part of Karpenter are the provisioners, we’ll get into that later.

#### What is Bottlerocket?

> Bottlerocket is a Linux-based open-source operating system that is purpose-built by Amazon Web Services for running containers.

We use [Bottlerocket](https://aws.amazon.com/bottlerocket/) in Karpenter as the family of AMIs our provisioners use, you can read about it [here](https://karpenter.sh/docs/concepts/node-templates/#specamifamily), but basically it is the AMI that Karpenter will use to create the instance that the pods will run on.

#### How to enable GPU?

You have some options here, you can use the [nvidia gpu operator](https://github.com/NVIDIA/gpu-operator) or the [nvidia device plugin](https://github.com/NVIDIA/k8s-device-plugin), for now we have choosen the plugin

#### Putting everything together

Now lets get into the details of each bit

#### Karpenter provisioner

This is the blueprint of what your instances will look like, so we can define, instance size, cpu, family, generation, architecture, etc. You can be as specific or generic as you like, make sure you use [Karpenter docs](https://karpenter.sh/preview/concepts/instance-types/#g4ad-family) to define stuff that is not contradicting itself like an arch that does not work on a specific instance type (it happens!)

JavaScript

Copy

resource "kubectl\_manifest" "karpenter\_provisioner\_models" { yaml\_body \= << \- YAML apiVersion: karpenter.sh / v1alpha5 kind: Provisioner metadata:name: models spec:labels:compute: models gpu \- type: nvidia requirements:\- key:"karpenter.k8s.aws/instance-category" operator: In values:\["g"\] \- key:"karpenter.k8s.aws/instance-cpu" operator: In values:\["4"\] \- key:"karpenter.k8s.aws/instance-size" operator: In values:\["2xlarge","xlarge"\] \- key:"karpenter.k8s.aws/instance-family" operator: In values:\["g4dn"\] \- key:"karpenter.k8s.aws/instance-generation" operator: In values:\["4"\] \- key:"karpenter.k8s.aws/instance-hypervisor" operator: In values:\["nitro"\] \- key:"topology.kubernetes.io/zone" operator: In values: $ { jsonencode (local.azs) } \- key:"kubernetes.io/arch" operator: In values:\["amd64"\] \- key:"karpenter.sh/capacity-type" \# If not included, the webhook for the AWS cloud provider will default to on \- demand operator: In values:\["spot","on-demand"\] kubeletConfiguration:containerRuntime: containerd maxPods:110 limits:resources:cpu:1000 consolidation:enabled:true providerRef:name: models ttlSecondsUntilExpired:604800 \# 7 Days \= 7 \* 24 \* 60 \* 60 Seconds YAML depends\_on \= \[ module.eks\_blueprints\_kubernetes\_addons \] }

Other handy resource is a node template, it is most likely that you are using python and that your docker container is huge, so you’ll need to add more disk to the instance, this is how you do that

JavaScript

Copy

resource "kubectl\_manifest" "karpenter\_provisioner\_models\_node\_template" { yaml\_body \= << \- YAML apiVersion: karpenter.k8s.aws / v1alpha1 kind: AWSNodeTemplate metadata:name: models spec:amiFamily: Bottlerocket subnetSelector: karpenter.sh / discovery:"${module.eks.cluster\_name}" securityGroupSelector: karpenter.sh / discovery:"${module.eks.cluster\_name}" blockDeviceMappings:\- deviceName:/ dev / xvdb ebs:volumeType: gp3 volumeSize: 60Gi deleteOnTermination:true YAML depends\_on \= \[ module.eks\_blueprints\_kubernetes\_addons \] }

Stay tuned for other articles we’ll put out on how we moved a lot of our code where appropriate from Python to Rust to get our containers a lot smaller and faster.

#### Enabling GPU

If you are using the EKS blueprints you’ll need to add this

Plain Text

Copy

enable\_nvidia\_device\_plugin = true nvidia\_device\_plugin\_helm\_config = { values = \[ <<-EOT nodeSelector: gpu-type: nvidia EOT \] }

This will tell the plugin to run on the instances with the gpu-type label

#### Making sure it all works

At this point your cluster is running, you have a bunch of pods running in kube-system and you have karpenter pods running in the karpenter namespace, but there are no instances and no plugin pods.

If you are using the blueprints your setup is using fargate for the base cluster and instances will be used for other pods, depending on your needs this might be a good idea or not.

But lets launch a pod that can help us see things are ok with the following one liner

Plain Text

Copy

cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: gpu-pod spec: restartPolicy: Never containers: - name: cuda-container image: nvcr.io/nvidia/k8s/cuda-sample:vectoradd-cuda10.2 resources: limits: nvidia.com/gpu: 1 # requesting 1 GPU tolerations: - key: nvidia.com/gpu operator: Exists effect: NoSchedule EOF

We are launching a container that will help us debug if the instance has the GPU enabled or not.

It is very important to add the gpu limits on the container section to the pod or deployment.

Now lets see the output

Plain Text

Copy

kubectl describe pods gpu-pod

Your logs should be something like this

Plain Text

Copy

➜ ~ kubectl logs gpu-pod \[Vector addition of 50000 elements\] Copy input data from the host memory to the CUDA device CUDA kernel launch with 196 blocks of 256 threads Copy output data from the CUDA device to the host memory Test PASSED Done

You can also check the logs of the nvidia-plugin pod and it should look like this

Plain Text

Copy

~ kubectl logs nvidia-device-plugin-m92hq -n nvidia-device-plugin 2023/08/03 14:37:13 Starting FS watcher. 2023/08/03 14:37:13 Starting OS watcher. 2023/08/03 14:37:13 Starting Plugins. 2023/08/03 14:37:13 Loading configuration. 2023/08/03 14:37:13 Initializing NVML. 2023/08/03 14:37:13 Updating config with default resource matching patterns. 2023/08/03 14:37:13 Running with config: { "version": "v1", "flags": { "migStrategy": "none", "failOnInitError": true, "nvidiaDriverRoot": "/", "plugin": { "passDeviceSpecs": false, "deviceListStrategy": "envvar", "deviceIDStrategy": "uuid" } }, "resources": { "gpus": \[ { "pattern": "\*", "name": "nvidia.com/gpu" } \] }, "sharing": { "timeSlicing": {} } } 2023/08/03 14:37:13 Retreiving plugins. 2023/08/03 14:37:13 Starting GRPC server for 'nvidia.com/gpu' 2023/08/03 14:37:13 Starting to serve 'nvidia.com/gpu' on /var/lib/kubelet/device-plugins/nvidia-gpu.sock 2023/08/03 14:37:13 Registered device plugin for 'nvidia.com/gpu' with Kubelet

On the karpenter pods logs you should also see the instance being provisioned and after the job completes deprovisioned

Plain Text

Copy

2023-08-03T14:35:42.015Z INFO controller.provisioner launching machine with 1 pods requesting {"cpu":"155m","memory":"120Mi","nvidia.com/gpu":"1","pods":"6"} from types g4dn.xlarge {"commit": "5a2fe84-dirty", "provisioner": "models"}... 2023-08-03T14:35:44.531Z INFO controller.provisioner.cloudprovider launched instance {"commit": "5a2fe84-dirty", "provisioner": "models", "id": "i-XXXXXXXXX", "hostname": "ip-172-31-XX-X.us-east-X.compute.internal", "instance-type": "g4dn.xlarge", "zone": "us-east-Xb", "capacity-type": "spot", "capacity": {"cpu":"4","ephemeral-storage":"60Gi","memory":"15155Mi","nvidia.com/gpu":"1","pods":"110"}}... 2023-08-03T14:37:18.043Z INFO controller.deprovisioning deprovisioning via consolidation delete, terminating 1 machines ip-172-31-16-11.us-east-2.compute.internal/g4dn.xlarge/spot {"commit": "5a2fe84-dirty"}

You should have a cluster configured in a way that can

Run applications that require GPU compute

Can launch spot or on-demand instances and terminate them once they are not needed based on the provisioner configuration.

#### Conclusion

GPU enabled cluster will be required for a lot of the solutions being built currently, there are a ton of options on how to do this, hopefully this gets you in the right direction.

Even more Karpenter offers a way to add flexibility without loosing control of the resources and spend associated with a kubernetes cluster with these requirements.

We will probably see easier ways to accomplish this in the future!