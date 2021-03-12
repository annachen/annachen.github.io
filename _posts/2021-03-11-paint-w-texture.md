---
layout: post
title: Paint with texture
tags: [GAN, art]
excerpt_separator: <!--more-->
---

In the [previous post](/2021/03/07/first-gan.html) we've developed a texture generating GAN that is able to convert a small patch of noise to a higher resolution texture:

<p align="center"><img src="/assets/img/paint_w_texture/noise_to_tx.png"/></p>

Using the same networks, I created an application that can convert a drawing with color blobs into a textured painting:

<p align="center"><img src="/assets/img/paint_w_texture/blobs_to_painting.png"/></p>

In this example, I used random crops from some of [my paintings](https://goo.gl/photos/RWheWukHeJtctmxM7) to train the networks, so the generated image has painting-like textures. After the networks are trained, I run many many random sampling of the GAN to create a "palette" of what the GAN is capable of generating. This palette is basically a mapping from the average color of a particular type of texture to a list of latent codes, something like: (in this visualization, I pass the latent codes through the generator to get some sample textures)

<p align="center"><img src="/assets/img/paint_w_texture/palette.png"/></p>

One interesting thing I observed when creating this palette is that I have a preference for a subset of colors in my painting. There're few very saturated colors and I like brown, orange, red, blue more than green. While in general I think this is true, some mode collapse of the GAN probably also contributed.

The rest is easy: using the palette, we can convert an image input to the spatial latent code, sample some noise, and pass it through the generator.
