---
layout: post
title: Understanding Cluster Data
author: Kyle Rooney
---

# {{ page.title }} #

## by {{ page.author }} ##

Let’s take a look at some cluster analysis data that was ran on the McGill Billboard Corpus of songs, starting with the first cluster of 6 we can begin to see identifying results as to what songs are grouped in this cluster.

| cluster1of6.csv | I | II | III | IV | V | VI | VII | bII | bIII | bV | bVI | bVII |
|-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| I | 0.2751 | 0.0807 | 0.0329 | 0.2356 | 0.1715 | 0.1643 | 0.0055 | 0 | 0.0011 | 0 | 0.0178 | 0.0148 |
| bII | 0.4397 | 0.0357 | 0 | 0 | 0 | 0 | 0 | 0.2223 | 0.1071 | 0.0259 | 0 | 0.1607 |
| II | 0.1719 | 0.0906 | 0.0986 | 0.2715 | 0.228 | 0.0577 | 0.0175 | 0.0114 | 0.0007 | 0.0114 | 0.0009 | 0.0399 |
| bIII | 0.0069 | 0.1435 | 0.0222 | 0.3056 | 0.0322 | 0.0556 | 0 | 0.0556 | 0.1551 | 0.0222 | 0.1734 | 0.0139 |
| III | 0.0185 | 0.2447 | 0.0911 | 0.2451 | 0.0519 | 0.2697 | 0 | 0.0157 | 0.0321 | 0.0147 | 0 | 0.0147 |
| IV | 0.0665 | 0.0243 | 0.0199 | 0.055 | 0.8087 | 0.0083 | 0 | 0 | 0.0033 | 0 | 0.002 | 0.0115 |
| bV | 0 | 0 | 0.3333 | 0 | 0.1667 | 0 | 0.1667 | 0.3333 | 0 | 0 | 0 | 0 |
| V | 0.6019 | 0.0188 | 0.0176 | 0.1369 | 0.13 | 0.0612 | 0 | 0.0046 | 0.0129 | 0 | 0.0122 | 0.0002 |
| bVI | 0.2086 | 0 | 0 | 0.0707 | 0.3159 | 0.1111 | 0 | 0.0556 | 0.0278 | 0 | 0.0804 | 0.13 |
| VI | 0.0948 | 0.0812 | 0.0546 | 0.4197 | 0.1859 | 0.1415 | 0.0081 | 0 | 0.0025 | 0.0013 | 0.0081 | 0 |
| bVII | 0.2729 | 0.0667 | 0 | 0 | 0.1854 | 0.0267 | 0.075 | 0 | 0.2 | 0 | 0.1067 | 0.0667 |
| VII | 0.3988 | 0 | 0.0186 | 0.2671 | 0.1786 | 0 | 0.0536 | 0 | 0.0833 | 0 | 0 | 0 |

Primarily what we want to look for in this data are chord transitions that we can say without a doubt are the most likely to occur, so we can begin to identify what is going on in this cluster.

> I -\> I, IV, V, and VI (all around 20-25%)  
bII -\> I, and bII  
II -\> IV, and I  
bIII -\> IV, and bVII  
III -\> II, IV

Now the transition probabilities for these first 5 chords don’t have any one transition that helps to identify the results, but looking at the next chord IV we see an 80% transition to V, which is a big tell that it occurs in almost all of the songs in this cluster of data.

>  IV -\> V(80%)  
bV -\> III, and bII

The easiest way to find out what musical style this cluster of data is encompassing is to find one true transition in the chords and to follow that transition down the line to find out what all of these songs have in common. The next big tell in this data is the transition off the V chord, which we identified as being prevalent from the IV -\> V (80%) data.

> V -\> I(60%)  
bVI -\>I, and V  
VI -\> IV(42%), V  
bVII -\> I, V  
bVII -\> I, IV, V

Now by looking at this data we can create a simple chord progression that is most likely to occur within this cluster and from that we can identify what style these songs have in common.

IV -\> V -\> I -\> VI is one of the most prevalent chord progressions in this data set. The starting root for this chord progression could be any of these four, but by looking at this data we can see very classical styles in this cluster.

> IV -\> V.  
V -\> I.  
VI -\> IV.  
I -\> IV, V , VI.

That is how you analyze cluster data from chord transitions, I hoped this example breakdown helped you better understand how to read this data. In conclusion the primary thing to look for in this data are transitions that are very likely of occurring and following the transition down the line to create a chord progression.
