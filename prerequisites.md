# Prerequisites

### 

There are few things you will need to get started:

#### Hardware

You can start a homelab with very modest hardware. As you deploy more things, your appetite for more hardware will likely grow but you can start small and still have a nice little place to play.

You want to start with something that can run 24/7 that has either amd64 \(intel laptops, desktop machines etc\) or arm \(raspberry pi, laptops or other mini computers\). Installing essentially any common Linux distribution on there is how to get started.

**Special note about SD cards**: If you do go the Raspberry Pi route, you will save yourself many headaches if you buy card\(s\) with high random read/write. I used [this benchmark](https://www.cameramemoryspeed.com/reviews/micro-sd-cards/) find one that wasn't too expensive and of high quality

#### Skills

At a minimum you should have skills in two underlying technologies:

* Basic Linux administration \(installing a distro, installing packages, using the command line, ssh etc\)
* Experience using Docker containers \(running them, a basic understanding about how they work etc\)
* Git is extremely useful so you can keep track of things that work and you can feel free to roll back if you messing things up.

From there you should be good to go! Let's get started

#### A place to persist data

Could be a local NFS share, local SD/HDD card \(not ideal\) or we can use something in the cloud like AWS.

