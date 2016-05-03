---
layout: post
title: Clustering
author: Chris Rooney
---

# {{ page.title }} #

## by {{ page.author }} ##



I’ll begin by explaining the method that we used to determine the transitional probabilities per song, how we clustered that data, and some of our preliminary analysis of the output.

We first computed the transitional probabilities from one chord to next for each individual song. The *transition\_probability-songBySongAverage.py* file (in the [GitHub repository](https://github.com/corpusmusic/billboardcorpus)) was used with our parsed McGill billboard corpus csv file (*AlldataWithNonHarmonics.csv*) to compute these probabilities and output them to a table for easier future analysis. This file (*output.csv*) was slightly modified to work in [Cluster 3.0](http://www.google.com/url?q=http%3A%2F%2Fbonsai.hgc.jp%2F~mdehoon%2Fsoftware%2Fcluster%2Fsoftware.htm&sa=D&sntz=1&usg=AFQjCNGnOUpNQdh2biayrHl2WfLHuC2SuA) and is saved as *output3.txt*.

We then ran *output3.txt* through Cluster 3.0 using a k-means clustering technique measured by Euclidean distance of transitional probabilities per song. The songs in our corpus were divided into a number of different clusters ranging from 2-12, corresponding to the k-value selected for each clustering run. This cluster data is contained in the *ClusterData* folder.

The cluster files were then run through *clusterize.py* to extract the harmonic information from each song in each cluster and output this data into files with the same format as the original parsed McGill billboard corpus csv file. These files are contained in the ClusterizedData folder.

Once we had the songs clustered and in the right form, we ran each of the files in ClusterizedData through our song by song transition probability script to get the chord transition probabilities for all songs in the specified cluster. These files are contained in the OutputClusterizedData folder.

Finally we ran this output through a script to calculate 95% confidence intervals (*confidence.py*) so that statistical analysis could be performed. This data is also contained in the OutputClusterizedData folder.

With just a cursory look at the end product, we are able to see songs clustered into groups with similar styles/genres and more importantly well-defined musical progressions. Further analysis of these clusters should yield very interesting results, unfortunately we ran out of time to complete this analysis.

See Kyle Rooney's post on [Understanding Cluster Data]({{ site.url }}/results/UnderstandingClusterData.html) for more information on interpreting the tables that resulted from this analysis.
