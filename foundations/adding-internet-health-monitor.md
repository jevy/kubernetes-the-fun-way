---
description: Let's deploy something useful and provide some value for all your hard work
---

# Adding Internet Health Monitor

Healthchecks is a really nice SaaS that you can set up to expect an HTTP call at a set interval, and send you a notification if it didn't get it. This could be helpful for detecting a number of things:

* Your k8s cluster is broken
* Your internet or power is out

They have a free tier which is good enough for what we are doing. Let's visit their site [https://healthchecks.io/](https://healthchecks.io/) and Sign Up

![Healthchecks Landing Page](../.gitbook/assets/healthchecks.png)

Once you sign up, create a new "check" and change the schedule so it expects to receive a request every 5 minutes:

![](../.gitbook/assets/fiveminutes.png)

Awesome! Now the fun part. Let's start by created a directory structure you want. This is only to keep you organized, and nothing about this structure is important for Kubernetes:

```text
$ mkdir -p networking/healthcheck
$ cd networking/healthcheck
```

In the future, we could make a `Deployment` Kubernetes Objects and a script inside , but here we just want something SUPER simple to make your cluster useful. Let's  use the `CronJob` Kubernetes Object. Create a file called `cronjob.yaml` and paste this in it:

```text
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: healthcheck
spec:
  schedule: "*/5 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: healthcheck
            image: curlimages/curl
            imagePullPolicy: IfNotPresent
            command:
            - /usr/bin/curl
            - -fsS
            - -m 10
            - https://hc-ping.com/<the url from healthcheck>
          restartPolicy: Never

```

The highlights of what we are doing here:

* Line 2 is telling Kubernetes what kind of "Object" this this. It's a simple cronjob
* Line 6 - Is the frequency we want to run the job. This can be whatever you want. Check out this [Crontab Guru](https://crontab.guru/) to change it.
* Line 7-10 - Kubernetes uses "templates" since it is designed to scale by making it easy to run duplicate pods and jobs. 
* Line 13: the image that we want to run. Since it's a simple curl command, we can use a purpose built curl image. By default, it uses the Docker Hub repo and you can see the image we are using [here](https://hub.docker.com/r/curlimages/curl). 
* Line 15 - 19 - This is the command we want to run in the container.

