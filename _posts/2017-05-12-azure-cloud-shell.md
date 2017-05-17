---
layout: default
title: "Azure Cloud Shell"
categories: Azure 
---

## Azure Cloud Shell

Last week during Build 2017 Microsoft announced the [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview) (Preview).

### Browser-based Shell Experience

Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind. Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.

This cool because now you can use the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview) directly from the portal.

My favorite feature is that you can actually have a stateful storage drive wthin Azure Store.

![Azure Cloud Shell]({{ site.url }}/assets/images/storage.png)

One thing I wanted to do after I was done playing was to reset my "clouddrive" so it's nice and clean. To do this inside cloud shell, run **`clouddrive unmount`** which will reset your account back and start from scratch.

![Unmout Clouddrive]({{ site.url }}/assets/images/unmount.png)

[back]({{ site.baseurl }}{% link index.md %})