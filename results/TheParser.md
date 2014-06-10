---
layout: post
title: The Parser
author: Andrew Mahan & Diego Escalante
---

# {{ page.title }} #
## by {{ page.author }} ##

In order to answer the question, “what harmonic practices are present in pop/rock represented by the McGill Billboard corpus?” the data from the corpus needed to be parsed. Essentially, before the data could be analyzed, it was necessary to sift through it, taking what is useful out of the nearly thousand files accessible to us, and placing that useful information into a neat and organized CSV file (a file type that stores tabular data; think Excel). Our team was tasked to create this parser.

## The Input ##

Each file in the billboard corpus contains musical annotations for a song. they hold information on the song name, artist, metre, chords and their qualities, among other things. Just as an example, the beginning of The Beatles’ Love Me Do file (including the intro) looks like so:

    \# title: Love Me Do  
    \# artist: Beatles  
    \# metre: 4/4  
    \# tonic: G  
    0.000000000 silence  
    0.417959183 A, intro, | G:maj | C:maj | G:maj | C:maj |, (harmonica  
    7.010816326 | G:maj | C:maj | G:maj | G:maj |, harmonica)

In the example above, the first four lines correspond to general information about the song. After that, the lines correspond to each phrase in the song. The first column in the line is the timestamp for where the phrase occurs in the recording that the transcriber used. Next, there is form information if the form changes with that phrase. This can be seen in the second phrase line where the intro formal functions starts with form letter A. After that, there is the string of chords delimited by “\|” that appear in phrase. Everything encapsulated by “\|”s denotes a bar the the phrase. Finally, any info about instrumentation is noted. While this example represents a large chunk of songs, there are a myriad of special cases that are discussed below.

## The Output ## 

The parser churns out a csv file containing a line of data for each chord in all the songs parsed. Each line in the csv file was formatted like so:

| Song name | Form function | Original chord | Roman numeral | Chord quality | Current bar in phrase | Total bars in phrase | Arrow (bool) |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| | | | | | | | | |
{: rules="groups"}


So, for example, taking the beginning of Love Me Do’s data as the input, the parser would return this output:

| Song name | Form function | Original chord | Roman numeral | Chord quality | Current bar in phrase | Total bars in phrase | Arrow (bool) |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| LoveMeDo | intro | A | G:maj | I | maj | 1 | 4 | 0 |
| LoveMeDo | intro | A | C:maj | IV | maj | 2 | 4 | 0 |
| LoveMeDo | intro | A | G:maj | I | maj | 3 | 4 | 0 |
| LoveMeDo | intro | A | C:maj | IV | maj | 4 | 4 | 0 |
| LoveMeDo | intro | A | G:maj | I | maj | 1 | 4 | 0 |
| LoveMeDo | intro | A | C:maj | IV | maj | 2 | 4 | 0 |
| LoveMeDo | intro | A | G:maj | I | maj | 3 | 4 | 0 |
| LoveMeDo | intro | A | C:maj | IV | maj | 4 | 4 | 0 |
{: rules="groups"}

## Parsing choices ##

The data files from the billboard include extensive annotation to describe each song in great detail. However, for the purposes of our project, we only needed specific information. Because our analysis was only concerned with harmony and form, things like metre and instrumentation were not necessary. The following is a list of special annotations and what our parser does with them:

-   **\| N \|**: Recorded in csv file as a non-harmonic.

-   **&pause**: Brief pauses of arbitrary length. Recorded in csv file as a non-harmonic.

-   **\| \* \|**: The \* denotes passages that were too musically elaborate to merit beat-level chord annotations. Ignored, not recorded.

-   **xn**: Repeat the phrase n times. Parser effectively repeats the phrases appropriately in the csv file.

-   **(\#/\#)**: We are not concerned with the metre, and so the parser ignores this.

-   **\| C:maj . . \|**: Dot means to repeat the previous chord. Ignoring, as we don’t care about duration.

-   **Z**: Denotes non-musical passages in the audio such as noise or spoken words. Recorded as a Non-harmonic in the csv file.

-   **B’**: Sometimes there are apostrophes following form content indicators. Recorded just like the other indicators, keeping the apostrophes in the csv.

-   **Timestamps**: As seen in the example above, timestamps occur at the beginning of each line. Our analysis was not concerned with this, and so they are completely ignored and not recorded.

-   **Leading Instruments**: Things like “(harmonica” in the example above. Again, we were not concerned with this. They were ignored and not recorded.

-   **-\>**: The arrow denotes a musicological hint that the phrase in which the arrow appears is musically elided into the following phrase. We gave this arrow its own column in the parser, as seen above.

For more specific information on the format of the data, you can visit the [McGill Billboard Project](http://www.google.com/url?q=http%3A%2F%2Fddmal.music.mcgill.ca%2Fbillboard&sa=D&sntz=1&usg=AFQjCNGPjlHiq8-zrKzjf1DXD9hXNGk7UQ).

Apart from taking account all these different annotations, the parser had to deal with a few discrepancies in the input data, like missing commas, an incorrect tonic note, or other minor details. In some instances, the transcriber decided to use different syntax in order to notate form changes which had to be dealt with.

