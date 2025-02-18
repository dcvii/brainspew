---
title: "GitHub publishes RSA SSH host keys by mistake, issues update"
source: "https://www.theregister.com/2023/03/24/github_changes_its_ssh_host/?utm_source=daily&utm_medium=newsletter&utm_content=top-article"
author:
  - "[[Liam Proven]]"
published: 2023-03-24
created: 2025-02-17
description: "Getting connection failures? Don't panic. Get new keys"
tags:
  - "clippings"
---
GitHub has updated its SSH keys after accidentally publishing the private part to the world. Whoops.

A [post](https://github.blog/2023-03-23-we-updated-our-rsa-ssh-host-key/) on GitHub's security blog reveals that the biz has changed its RSA SSH host keys. This is going to cause connection errors, and some frightening warning messages, for a lot of developers, but it's all right: it's not scary hackk0r activity, just plain old human error.

[Microsoft subsidiary GitHub](https://www.theregister.com/2018/06/04/microsoft_buys_github/) is the largest source code shack in the world, with an estimated 100 million active [users](https://github.blog/2023-01-25-100-million-developers-and-counting/). So this is going to trip up a *lot* of people. It's not the end of the world: if you normally push and pull to GitHub via SSH – which most people do – then you will have to delete your local GitHub SSH key, and fetch new ones.

As the blog post describes, the first symptom is an alarming warning message:

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
```

For almost everyone, this warning is spurious. It's not that you're being attacked – although that is always a *remote* ([ha ha, only serious](https://en.wiktionary.org/wiki/ha_ha_only_serious)) possibility – it's that GitHub revoked its old keys and published new ones. Hanlon's Razor applies, as it most often does:

(The word *stupidity* is often replaced with *incompetence*, but then, one does tend to lead to the other.)

This time, the reason was – as usual – plain old human error. Someone published GitHub's **private** RSA keys in a repository on GitHub itself. If you're unclear how SSH encryption works, about public versus private keys, or the different cryptographic algorithms SSH uses, there are many good [explanations](https://www.digitalocean.com/community/tutorials/understanding-the-ssh-encryption-and-connection-process) out there.

In brief and as most *Reg* readers know, it is fine and good to reveal, publish and share *public* keys, but your *private* keys must be kept secret. If they get out – for instance, if someone accidentally publishes them on a high-profile website – then anyone who has them can pretend to be you. That is bad.

- [GitHub Copilot learns new tricks, adopts this year's model](https://www.theregister.com/2023/03/22/github_copilot_learns_new_tricks/)
- [GitHub rolls out mandatory 2FA for loads of devs next week](https://www.theregister.com/2023/03/09/github_2fa_requirement/)
- [GitHub claims source code search engine is a game changer](https://www.theregister.com/2023/02/07/github_code_search/)
- [Microsoft, GitHub, OpenAI urge judge to bin Copilot code rip-off case](https://www.theregister.com/2023/01/31/microsoft_github_openai_copilot/)

SSH supports alternative cryptographic [algorithms](https://goteleport.com/blog/comparing-ssh-keys/) to RSA for its keys, and GitHub [also](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints) has ECDSA and Ed25519 keys as well. Those were not published, so they haven't changed.

GitHub isn't saying who published the keys or where, which is perfectly fine, but we suspect that information might trickle out later on. At any rate, at 0500 UTC today it changed the RSA for a new one, so you should follow the instructions in the blog post, delete the old key, and add the new ones, as soon as possible. ®

### Bootnote

Hanlon's Razor itself is a corollary of [Finagle's Law](http://www.catb.org/jargon/html/F/Finagles-Law.html): *Whatever can go wrong, will go wrong.* And as an ironic but rather good example of that, it could well be that Robert J. Hanlon was actually slightly [misquoting](https://quoteinvestigator.com/2016/12/30/not-malice/) Robert A. Heinlein, and so it really ought to be Heinlein's Razor.