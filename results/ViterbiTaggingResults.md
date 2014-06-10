---
layout: post
title: Viterbi Tagging Results
author: Aaron Davis
---

# {{ page.title }}  
{{ page.author }} #

## Overview ##

I asked the question, “Given a sequence of harmonic roots (roman numerals), can we automatically determine what formal module these roots belong to?” The question has two sides. First, is there enough of a relationship between harmony and form to make this question answerable? And second, which computational methods can be used to determine formal elements from the chord roots?

## Approach ##

I decided to try using a hidden Markov model (HMM) with the Viterbi algorithm. The Viterbi algorithm answers the question, “Given a sequence of observed states, can we automatically detect a corresponding sequence of ‘hidden’ states?” In this case, the observed states were the harmonic roots, and the hidden states were the formal modules (verse, chorus, etc.). The Viterbi algorithm requires two probability tables, the transition probabilities, and the emission probabilities.

The transition probabilities indicate the probability that a given hidden state (in this case, formal module) will follow another. Mathematically, this is Pr( hidden\_state\_i | hidden\_state\_i-1 ). An example is Pr( verse | chorus ), or what is the probability that a verse will follow a chorus.

The emission probabilities indicate the probability that a certain observed state will be produced by a given hidden state. Mathematically, this is Pr( observered\_state\_i | hidden\_state\_i ). An example is Pr( II | verse ), or the probability that a II chord will be “emitted” from a verse hidden state.

Both of these probability tables are calculated based on the maximum likelihood estimates from the McGill Billboard corpus.

The rationale for trying this approach is that similar looking problems, such as part of speech tagging in natural language processing (NLP), are tackled very successfully with this algorithm. Additionally, other uses of HMMs have already been tried on this corpus (Expectation Maximization for instance), so there was no point in repeating what has already been done.

## Results ##

Normally, one would divide the corpus into training and test segments, and assess the system based on accuracy, precision, and recall. However, preliminary tests using the same corpus as both test and training data revealed that the accuracy was so low that this system appears basically useless for form tagging.

## Analysis ##

So why did this approach fail to work? The fundamental reason appears to be that harmony is not correlated with form enough for this approach to work. In order for this system to work, certain chord changes would have to be highly correlated with certain formal changes. This correlation is just not there in the data (at least it does not seem to be based on what I have found so far). Typically, the system would predict “intro” correctly (which isn’t a big surprise since this occurs first nearly always), and then get stuck on whatever the next formal element is and stay there for the rest of the song. This is because the probability of a “verse” staying a “verse” is very high compared to the probability of a transition to another formal element.

I attempted to offset this problem by using the bar\_of\_phrase data in addition to the formal module as the hidden state, so “verse\_1”, “verse\_2”, etc., as opposed to just “verse”. This yielded slight improvements of the accuracy, but nothing substantial. The fundamental problem remains, that the end of formal modules doesn’t seems to correspond with any particular chord change, thus there is no way the system would know how to predict these.

# Musical Knowledge ##

In order to prepare the corpus for this kind of tagging, we needed to transform the corpus from its native haphazard form labels, to more up-to-date, theoretically sound form labels. This required study of form in pop/rock, in order to replace the old form labels with new ones. Some of these replacements were done algorithmically in the code, and some were done manually by listening to songs with the musicians and determining the formal structures by ear.

