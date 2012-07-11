---
layout: post
title: Visual Studio Code Metrics Without Visual Studio
permalink: 2011-06-23-visual-studio-code-metrics-without-visual-studio.html
---

Recently I wanted to integrate the Visual Studio code metrics into my build. I use TeamCity as the build server. After some searching I found the Visual Studio Code Metrics Power Tool which allows you to generate the metrics from the command line. As a general rule I do not install Visual Studio on my build servers, but this tool appeared to require the installation of Visual Studio. This is NOT true. It only requires FxCop. When you install the tool in puts two files into your FxCop directory.

![metrics files](/img/metricsfiles.png)

In order to run the tool my build server all I had to do was copy those two files into my FxCop directory and viola, code metrics. In addition, you can also copy the FxCop directory to your build server so there isn't even a requirement for FxCop to be installed with the installer. I find this helpful because the location of FxCop installed with Visual Studio is not the same as when installed with the Windows SDK.