---
layout: post
title: "Demo: Monitoring Forest Disturbances"
date: 2016-03-24
description: "One of my PhD chapters looked at monitoring small-scale forest disturbances in an Afro-montane forest system in southern Ethiopia. We used dense Landsat time series to map these disturbances over time."
---

One of my PhD chapters looked at monitoring small-scale forest disturbances in an Afro-montane forest system in southern Ethiopia. We used dense Landsat time series to map these disturbances over time. 'Dense', meaning we didn't composite or take annual imagery, but with persistent cloud cover over much of the area (a problem frequently encountered in the tropics), the time series was anything but dense. Still, we were able to capture much of the typically small-scale disturbances that occur in these landscapes.

Some of the code from this paper has been rolled into the [bfastSpatial](http://github.com/dutri001/bfastSpatial) R package, which I have been working on in collaboration with one of my PhD colleagues Loic Dutrieux (check out his site <a href="http://loicdutrieux.com" target="_blank">here</a>).

{% highlight r %}
library(devtools)
install_github("dutri001/bfastSpatial")
install_github("bendv/bfastPlot")
{% endhighlight %}

