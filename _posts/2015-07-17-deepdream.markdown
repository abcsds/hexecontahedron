---
layout: post
title: "DeepDream"
date: "2015-07-17 12:40:06 -0600"
comments: true
tags: google, deepdream, vagrant, ai, english
---
No cognitivist could avoid noticing google's new demonstrations on Deep Learning posted on their [research blog](http://googleresearch.blogspot.mx/2015/06/inceptionism-going-deeper-into-neural.html) this june. Images all over the web like those on google's own [gallery](https://photos.google.com/share/AF1QipPX0SCl7OzWilt9LnuQliattX4OUCj_8EP65_cTVnBmS1jnYgsGQAieQUc1VQWdgQ?key=aVBxWjhwSzg2RjJWLWRuVFBBZEN1d205bUdEMnhB) showing what artificial neural networks "see" when trying to make sense of images make everyone wonder how could a machine make such beautiful, weird, and surprisingly familiar images.

### Running Google's DeepDream

So many people from so many different backgrounds, from scientists to artists, have been so interested in google's deepdreaming that the company decided to open their code. The repo can now be found as an IPython notebook on [github](https://github.com/google/deepdream) so anyone and everyone can have their own deeplearning nerual network, and now thanks to [Gary Arnold's](https://github.com/Dhar) [Image-dreamer Vagrant Box](https://github.com/Dhar/image-dreamer) it's even easier to get experimenting with your own images.

All you need is [VirtualBox](https://www.virtualbox.org/) and [Vagrant](https://www.vagrantup.com) to run the virtual machine that installs all the dependencies. If you want to see exactly what dependencies are installed, you can check out the [Vagratfile](https://raw.githubusercontent.com/Dhar/image-dreamer/master/Vagrantfile)

### Get it running
Once you clone the repo, you must run the vagrant box by calling the `vagrant up` command, this can take up to several hours depending on your machine. Once it finishes, put an image of your liking into the repo's root folder and ssh into the box with `vagrant ssh`.

Once inside the box, you must cd to the root folder `/vagrant`, which is the same folder as the repository on the host, but has been mounted to the guest machine. Here you will find a python script, which has automated the process of running google's deep dream. To run your first test simply type:

```bash
python dreamify.py <input JPEG filename> <output PNG filename>
```

That's it. You can play around google's state of the art deep neural network.
I really appreciate this specific repo, you see; This Vagrantfile has accomplished to reduce hours of installing dependencies, made solution cross-platform, and all on two files (and the README) and three codes. This is a clear example of how technology should be accessible to the public. Anyone with an internet connection and a decent computer can now play around with high end technology, but most important, just reading the code you can start configuring the internals of the system.

### Playing with the network
The principle behind deep neural networks is basically laying several networks one on top of the other. Every step further up is also a further abstraction; This means the first neural networks are sensible to simple features like lines or edges, the next ones might be more sensible to contours or shapes, and all the way up there can be some really complex abstractions like faces, cars, or animals. Therefore, deep neural networks have several possible outputs; one for every abstraction layer (or so). This is the first tweak we can do to our newly obtained DeepDream; by giving the layer name to the python script on the repo, we can select how much abstraction layers do we want our network to look for in the image.

The layer's names are specified in the std output when you run the network. The one running by default is `inception_4c/output`, which seems to be sensible to animal faces, fishes, trees, and building-like structures.

Here is an example of how an image might look after running through this network:

![Original Image]({{ site.static_folder }}/img/DeepDream/orig.jpg)
On top you can see the original image; a picture my friend [Federico](https://twitter.com/tejonBiker) made with his raspberryPI, and on the bottomp the converted image.

![Eyed Image]({{ site.static_folder }}/img/DeepDream/eyes.jpg)


Another option is running the network to output on the `inception_3c/output` layer, which seems to be sensible curves and contours. You do this by adding the name of the layer you wish to output right after the output image when running the script:

```bash
python dreamify.py <input JPEG filename> <output PNG filename> inception_3c/output
```

This might generate an image like this one:

![Flowing Image]({{ site.static_folder }}/img/DeepDream/beto.png)

I invite you to read the script [Gary Arnold](https://github.com/Dhar) has made, tweek it, play arround with it, learn a lot, and [create art](https://www.youtube.com/watch?v=0qVOUD76JOg) ;) . I hope you'll show it arround in your social networks and tag me.
