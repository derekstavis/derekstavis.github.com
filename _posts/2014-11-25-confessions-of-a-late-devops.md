---
layout: post
title: "Confession of a late devops"
category: posts
---

I must confess that I'm a late devops. In the company I work there's a lot of
servers to manage, that absolutely no one gives a shit, only me.
As I'm involved full-time on a project, I haven't had time to upgrade the servers
to be safe from latest threats (openssl, shellshock, wget).

Today I upgraded every server. The majority still runs Debian Squeeze. When I
issued a 

	apt-get update && apt-get upgrade
  
Boom. No upgrades available.

The Long-term support
----------------------

Debian 6 was declared a LTS release by Debian team. But to have the long-term 
suport packages you must include an APT repository, so:

	vi /etc/apt/sources.list
  
and include the following line:

	# Squeeze Long-term Support
	deb http://ftp.us.debian.org/debian squeeze-lts main non-free contrib
  
after this you can:

	apt-get update && apt-get upgrade
  
Now you can be happy again, not feeling guilty.
