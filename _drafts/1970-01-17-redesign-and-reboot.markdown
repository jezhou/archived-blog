---
layout: post
title: Redesign and reboot!
---
So I finally spent some time to redesign the blog. Yay! This means that:

1. I'm finally gonna use this website (I've been keeping it more or less a secret for a couple of years without really committing to it)
2. I have another thing to write about. And this one is gonna be a doozy.

I think something as simple as redesigning / rebooting a blog can be a crazy task in itself, so I decided to write about my efforts here. Most of my efforts went into first doing some research into what was the best platform to blog on, then what my redesign was going to be, and finally how I configured and programmed everything to work the way I wanted it to. 

So first off, the research!

## What was the best blogging platform for me?

## Configuring and setting up 😩

Literally this was the worst part of all of this. So remember how I mentioned that I was running `ghost-0.6.x`? Well, I forgot to that when you have a version of ghost that old, you have to make sure you don't install the latest version directly or else it just causes so many problems.

Another thing that I was having trouble with was I was getting this weird `npm install --production` error. It said that while install, `npm` was getting the `ENOMEM` error which on further inspection, meant that my machine was running out of memory *while it was installing updates to ghost*. 

Which is fucking stupid, because Ghost promised me that 512mb was enough memory for a basic blog, but I don't think they were considering updates as part of the memory requirements. But I didn't want to complain at this point, I kinda just wanted to get this done. So I doubled the amount of memory my DigitalOcean droplet had to 1gb, and voila! `npm` now installed all the correct modules without that pesky memory error. 

I'll probably just keep it at 1gb, because I don't want to have to keep switching plans (Digital Ocean memory changes are reversible apparently), and paying a little extra per month isn't that big of a deal to me, especially if I'm going to commit to doing this for the long run.

Next up were the domain name issues and email setup. Ghost needs some kind of email service to work 100% correctly, so I ended up just signing up for Mailgun (which is what apparently they recommend?), and I followed this guide after securing my domain name.

It really takes like an hour two for the domain changes to propogate through, assuming you did everything right. 
