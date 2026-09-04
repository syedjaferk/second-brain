---
layout: post
title: 'Docker Ep 3 : Virtual Machines VS Containers'
date: 2024-08-12 08:40:04+00:00
render_with_liquid: false
category: Docker
tags:
- Containers
- VirtualMachines
- Linux
- DevOps
- Software
---



<figure class="wp-block-table"><table class="has-fixed-layout"><tbody><tr><th class="has-text-align-center" data-align="center"><strong>SNo.</strong></th><th><strong>Virtual Machines(VM)</strong></th><th><strong>Containers</strong></th></tr><tr><td class="has-text-align-center" data-align="center">1</td><td>VM is a piece of software that allows you to install other software inside of it so you control it virtually as opposed to installing the software directly on the computer.</td><td>While a container is software that allows different functionalities of an application independently.</td></tr><tr><td class="has-text-align-center" data-align="center">2.</td><td>Applications running on a VM system, or hypervisor, can run different OS.</td><td>While applications running in a container environment share a single OS.</td></tr><tr><td class="has-text-align-center" data-align="center">3.</td><td>VM virtualizes the computer system, meaning its hardware.</td><td>While containers virtualize the operating system, or the software only.</td></tr><tr><td class="has-text-align-center" data-align="center">4.</td><td>VM size is very large, generally in gigabytes.</td><td>While the size of the container is very light, generally a few hundred megabytes, though it may vary as per use.</td></tr><tr><td class="has-text-align-center" data-align="center">5.</td><td>VM takes longer to run than containers, the exact time depending on the underlying hardware.</td><td>While containers take far less time to run.</td></tr><tr><td class="has-text-align-center" data-align="center">6.</td><td>VM uses a lot of system memory.</td><td>While containers require very less memory.</td></tr><tr><td class="has-text-align-center" data-align="center">7.</td><td>VM is more secure, as the underlying hardware isn’t shared between processes.</td><td>While containers are less secure, as the virtualization is software-based, and memory is shared.</td></tr><tr><td class="has-text-align-center" data-align="center">8.</td><td>VMs are useful when we require all of the OS resources to run various applications.</td><td>While containers are useful when we are required to maximize the running applications using minimal servers.</td></tr><tr><td class="has-text-align-center" data-align="center">9.</td><td>Examples of Type 1 hypervisors are KVM, Xen, and VMware. Virtualbox is a Type 2 hypervisor</td><td>Examples of containers are RancherOS, PhotonOS, and Containers by Docker.</td></tr></tbody></table></figure>


## Related Posts
- [[Locust EP 3: Simulating Multiple User Types in Locust]]
- [[Python List : The Delivery Man's Busy Day]]
- [[HAProxy EP 3: Sarah’s Adventure with L7 Load Balancing and HAProxy]]
- [[Docker Ep 2 : The Tale of Magic Kitchen : A Docker Architecture]]
- [[Docker Ep 4 : The Digital Tea Kadai - Client Server Architecture &amp; Docker]]

