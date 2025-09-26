---
title: "Redis Lost. Or did they?!"
source: "https://dev.to/code42cate/stop-using-aws-4eg"
author:
  - "[[DEV Community]]"
published: 2025-05-03
created: 2025-05-06
description: "Not long ago, Redis was tired of being eaten alive by the hyperscalers.  Amazon, Microsoft, and... Tagged with cloud, devops, redis, opensource."
tags:
  - "clippings"
---
How many times have you seen someone build an MVP with all the cloud bells and whistles, only to watch it go nowhere?

The product had Lambda functions. It had API Gateway. It had Cognito. It had S3, CloudFront, DynamoDB, CloudWatch, IAM policies, and more. The architecture diagram looked like a subway map. And yet... nobody used it.

The truth is simple: you don't need AWS to build something users love.

## The Overkill Problem

There is a common trap that builders fall into. You read a few blog posts or see a diagram on Twitter and suddenly you think your tiny project needs the same architecture as Netflix.

You don’t.

Most early-stage projects die not because they lacked scalability, but because they lacked users. Or because the product was confusing, buggy, or didn’t solve a real problem.

Overengineering your infrastructure is a great way to waste your time, burn out, or never launch at all.

[![AWS](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F3ux15y25brqb9cbjhgll.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F3ux15y25brqb9cbjhgll.png)

## What You Actually Need

If you are a solo developer or small team trying to build and ship something useful, this is probably all you need:

- A €5 to €20 per month VPS from [Hetzner](https://hetzner.cloud/?ref=mZziDsGU2VVpcloud), DigitalOcean, or similar
- Docker Compose to run your app and a database
- A managed container platform like [Sliplane](https://sliplane.io/?utm_source=you-dont-need-aws-to-build-something-great) if you want to avoid server management entirely (yes I am biased as the founder)

You do not need Kubernetes. You do not need to worry about auto-scaling. You do not need to connect six AWS services to display a single page.

Most indie products run perfectly fine on a single server for a long time.

## When AWS Does Make Sense

Let's be fair. There are situations where AWS is the right choice:

- You want to learn AWS because you're job hunting or building cloud career skills
- You have very specific requirements, like needing data stored in a government cloud or being close to customer infrastructure that is also on AWS
- You are solving a problem that truly needs global scale from day one
- You're already deep in the AWS ecosystem and have a lot of expertise in it

These are good reasons. But be honest with yourself. Most projects don't start here.

And even if you do need AWS later, that's fine. You can always migrate when the time comes. At that point, you will hopefully have revenue, users, and a better understanding of your needs.

Remember this:

**Your product is far more likely to fail because of what it does, not where it runs.**

## How to Get Started Without AWS

Want to launch something fast without spending weeks learning cloud architecture? Here’s a solid starting point:

- Use Docker Compose to define your app, database, and any background workers
- Deploy it to a VPS with ssh and docker compose up
- Or use a platform that abstracts the ops away and lets you focus on code
- Pick open-source tools for things like monitoring, auth, or task queues

That’s it. You can go from zero to deployed in an afternoon. No certification required.

## Final Thoughts

You don’t need AWS to build something great. What you need is focus, a working product, and the ability to ship quickly. Big infrastructure will not save a bad product. Simple infrastructure will not kill a good one.

**Start small. Launch early. Learn fast. You can always scale later.**

Cheers,

Jonas, Co-Founder of [Sliplane](https://sliplane.io/?utm_source=you-dont-need-aws-to-build-something-great)

PS: Just for clarification, I love AWS and I [often even recommend it for specific use cases](https://sliplane.io/blog/globally-replicated-services-for-the-rest-of-us)

[![Neon image](https://media2.dev.to/dynamic/image/width=775%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fneon.tech%2F_next%2Fimage%3Furl%3Dhttps%253A%252F%252Fneondatabase.wpengine.com%252Fwp-content%252Fuploads%252F2025%252F03%252Fneon-vibe-coding-cover.png%26w%3D1920%26q%3D85%26dpl%3Ddpl_wD1CG9fKdjGA57ysJCJqcsyYaEMY)](https://neon.tech/blog/vibe-coding-with-ai-to-generate-synthetic-data-part-1?utm_source=devto&utm_medium=bb&utm_campaign=ai_intro&bb=226018)

### Build better on Postgres with AI-Assisted Development Practices

Compare top AI coding tools like Cursor and Windsurf with Neon's database integration. Generate synthetic data and manage databases with natural language.