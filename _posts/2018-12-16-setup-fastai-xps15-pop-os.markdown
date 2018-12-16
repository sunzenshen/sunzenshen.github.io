---
layout: post
title: Setting up fast.ai on an Dell XPS15 9570 with Pop!_OS
categories: [Tutorials]
tags: [fast.ai, Python, Jupyter]
description: Hopefully this doesn't nuke anyone's laptop.
---

Setting up fast.ai on an Dell XPS15 9570 with Pop!_OS
---------------------

In these notes, I will attempt to recall the main points of interest
that I encountered as I worked to port over the
[fast.ai paperspace setup](https://course.fast.ai/lessons/lesson1.html)
on a Dell XPS 15 model 9570.

Laptop Specifications
---------------------
The specific model that I am using for this writeup is the XPS9570-7085SLV-PUS.
In case the internet loses all recollection of the contents of this model, it includes:
* Intel® Core™ i7-8750H Processor 2.2GHz (6 cores)
* 32GB DDR4 2666MHz RAM
* 1TB M.2 PCIe Solid State Drive
* 4GB NVIDIA® GeForce® GTX 1050 Ti Graphics

Installing Pop!_OS as dual boot with Windows 10
-----------------------------------------------
I settled on using Pop!_OS as the Linux distribution.
* https://system76.com/pop

My reasoning for this doesn't really extend beyond my seeing testimonials that Pop!_OS runs on a Dell XPS15 with minimal fuss after installation, especially if the Nvidia version of their ISO images is used to have drivers right after install.
System76, the distro maintainer, also maintains their own apt installs for the NVIDIA CUDA Toolkit. I am also using the 18.04 LTS version, as I saw some complaints that Linux on XPS13/15 installs could get corrupted from upgrading between major versions.

These articles were especially helpful for getting the Pop!_OS disk image to be recognized on boot, along with installation:

* [How to dual boot Windows 10 and Ubuntu 18.04 on the 15 inch Dell XPS 9570 with Nvidia 1050 ti GPU](https://medium.com/@pwaterz/how-to-dual-boot-windows-10-and-ubuntu-18-04-on-the-15-inch-dell-xps-9570-with-nvidia-1050ti-gpu-4b9a2901493d)

Patrick Waters' guide is a great overview of what one can expect when installing a Linux distro on an XPS 15.
In particular, the instructions on how to work with a Bitlocker encrypted Windows 10 install are particularly important.
Save your Bitlocker recovery keys!!! You'll type them in alot!
However, take a look at the rest of this section to see were I diverged from that overview post.

* [Personal experience of installing Ubuntu 18.04 LTS on XPS 15 9570](https://medium.com/@peterpang_84917/personal-experience-of-installing-ubuntu-18-04-lts-on-xps-15-9570-3e53b6cfeefe)
* [Switching between AHCI and RAID on the Dell XPS 15 (9560)](https://gist.github.com/chenxiaolong/4beec93c464639a19ad82eeccc828c63)

One panic surprise I encountered was that I couldn't enable Windows Safe Mode after I had switched to AHCI from the BIOS menu.
Peter Pang and chenxiaolong's posts point out that it's easier to enable Safe Mode _before_ enabling AHCI, otherwise Windows will not boot.
Also, you can't use pin or fingerprint login while in Safe Mode, so plan how to log into Safe Mode accordingly.

* https://support.system76.com/articles/live-disk/

I second the recommendation of using Etcher for writing a bootable USB stick.

When partitioning for my Linux install, I allocated 1GB for /boot, 32 GB for swap (to match the RAM), and the rest for my root directory.

After Pop!_OS is installed, my favored dual boot setup is to open the BIOS settings again, and to set the Windows boot as the default option.  When I want to boot into Pop!_OS, I hold F12 to bring up the boot options.

I haven't totally gone through Patrick Waters' Post-Installation recommendations, as Pop!_OS seemed to work well out of the box.  I plan to look over [JackHack96's scripts](https://github.com/JackHack96/dell-xps-9570-ubuntu-respin) later to see if there are any interesting tweaks I should pick up.

Setting up fast.ai with the Paperspace script
---------------------------------------------
To set up fast.ai's course repository, I started off with the paperspace script:
* http://files.fast.ai/setup/paperspace

However, there were a few tweaks I needed to make, to get it working:
* https://github.com/sunzenshen/fast-ai-notes/blob/master/paperspace_pop_os.sh

To summarize my divergence:
* The directory of `/etc/apt/apt.conf.d/*.*` does not exist, so I skipped that removal step.
* On both a Ubuntu VM and with this Pop!_OS install, I had trouble using apt install to get the NVIDIA CUDA Toolkit. Specifically I was getting the following error:

```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 cuda : Depends: cuda-10-0 (>= 10.0.130) but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
```

My workaround for this dependency error was to use Pop!_OS's maintained version of the NVIDIA CUDA Toolkit:
* https://support.system76.com/articles/cuda/

(Also note that virtual machines do not support GPU passthrough as of this writing.  Don't be like me and not realize this when setting up an Ubuntu image on a VMWare player.)

Setting up Jupyter Notebook to run from localhost
-------------------------------------------------
To check that my setup is working, I followed the post-paperspace-setup steps from lesson 1:
* https://course.fast.ai/lessons/lesson1.html

The following assumes the commands are run in ~/fastai/ :

Do once in awhile:
```
git pull
conda env update
```

Because I am running jupyter from my laptop, I need to set the IP to localhost, otherwise I will get the errors:
```
KeyError: 'allow_remote_access'
...
ValueError: '' does not appear to be an IPv4 or IPv6 address
```

The solution was found in the discussion at
* https://forums.fast.ai/t/jupyter-notebook-keyerror-allow-remote-access/24392/8

In a nutshell, I needed to create jupyter_notebook_config.py in ~/fastai/, and to set the IP address to localhost:
```
touch jupyter_notebook_config.py
jupyter notebook --generate-config jupyter_notebook_config.py “c.NotebookApp.ip = ‘127.0.0.1’”
```

Then the notebooks could be hosted locally using the command:
```
jupyter notebook
```

Sanity Check: Deep Learning 2018 Lesson 1
-----------------------------------------

The first lesson could then by found at:
http://localhost:8888/notebooks/courses/dl1/lesson1.ipynb

And thankfully, the notebook indicated that cuda and cudann were both enabled (returning true)!

```
torch.cuda.is_available()
torch.backends.cudnn.enabled()
```

Because I was not using Paperspace or Crestle, I needed to download the dogs and cats dataset into the ~/fastai/data/ folder:
```
~/fastai/data$ wget wget http://files.fast.ai/data/dogscats.zip
```

So how long did it take to use the resnet34 model for the first dogs/cat exercise?
```
100%|██████████| 360/360 [06:26<00:00,  1.17it/s]
100%|██████████| 32/32 [00:33<00:00,  1.22it/s]

Epoch
100% 2/2 [00:04<00:00, 2.25s/it]

epoch      trn_loss   val_loss   accuracy                     
    0      0.044299   0.028482   0.989     
    1      0.042639   0.026683   0.99                          

[array([0.02668]), 0.99]
```

6-7 minutes? Not as fast as the 20 seconds expected runtime from the lesson notes, but pretty good for a laptop!

Wrapup
------
That about covers all the major obstacles that traumatized me enough to remember them after the entire setup experience.
If you also have an XPS 15 and are having issues setting up a similar environment, feel free to [send me a message](https://twitter.com/@sunzenshen) or [open an issue on Github](https://github.com/sunzenshen/fast-ai-notes/issues).
I can't promise that I'll get your issue resolved or that my suggestions won't nuke your existing Windows install,
but hopefully I can remember something that I forgot to put into this guide.

Best of luck on your own setup!

-Alan


> Like this post, or would like to discuss it on some sort of forum?
> Feel free to post it on your favorite social media site (HN, Reddit, Lobste.rs, etc), and to send me the link!
> I promise to relink the discussion thread from this post, and to upvote your submission.
> It'll be win-win: you'll rake in the sweet-sweet karma/points/upvotes,
> and I won't need to worry about hunting spam-bots in an otherwise empty Disqus thread.
