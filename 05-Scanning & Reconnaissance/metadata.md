# Metadata

## Overview

This challenge involves interacting with the AWS EC2 Instance Metadata Service (IMDS) AWS automatically runs a small HTTP server on every EC2 instance that exposes metadata about the instance


In this challenge, the service is exposed through a provided hostname and port

The goal is to enumerate metadata endpoints and retrieve information about the cloud instance


## Gathering Instance Information

Open the provided host in a browser or with `curl`:

```
http://[hostname]:[port]
```

This indicates the AWS metadata API version Next, append `/latest/`:


You should see:

```
dynamic
meta-data
user-data
```

The most important directory is `meta-data` Enumerate it with:


Manually explore these directories to gather instance information  
 About the `availability zone`, `security-credentials` and `instance-type`


## Operating System Name

Get the AMI ID:

```
http://[hostname]:[port]/latest/meta-data/ami-id
```

Example:

`ami-0abcdef12345`

Look up the AMI at:


```
https://cloud-images.ubuntu.com/locator/ec2/
```

## Finding the Flag

Start by finding the mac endpoint:

```
http://[hostname]:[port]/latest/meta-data/network/interfaces/macs/
```

Example output:

`02:7b:64:49:27:21/`

Use the returned MAC address and navigate to:


```
http://[hostname]:[port]/latest/meta-data/network/interfaces/macs/[mac]/vpc-ipv4-cidr-blocks
```

The flag is located here
