# Setting up your persistent storage locations

As mentioned in Foundational Concepts, storage requirements is decoupled from storage location, in a home lab environment it might feel like a bit of overkill. 

### Decide where you want to host your data

The first thing you need to do is decide where you want to put your data. Personally, I have a Synology diskstation serving up a single NFS share that I have Kubernetes to manage. If you don't have an NFS storage option, you can use something like S3 to get started since it's cheap, and highly available. It breaks the mold of "self hosting" but to get started it works fine. You can always migrate later.

