---
layout: post
title:  "Special Job"
date:   2016-01-18 14:14:38 -0500
categories: GRAPLEr
---
<p>The function allows user to submit an experiment to a GRAPLEr service running on endpoint graplerURL. The input files should be placed in ExperimentRootDir.</p>{: .text-justify} 

If a filtername is not provided, the archive contents should be similar to the below figure:

![Special Experiment without filter]({{ site.url }}/assets/SpecialWOFilter.jpg){: .center-image }

Example: 

{% highlight ruby %}
graplerURL<-“http://graple-service.cloudapp.net”
simDir="C:/Workspace/SimRoot/Exp5"
JobFileName="sweepexp.tar.gz"
setwd(simDir)
expId5 <- GrapleRunExperimentJob(graplerURL, simDir, JobFileName)
{% endhighlight %}

If a filtername is provided, the archive contents should be similar to the below figure:

![Special Experiment with filter]({{ site.url }}/assets/SpecialWithFilter.jpg){: .center-image }

Example: 

{% highlight ruby %}
graplerURL<-“http://graple-service.cloudapp.net”
simDir="c:/Workspace/SimRoot/Exp6"
JobFileName="sweepexp.tar.gz"
filterName = "Filter1.R"
setwd(simDir)
expId6 <- GrapleRunExperimentJob(graplerURL, simDir, JobFileName)
{% endhighlight %}

<p>However, if a filtername is provided and experiment root directory does not have a “FilterParams” file, then it is expected that the filtername chosen has the parameters required and it will be used as a filter directly.</p>{: .text-justify}
