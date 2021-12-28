---
title: Windows - How to check if your PC has TPM for windows 11
published: true
description: Checking if your PC has tpm 2.0 for windows 11
tags: 'windows11, tpm, windows, 11'
cover_image: ./assets/cover.jpg
canonical_url: null
id: 938460
date: '2021-12-28T12:30:55Z'
---

## TPM
[Trusted Platform Module (TPM)](https://docs.microsoft.com/en-us/windows/security/information-protection/tpm/trusted-platform-module-overview) is a hardware-based that provides physical security protection to your data. TPM version 2.0 is required for windows 11, the new version of windows.

## TPM on BIOS
Maybe your PC has the component but you might to enable or update its BIOS version to get ready to use it. So, you could check your PC factory's website to see how to activate it.

You can open the start menu and type **Sytem information** to check if **Secure Boot State** is turned on.

![Image 3](./assets/img3.png)


## Chaking TPM version
There are some examples of how to check your TPM version.

### Management tool
Open the Run dialog. You can use the *Win + R* shortcut for that. Type *tpm.msc* and *Enter*. 

![Image 1](./assets/img1.png)

If you have TPM on your PC you can see a new window with some informations. You should verify **Status** and **Specific version** under *TPM Manufacturer Information*. 

![Image 2](./assets/img2.png)

### Device manager
Open the Run dialog. You can use the *Win + R* shortcut for that. Type *devmgmt.msc* and *Enter*. 

![Image 4](./assets/img4.png)

Or right-clicking start menu button and then click on Device Manager.

![Image 5](./assets/img5.png)

Under **Security devices** you can find **Trusted Platform Module**. Right-click it and click on Properties to see a new window with more details.

![Image 6](./assets/img6.png)

### CMD or PowerShell
You can use CMD or PowerShell to check TPM. Open start menu and type *CMD* or *PowerShell* and run it as **Administrator**.

Use the following command to see more information.

```
wmic /namespace:\\root\cimv2\security\microsofttpm path win32_tpm get * /format:textvaluelist.xsl
```

![Image 7](./assets/img7.png)

To know if TPM is installed, all of three valeus must to be **TRUE** 
- IsActivated
- IsEnabled
- IsOwned

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.
