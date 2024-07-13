---
date: 2024-07-13
description: Easy/Lazy bash prompt from an uambiguous docker container 
category: docker, devops
tags: 
  - docker
  - devops
  - Home Assistant
layout: blog
author: 
  name: klc
  email: k@lo0.ca
expanded: true
---
# So you want to run a command in a docker container.
I needed to reset my password on `emqx` within my `Home Assistant` setup.

To do this outside of a container, [we simply run a command](https://forum.emqx.io/t/i-cant-remember-my-username-or-password/358) directly ie `emqx admins ...`.

Within home assistant, plugins/add-ons are docker containers. To run commands within docker containers, we have a few different ways, but I usually like to interact with a shell prompt.

When looking around for a lazy one liner to run, [I found a post](https://community.home-assistant.io/t/emqx-password-reset/742927) looking for help doing the exact same thing. I've replied to it; but also I'm going to leave this here for myself or others to use later. 

This can probably be done without `jq`, but instead of memorizing docker filters (yet), it's more useful to me to know the `jq` filter syntax; simply as it works across any tool with json output.

To use for things other than `emqx`, just replace `emqx` with a string that is contained in the container name. To look at container names you can use `docker ps`.

Lmk if you found this useful :D

`docker exec -it $(docker ps --format json | jq -r -c 'select( .Names | contains("emqx")).ID') bash`

-KC