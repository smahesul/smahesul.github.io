---
layout: post
title:  "Sweep Job"
date:   2016-01-18 14:14:38 -0500
categories: GRAPLEr
---
<p>The function allows user to submit an experiment to a GRAPLEr service running on endpoint graplerURL. The input files should be placed in ExperimentRootDir.</p>{: .text-justify} 

User can optionally run a script to filter the results by extracting one or more variables from the output file “output.nc”. 

<p>The function allows user to submit a sweep experiment to a GRAPLEr service running on endpoint graplerURL. The input files should be placed in SimDir.</p>{: .text-justify} 

<p>If a filtername is not provided, the directory structure of experiment root directory should be similar to the below figure:</p>{: .text-justify}

![BatchExperiment without filter]({{ site.url }}/assets/SweepWOFilter.jpg){: .center-image }

Example: 

{% highlight ruby %}
graplerURL<-“http://graple-service.cloudapp.net”
expRootDir<-"c:/ExperimentRootDir"
setwd(expRootDir)
expId1<-GraplePostProcessRunExperiment(graplerURL, expRootDir)
{% endhighlight %}

If a filtername is provided, and the experiment root directory has a folder “FilterParams” which consists of a file “FilterParams.txt” (An R script with the “filtername” should be present on the server), then both these files are merged to form a filter “PostProcessFilter.R” which will be used to filter the results. 
The “FilterParams.txt” file consists of the parameters required for the filter (filtername - chosen by the user). The directory structure should be similar to the below figure:

![BatchExperiment with filter]({{ site.url }}/assets/SweepWithFilter.jpg){: .center-image }

Example: 

{% highlight ruby %}
graplerURL<-“http://graple-service.cloudapp.net”
expRootDir<-"c:/ExperimentRootDir"
filterName <- "Filter1.R"
setwd(expRootDir)
expId2<-GraplePostProcessRunExperiment(graplerURL, expRootDir, filterName)
{% endhighlight %}

However, if a filtername is provided and experiment root directory does not have a “FilterParams” file, then it is expected that the filtername chosen has the parameters required and it will be used as a filter directly.
