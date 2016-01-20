---
layout: post
title:  "Batch Job"
date:   2016-01-17 14:14:38 -0500
categories: GRAPLEr
---
<p>The function allows user to submit an experiment to a GRAPLEr service running on endpoint graplerURL. The input files should be placed in ExperimentRootDir.</p>{: .text-justify} 

User can optionally run a script to filter the results by extracting one or more variables from the output file “output.nc”. 

<p>If user desires to run a script, user has to include a file “FilterParams.txt” in the input working directory, which should be placed in a folder “FilterParams”. This file should contain the variables and their corresponding depths. </p>{: .text-justify}

Sample contents of the file should be as below:

{% highlight ruby %}
VarsToAnalyze = c('OXY_oxy','OGM_doc')
Depths = list(NULL,c(1,5,10))
{% endhighlight %}

Additionally user also has to provide the name of a filter script which is already present on the server in the below path:

{% highlight ruby %}
“/datadrive/Graple-flask/GRAPLE_SCRIPTS/Filters”
{% endhighlight %}

A sample script file can be downloaded by clicking on the link below:

<a href="{{ site.url }}/assets/SampleFilter.R">Download Sample Script</a>

If a filtername is not provided, the directory structure of experiment root directory should be similar to the below figure:

![Batch Experiment without filter]({{ site.url }}/assets/BatchWOFilter.jpg){: .center-image }

Example: 

{% highlight ruby %}
graplerURL<-“http://graple-service.cloudapp.net”
expRootDir<-"c:/ExperimentRootDir"
setwd(expRootDir)
expId1<-GraplePostProcessRunExperiment(graplerURL, expRootDir)
{% endhighlight %}

<p>If a filtername is provided, and the experiment root directory has a folder “FilterParams” which consists of a file “FilterParams.txt” (An R script with the “filtername” should be present on the server), then both these files are merged to form a filter “PostProcessFilter.R” which will be used to filter the results.</p>{: .text-justify}

<p>The “FilterParams.txt” file consists of the parameters required for the filter (filtername - chosen by the user). The directory structure should be similar to the below figure:</p>{: .text-justify} 

![Batch Experiment with filter]({{ site.url }}/assets/BatchWithFilter.jpg){: .center-image }

Example: 

{% highlight ruby %}
graplerURL<-“http://graple-service.cloudapp.net”
expRootDir<-"c:/ExperimentRootDir"
filterName <- "Filter1.R"
setwd(expRootDir)
expId2<-GraplePostProcessRunExperiment(graplerURL, expRootDir, filterName)
{% endhighlight %}

<p>However, if a filtername is provided and experiment root directory does not have a “FilterParams” file, then it is expected that the filtername chosen has the parameters required and it will be used as a filter directly.</p>{: .text-justify} 
