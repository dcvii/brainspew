---
title: "How to secure SSH and Postgres with Warpgate"
source: "https://packagemain.tech/p/secure-ssh-and-postgres-with-warpgate?publication_id=2652085&post_id=213907238&isFreemail=true&r=7br8e&triedRedirect=true"
author:
  - "[[Alex Pliutau]]"
published: 2026-09-04
created: 2026-09-04
description: "A great open source alternative bastion host."
tags:
  - "brainspew"
---
Throughout my career I have seen and used various ways of connecting to the internal infrastructure, the most common was probably a direct SSH connection (managing the authorized\_keys manually), I also used manually configured “jump hosts” and more mature tools like [Teleport](https://goteleport.com/blog/ssh-bastion-host/). And a few months ago I learned and used a new great open source bastion software - [Warpgate](https://warpgate.null.page/). Now I enjoy using it so much that I decided to share that experience with you.

First, what is a bastion and why do we need it? In a nutshell, a bastion is the the only server which accepts SSH connections from the outside. If a user wants to access another machine, they need to connect to the bastion first, and then make another SSH connection from the bastion to the final destination. Sometimes this process is called “jumping” and SSH bastions are also called “jump hosts”. The concept can also apply to database connections, Kubernetes cluster connections and so on.

[Warpgate](https://warpgate.null.page/) is an open source project written in Rust that doesn’t require a client, has an enormous amount of features that would be even hard to fit into this article, so I will showcase the most important to me at least.

![](https://substackcdn.com/image/fetch/$s_!nKdt!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9d01d756-75bd-4c9f-9f00-8f9b5cc02485_1250x902.png)

So the main features advertised are:

- Add user accounts and easily assign them to specific hosts and URLs within the network.
- Warpgate will record every session for you to view (live) and replay later through a built-in admin web UI.
- Browser-based SSH, RDP and VNC access is built in; native clients continue to work.
- Not a jump host - forwards connection straight to the target in a way that’s fully transparent to the client.
- Native 2FA and SSO support (TOTP & OpenID Connect)
- Built-in brute-force protection with IP blocking and user lockout
- Single binary with no dependencies.

For my project the main needs were to distribute the access via RBAC, support browser-based connections (still keeping native clients), have 2FA auth with SSO. Let’s now go through the installation / configuration process to showcase the result.

First of all, you’ll need a host itself. Then there are two ways of installing it on your infrastructure: using a single binary or via Docker. I would always prefer the first option.

I support the software packages that come in the form of a single binary executable (statically linked or portable), that one can just copy anywhere in ${PATH} and execute, without needing sudo, or downloading half the distribution’s packages as dependencies.

Just download the binary from the [Releases](https://github.com/warp-tech/warpgate/releases) page, put it on your server and run:

```markup
$ warpgate setup

13:43:10  INFO Welcome to Warpgate 0.6.0
13:43:10  INFO Let's do some basic setup first.
13:43:10  INFO The new config will be written in /etc/warpgate.yaml.
13:43:10  INFO * Paths can be either absolute or relative to /etc.
✔ Directory to store app data (up to a few MB) in · /var/lib/warpgate
✔ Endpoint to listen for SSH connections on · 0.0.0.0:2222
✔ Endpoint to expose admin web interface on · 0.0.0.0:8888
✔ Do you want to record user sessions? · yes
✔ Set a password for the Warpgate admin user · ********
13:43:28  INFO Generated configuration:
[...]
13:43:28  INFO Saved into /etc/warpgate.yaml
13:43:28  INFO Using config: "/etc/warpgate.yaml" (users: 1, targets: 1, roles: 1)
13:43:28  INFO Generating HTTPS certificate
13:43:28  INFO
13:43:28  INFO Admin user credentials:
13:43:28  INFO   * Username: admin
13:43:28  INFO   * Password: <your password>
13:43:28  INFO
13:43:28  INFO You can now start Warpgate with:
13:43:28  INFO   warpgate --config /etc/warpgate.yaml run
```

The wizard helps you to configure the setup, or you can also use the YAML file if you want to.

During the setup you can enable session recordings which is another great feature of the Warpgate, very valuable for big orgs.

![](https://substackcdn.com/image/fetch/$s_!uff1!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F41084340-a80e-4215-8b78-f9dabee2cf44_1133x751.png)

Yes, warpgate comes with the web interface (optional), address to which you can configure in the YAML config file:

```markup
http:
  listen: "127.0.0.1:8080"
  external_port: 443
  trust_x_forwarded_headers: true
```

Warpgate also supports SSO and RBAC access controls, which makes it very easy to assign permissions and server access. Can be configured in the YAML file.

```markup
sso_providers:
  - name: azure
    label: 
    return_url_prefix: _
    auto_create_users: false
    provider:
      type: azure
      client_id:
      client_secret:
      tenant:
```

Ok, now we’re coming to a fun part: targets and 2FA. This is where we can see a real beauty of Warpgate.

Adding a target is easy, we can do it completely in the UI.

![](https://substackcdn.com/image/fetch/$s_!F6V-!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F70737c07-cce5-4ddd-a141-37e4f5eb9de2_977x715.png)

```markup
User -> Warpgate -> Target (SSH or Postgres or k8s)
```

As you can see in this simple diagram, we should only connect to our targets from the Warpgate, meaning that ideally the connections from the outside are blocked, this can be done in many ways, one option is to use the [ufw](https://wiki.archlinux.org/title/Uncomplicated_Firewall).

```markup
sudo ufw allow from <WARPGATE_IP> to any port 5432 proto tcp
sudo ufw enable
sudo ufw status numbered verbose
```

Warpgate can connect to PostgreSQL servers with a username and password using password (cleartext), md5 or SCRAM (SASL) authentication.

As a PostgreSQL protocol server (towards clients), Warpgate only allows secure (TLS) connections and uses the password auth mode.

You can now use any PostgreSQL client applications to connect through Warpgate.

The experience is similar to SSH, we use our normal commands like ssh, psql, which prompts us to do the quick 2FA, and then proceeds with proxying all the requests.

![](https://substackcdn.com/image/fetch/$s_!K7xN!,w_1456,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Faada97fa-d64e-47c9-902d-4ab7d2a538b3_1566x824.png)

Is installing Warpgate in your infrastructure enough to be 100% secure? No, there are many other things you need to take into the consideration: supply chain, networking, key management and so on.

p.s. I like the name Warpgate, but man the search engines bury it deep down after many other projects and games with a similar name:)

### Resources

- [warpgate.null.page](https://warpgate.null.page/)

---

∙