---
title: "Test Image #2"
date: 2021-10-19T09:36:25Z
publishDate: 2021-10-19T09:36:25Z
categories:
    - Markdown Images
tags:
    - Example Post
author: "Daniel F. Dickinson"
imageLinkFull: true
imageAltAsCaption: true
imageAddWrapper: span
imageAddClass: markdown-image-wrapper
weight: 10
---

## Via Markdown (span wrapper, alt as caption):

![Photo of a rock garden with tulips and rust-coloured plants](backgarden-tulips+rocks.png)

## Via figure shortcode (but \<div> as wrapper):

{{< figure class="responsive-div" image_wrapper="div" title="Figure 1: Differences between markdown figures and figure shortcode" src="backgarden-tulips+rocks.png" alt="Photo of a rock garden with tulips and rust-coloured plants" caption="For a figure caption can be different than alt text">}}

## Via figure shortcode (fullheight):

{{< figure class="responsive-figure-fullheight" title="Figure 1: Differences between markdown figures and figure shortcode (full height)" src="backgarden-tulips+rocks.png" alt="Photo of a rock garden with tulips and rust-coloured plants (no caption specified so alt as caption)">}}

Note that due to the use of of srcset and sizes, this actually uses an image sized for the display rather than the full-sized image.

TODO: #10 Allow to disable 'responsive' (srcset and sizes) behaviour via shortcode.

## Via figure shortcode (fullwidth):

{{< figure class="responsive-figure fullwidth" title="Figure 1: Differences between markdown figures and figure shortcode (full width)" src="backgarden-tulips+rocks.png" alt="Photo of a rock garden with tulips and rust-coloured plants (no caption specified so alt as caption)">}}
