---
layout: post
title: "AWS Lightsail sucks"
description: 
summary: 
---

After a long time managing my own servers, either at home or VPSs on Linode, I wanted to broaden my repertoire a little by getting some hands-on experience with AWS. AWS offers two VPS products, EC2 and Lightsail. Lightsail is meant to be their simple, easy-to-use offering, and can be configured pretty quickly.

To test Lightsail out, I migrated my website [nflfunindex.com]() from its current Linode host, a $5/mth box with 1 vCPU and 1GB RAM. I first heard about Linode on Jupiter Broadcasting podcasts and have been very happy with it. Love the product, love the company. The only reason I'm trying AWS is because so many damn job descriptions want experience with it!

Setting up a Lightsail instance was incredibly easy, and the price of $3.50/mth for the 512MB RAM box is pretty hard to beat. I chose my preferred server disto, Ubuntu Server 20.04, configured a static IP and uploaded my public SSH key and within a couple of minutes the box was up and ready to SSH into. So far, so good.

My website is containerised with Docker and orchestrated with docker-compose so it was super easy to migrate. Stop the containers with `dcp down` (`dcp` is a great alias for `sudo docker-compose`!) then bundle the directory into a tarball and copy over to the new machine. Untar, and `dcp up` and we're away.

So why does Lightsail suck? Well, let me answer that with another question. What is the most important feature of a cloud hosting product? I think most people would say **reliability**.

And here's the rub - Lightsail isn't reliable!

As I write this, users trying to reach [nflfunindex.com]() are being greeted with a Cloudflare error page with a 522 error code. I try to SSH into the box and the operation times out. I try to open Lightsail's own in-browser SSH tool and it returns a completely blank terminal with no cursor. According to AWS, the box is running, the CPU usage has consistently been in the 'sustainable zone' (side note: that's a zone that shouldn't even exist. Either I have a vCPU to use or I don't). According to AWS, everything is fine.

Thanks but no thanks, Jeff and Andy. I'll be sticking with Linode for my VPS needs from now on.