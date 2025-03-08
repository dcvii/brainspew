---
title: "Whats the use of jinja in real world projects?"
source: "https://www.reddit.com/r/Python/comments/16hxm0r/whats_the_use_of_jinja_in_real_world_projects/"
author:
  - "[[[deleted]]]"
published: 2023-09-13
created: 2025-02-21
description: "Currently learning python in flask, and got me wondering on how i could use this knowledge upon building projects as i planned to use flask"
tags:
  - "jinja"
---
Currently learning python in flask, and got me wondering on how i could use this knowledge upon building projects as i planned to use flask as a be and react as fe although i wanted to do it all python but i think making jinja a no refresh is a hassle

---

## Comments

> **hydro\_agricola** • [65 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0gl1vp/) • 2023-09-13
> 
> My team has used it to create SQL templates for deploying replication on the fly.
> 
> > **Reasonable-Ladder300** • [32 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0gtwmt/) • 2023-09-13
> > 
> > Almost literally what dbt is
> > 
> > > **\[deleted\]** • [16 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0hv3zs/) • 2023-09-14
> > > 
> > > Dbt too uses jinja for its sql generation.
> > > 
> > > > **Bitter-Green2100** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0ktqcd/) • 2023-09-14
> > > > 
> > > > I use jinja for dbt 🤷🏻‍♂️ it’s pretty neat and I like it a lot
> > 
> > **hydro\_agricola** • [2 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0gx6k9/) • 2023-09-13
> > 
> > I think the reason to use Jinja templates was to create objects in our niche target db which differs quite a bit from your standard SQL syntax
> 
> **RizzyNizzyDizzy** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0i2p1f/) • 2023-09-14
> 
> Doing that only lol
> 
> **MrMxylptlyk** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0korwp/) • 2023-09-14
> 
> Can you point me to some examples of thsi on the net?

> **mattl33** • [44 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0giw7l/) • 2023-09-13
> 
> I'm a network engineer, jinja is commonly used for templating network device configurations that tend to get very long and complex.
> 
> > **Pengwyn2** • [9 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0hbmus/) • 2023-09-13
> > 
> > Can second this, our company also uses Jinja for templating device configurations; bash scripts; and/or ansible scripts (actually we mostly use Django templating but its almost a carbon copy of jinja)
> > 
> > **Show\_Me\_Your\_Packets** • [2 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0n82el/) • 2023-09-15
> > 
> > Not only long and complex but following standards, makes sure people don’t forget certain components, include certain parts based on other metadata (location, primary/secondary configs), can use lots of logic to infer large amounts of configuration with minimal user or data input
> > 
> > **TheBros35** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0hiky6/) • 2023-09-14
> > 
> > Network engineer also. Do you use them to display them, or like you have a template that you fill out with certain words and then it prints out a config?
> > 
> > > **Pengwyn2** • [3 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0hmxsh/) • 2023-09-14
> > > 
> > > more like vlans, vrf, fw rules, interfaces, ip addresses etc instead of 'words' but it is used to generate config files or configuration scripts that are then pushed/deployed to devices

> **riklaunim** • [27 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0gflug/) • 2023-09-13
> 
> If you make web applications then you will have HTML and that can be managed by Jinja in a clean and handy way. This can happen but not always - like when the frontend isn't managed by a Python app but is a stand-alone JavaScript app (like an SPA app) or a mobile/desktop app functioning as a client for a REST/other API provided by a Python app. Then you would not really have HTML templates on the Python side.
> 
> > **SpaceBucketFu** • [3 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0iptq6/) • 2023-09-14
> > 
> > This is an underrated ass comment.  
> > I’ll break this down a little for the OP.  
> > Templating like Jinja2 happens serverside. Sometimes you might have an application that can’t be completely determined before presenting to the client side. That is a design pattern you have to deal with and think about and understand.

> **sinsworth** • [18 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0gt91e/) • 2023-09-13
> 
> Jinja can template anything, not just HTML, e.g. I've used it a lot for templating LaTeX and Markdown docs. More on topic of webdev though, even in an SPA you might want to have parts of your HTML rendered by the backend, template some JS snippets, propagate some settings to your client code etc. all the while avoiding additional requests on initial page load.

> **dmtucker** • [9 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0gk5qs/) • 2023-09-13
> 
> Salt uses it, as well as Cookiecutter.

> **Unique\_Squash\_7023** • [9 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0glf7h/) • 2023-09-13
> 
> Terraform HCl files, anything that is a global deployment with a decent amount of resources, I would use jinja2 templates all the time.

> **metaphorm** • [6 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0ghi92/) • 2023-09-13
> 
> It was designed as a server side HTML templating language. That's still a useful pattern in many web apps, but is less useful for SPA style apps where all of the templating is done in JavaScript in the browser.
> 
> Jinja is versatile though and sees use in all kinds of things where generating text files is important. For example, Ansible (a configuration management tool) uses Jinja as it's built in default template engine. In this use case you're typically generating configuration files (like .ini or system.d unit files) instead of HTML. Works great in this role.
> 
> > **silent\_guy1** • [7 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0iad20/) • 2023-09-14
> > 
> > I used htmx with jinja html templates and flask to create a server side rendered website and it was very smooth. As someone with very limited frontend experience, I didn't need to deal with javascript to add interactivity.
> > 
> > > **mRWafflesFTW** • [4 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0j4p00/) • 2023-09-14
> > > 
> > > This is the way.
> > > 
> > > **borborygmis** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0nkm4p/) • 2023-09-15
> > > 
> > > You can also use nunjucks on the client side (with htmx). Pretty nice for handling JSON responses.
> > > 
> > > > **silent\_guy1** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0ox3lx/) • 2023-09-15
> > > > 
> > > > Right! I discovered that yesterday and I was so happy to have a nice separation of UI and API. Htmx supports three js templating engines but I could get only one to work.
> > > > 
> > > > I don't know how js templates will work with jinja templates since they use similar escape characters. I'll try that this weekend.
> 
> **agrif** • [4 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0hogq4/) • 2023-09-14
> 
> Systemd itself uses Jinja as a template engine during build, to make unit files but also for other configuration files, manpages, etc.

> **The\_Young\_Busac** • [6 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0gxq05/) • 2023-09-13
> 
> I regularly use Jinja2 in my line of work. I've built dozens of templates that generate pdf deliverables to mail out. It can be a very useful tool in certain domains.

> **IcedThunder** • [5 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0ha8t0/) • 2023-09-13
> 
> I am a python dev who occasionally has to do web frontend stuff and it's nice learning as little html and JS as possible *shrug*. It's almost magic to me what Jinja can do with html pages, and I know it can do a lot more.

> **silent\_guy1** • [4 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0iapdx/) • 2023-09-14
> 
> You can do full stack development with flask and jinja html templates. You can use htmx to add interactivity. You'll have to deal with only python and html. It's good for backend people who have limited frontend experience.
> 
> I created a small website like that and it took me only two days.
> 
> > **MrMxylptlyk** • [2 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0kq38p/) • 2023-09-14
> > 
> > That's awesome. Do you have any good tutorials to do this end to end? Htmx and jinja? I believe litestar as htmx support built in.
> > 
> > > **silent\_guy1** • [2 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0lnc6z/) • 2023-09-14
> > > 
> > > I referred to this one: [https://codecapsules.io/docs/tutorials/build-flask-htmx-app/](https://codecapsules.io/docs/tutorials/build-flask-htmx-app/)
> > > 
> > > There are other flask and jinja packages to make the htmx integrations easier but I'd suggest you to start without them first and see if it suits your needs.
> > > 
> > > These are some full fledged apps using that stack and css framework: [https://github.com/tataraba/musicbinder](https://github.com/tataraba/musicbinder) [https://github.com/AutomationPanda/bulldoggy-reminders-app](https://github.com/AutomationPanda/bulldoggy-reminders-app)
> > > 
> > > > **MrMxylptlyk** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0mlazg/) • 2023-09-15
> > > > 
> > > > Nice, thanks

> **0rionsEdge** • [3 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0hcrcz/) • 2023-09-14
> 
> Ansible uses it it's template engine. I use Ansible to generate host-specific config files using templates.
> 
> I have also used jinja to generate code before now, although that is far more situational

> **Dr\_Ironbeard** • [3 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0i7hai/) • 2023-09-14
> 
> If you want to "do it all python" then you should look into using HTMX instead of React. This would allow you to use Jinja to create HTML templates that get served and utilized by HTMX to create a SPA feel.

> **PhishGreenLantern** • [3 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0ib1ls/) • 2023-09-14
> 
> We have a really large YAML cloudformation template. It has a lot of IAM policy statements in it and used to be really hard to read. So we just broke the YAML up into Jinja templates and then reassemble it at render time.
> 
> Bonus we added all the comments we need and then we use cfn-flip to swap the template to json and ship it without comments.
> 
> The whole thing is super readable now as it's broken down into semantically named field with good comments.

> **Yellow\_Robot** • [3 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0j0pur/) • 2023-09-14
> 
> military orders generator (ukraine)

> **hidazfx** • [2 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0gz0rg/) • 2023-09-13
> 
> I've personally used it for doing printable documents that get converted to PDFs via headless Chrome running in a Docker container.

> **idetectanerd** • [2 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0ijlld/) • 2023-09-14
> 
> My Ansible job use j2 for templating. It’s picked up my Jenkins job.

> **warm\_cocoaRS** • [2 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0ijpwj/) • 2023-09-14
> 
> One option for updating jinja templates without a refresh is using websockets. Load up a frame with jinja then populate elements in the frame with websocket data and client-side javascript. flask-socketio is good for this.

> **OogalaBoogala** • [4 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0girij/) • 2023-09-13
> 
> If you’re just using flask as a rest api, there’s really no need for jinja. if you’re committed to jinja and willing to switch out front end frameworks, the new hotness is HTMX. Used [this](https://codecapsules.io/docs/tutorials/build-flask-htmx-app/) as a tutorial. Built out a small app in less than a day.

> **fogel3** • [3 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0h1587/) • 2023-09-13
> 
> If you’re just starting out in web dev and want to go full python, check out Reflex, streamlit, and nicegui

> **YellowSharkMT** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0j9ws1/) • 2023-09-14
> 
> Look you've got multiple things going on here.
> 
> 1. Jinja is used in a ton of places, as others have mentioned. I personally use it a ton with Ansible, as well as Home Assistant.
> 2. No idea about your skill level with React, so we can't evaluate what would be the better choice for you. If you're already comfortable writing frontends with React though, then that's probably a fine way to start.

> **floriv1999** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0gz1ro/) • 2023-09-13
> 
> [https://github.com/PickNikRobotics/generate\_parameter\_library](https://github.com/PickNikRobotics/generate_parameter_library) generates cpp (and python) code for some config structs based on a yaml file during compile time. The code is generated using jinja templates.

> **vantasmer** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0hc8qs/) • 2023-09-13
> 
> I’ve used to dynamically generate deployment pipelines in gitlab and a lot of use is also for network device configuration.
> 
> Also autogenerate emails upon certain actions being performed.

> **nickbernstein** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0hjb42/) • 2023-09-14
> 
> Ansible for dynamic values in config files

> **djddanman** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0hwwqp/) • 2023-09-14
> 
> The Klipper 3D printer firmware uses jinja for writing macros

> **Merakel** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0iahsu/) • 2023-09-14
> 
> It's amazing with Ansible, which was written in python.

> **EmperorOfCanada** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0idclk/) • 2023-09-14
> 
> If you are not talking about some complex framework there are basically two fundamental formulas for displaying stuff on the web:
> 
> - You have an html page which reaches out and gets json, formats it, and then displays it. Where this is the superior formula is when the user can click on something which needs to display new data.
> - You have something static (in that the user won't soon want slight variations). This is where jinja skips the steps of getting json, and then applying that json data to display.
> 
> Where to use one or the other isn't entirely always clear. You might have a page which rarely changes, so jinja looks like a good idea. But a mobile app also wants the data, so providing it in json and doing the html/json thing is a good idea.
> 
> Or, you have a page which could take the data and then do a pile of serious processing. This could significantly reduce the load on your server. In this case, html/json is potentially a good idea.
> 
> I've used jinja where the pages were fairly complex and the sql queries were somewhat demanding. But the pages generated would not change for years at a time. So, I pre-generated all the pages using jinja, and only when a user changes something, do I regenerate the relevant pages (takes under a minute).
> 
> Where jinja is great is you generally end up with way less code. Less code should be faster to develop, and it should be easier to maintain. The problem is that it can become very tempting to start really blending the view and model layers. While this can be a bad thing, sometimes it is so simple, that there is little risk. It is complicated.
> 
> I've noticed a few people mentioning generating latex, configs, etc. This would be very much perfect for jinja as those could be considered "static" and certainly can't be reaching back for some json.
> 
> The answer is: the more static- > Jinja, the more dynamic -> json. But keep in mind this is all a spectrum.

> **draeath** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0iefxz/) • 2023-09-14
> 
> I use it all the time with Ansible, to template configuration files and the like.
> 
> It's even used directly in the playbooks (YAML files), not just the template module.

> **datadidit** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0irc13/) • 2023-09-14
> 
> Ansible uses ninja templates.

> **techtesh** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0is3dq/) • 2023-09-14
> 
> I am using it to write ansible rules (config mgmt) for all our hosts and workspaces

> **Ivantgam** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0iwwy2/) • 2023-09-14
> 
> Jinja is the heart of dbt which is the part of the modern data infrastructure

> **notreallymetho** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0iymvu/) • 2023-09-14
> 
> Helm / yaml templating / k8s stuff? Honestly I kinda hate Jinja but that’s what we use it for my (I’m an SRE)

> **hitchdev** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0j3k84/) • 2023-09-14
> 
> I use it to take org mode notes from the orgzly app on my phone and generate documents [with orji](https://github.com/crdoconnor/orji) using termux. At the moment I have script shortcuts to:
> 
> - Generate my latex CV using a nice template and press a button to generate a new PDF with tweaked content.
> - Generate a nice looking latexed postal letter PDF easily from my phone for when I want to write an official letter of complaint or something.
> - Push out pages to my website in markdown.

> **Fabulous-Possible758** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0j9p5g/) • 2023-09-14
> 
> Programmatic templating is useful. For as much shit as people give HTML as “not a programming language” it is actually necessary to have a language which determines page layout and UI.
> 
> Making boilerplate generation easier has… almost been the entire history of programming languages. Jinja both helps and thwarts that in the same way so many templating languages have.

> **9\_11\_did\_bush** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0jfzd2/) • 2023-09-14
> 
> One place I have used Jinja at work is writing YAML recipes for conda.

> **owliger** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0jq0rj/) • 2023-09-14
> 
> For email templates, we have saved them in the database, allowing us to use a rich text editor to make changes.

> **borborygmis** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k0no2a7/) • 2023-09-15
> 
> I've used it extensively in:
> 
> - generating on the fly dynamic ci/cd configs
> - server config generator
> - Django templates
> - helm and kubernetes configs (over go templating)
> - generating static html pages

> **monorepo** • [1 points](https://reddit.com/r/Python/comments/16hxm0r/comment/k1ymn7h/) • 2023-09-24
> 
> Aside from daily use in Ansible projects, I have built almost all of my recent applications with only a Python web framework, Jinja templating, HTMX, and TailwindCSS.  
> No need for NPM, or whatever front-end stuff people use.
> 
> It's quite flexible.