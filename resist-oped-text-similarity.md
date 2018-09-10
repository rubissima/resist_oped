
***THIS IS A DRAFT OF A POST INTENDED FOR PUBLICATION BY REYNOLDS
JOURNALISM
INSTITUTE***

# Identifying the author behind New York Time’s op-ed from *Inside the Trump White House*, using data science

|                                                |              |
| -------------------------- -------------------- | ------------ |
| *BY: [MICHAEL W. KEARNEY](https://mikewk.com)* | *2018-09-06* |

Yesterday the *New York Times* published an [opinion
piece](https://www.nytimes.com/2018/09/05/opinion/trump-white-house-anonymous-resistance.html)
about the *Resistance Inside the Trump White House*. It was written by
an [anonymous
source](https://www.nytimes.com/2018/09/06/podcasts/the-daily/trump-administration-official-anonymous-op-ed.html)–identified
only as “a senior official in the Trump administration.” It didn’t take
long for President Trump to tweet his reactions:

<blockquote align="center" class="twitter-tweet" data-lang="en">

<p lang="en" dir="ltr">

TREASON?

</p>

— Donald J. Trump (@realDonaldTrump)
<a href="https://twitter.com/realDonaldTrump/status/1037464177269514240?ref_src=twsrc%5Etfw">September
5,
2018</a>

</blockquote>


<blockquote align="center" class="twitter-tweet" data-lang="en">

<p lang="en" dir="ltr">

Does the so-called “Senior Administration Official” really exist, or is
it just the Failing New York Times with another phony source? If the
GUTLESS anonymous person does indeed exist, the Times must, for National
Security purposes, turn him/her over to government at once\!

</p>

— Donald J. Trump (@realDonaldTrump)
<a href="https://twitter.com/realDonaldTrump/status/1037485664433070080?ref_src=twsrc%5Etfw">September
5,
2018</a>

</blockquote>

<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Early speculation about who authored the *Times* op-ed focused on the
use of the word,
[“lodestar”](https://www.huffingtonpost.com/entry/lodestar-mike-pence-anonymous-new-york-times_us_5b905dd5e4b0511db3dec1e1),
an usual term previously used by Vice President Mike Pence in a [CBS
interview](https://www.cbsnews.com/news/mike-pence-pledges-proper-separation-donald-trump-business-empire/).
Others have argued that such an obvious use of a unique term is instead
a form of [intentional
misdirection](https://www.independent.co.uk/news/world/americas/us-politics/lodestar-mike-pence-donald-trump-new-york-times-op-ed-latest-who-author-identity-a8525381.html).
With this back-and-forth about *lodestar* in mind, one can easily
imagine how the exercise of identifying unique words and speculating
about their re-occurrences could continue on, perhaps, indefinitely.

We may never know who actually authored the *New York Times* op-ed about
the *Resistance Inside the Trump Administration*. In retrospect, we may
even judge the search–to identify the anonymous author–itself as poor
form, at least in the democratic sense. I’ll leave those judgments to
the political scientists and democratic theorists. But, for now, I would
like to point out that while the knee-jerk reaction to look at
communication patterns among senior-level White House officials makes
some sense, doing so without leveraging recent advances in data science
would be a huge waste and, for me, a total bummer.

Ultimately, the question “*can past communication records be used to
help identify the author of the anonymous New York Times op-ed?*” is an
empirical one. It’s one that–thanks to the wonders of digital media and
data science–we can start to gain insights from (whether accurate or
not) in a relatively short amount of time. And since a lot of the work I
do involves analyzing political communication on Twitter anyway, I
figured I’d give it a shot as a way to demonstrate what’s possible with
some data science training, plenty of data, and a little bit of time.

## Analysis

First, I grabbed the \[reference\] text from the actual *New York Times*
op-ed.

1.  I collected op-ed text

Next, because I needed some writing/communication samples to compare
against the text of the op-ed, I turned to Twitter–because it only
seemed apropos given communication preferences of the current
administration, and because I just so happened to maintain some
open-source [software for interacting with Twitter’s
APIs](https://rtweet.inf). For the sake of time, I decided to limit my
analysis to members of the President’s cabinet. Plus, given the only
description we have of the author, it seemed fairly safe to assume that
a *senior official in the Trump administration* would, at the very
least, be an accurate description of a member of Trump’s Cabinet.

2.  I collected up to the most recent 3,200 tweets from each
    \[Twitter-using\] member of Trump’s cabinet

With a reference text and a number of samples from Twitter, I then split
the op-ed text by paragraph to roughly match the length of tweets.

3.  I split op-ed text into paragraphs

Using this supply of texts matched to screen name or “op-ed” authors, I
then extracted estimates for over 100 features (numeric representations
of observed patterns in the text) for each string of text. Some examples
of the features include capitalization, punctuation (commas, periods,
exclamation points, etc.), use of white space, word length, sentence
length, use of ‘to be’ verbs, and numerous thesaurus-like
representations of word dimensions (similar to dividing commonly used
words into eighty different topics and then measuring the extent to
which each text used words from each topic).

4.  I converted each text into 107 numeric features

Finally, to get an actual measurement of similarity between the op-ed
and the Twitter screen names, I averaged the numeric featured by author,
and then used those values to estimate the correlations (measure of
association ranging from -1 to 1) between the op-ed texts and the
Twitter user texts.

5.  I estimated the correlation between the op-ed texts and the tweets
    posted by each Cabinet member account

You can find the code I used [on
Github](https://github.com/mkearney/resist_oped). And here is the visual
representation of the correlation coefficients:

<p style="align:center">

<img src="plot.png"/>

</p>

## Limitations

This exercise is useful for illustrating how it’s possible to use data
science to estimate the similarity between multiple texts, but it does
not provide any conclusive evidence to answer the question of who
authored the *New York Times* op-ed. In fact, there are numerous reasons
why one should be skeptical of inferences made from this analysis. I
will describe just a few of those limitations in the next few
paragraphs.

First, the comparison texts are limited because they were designed for
Twitter and not the New York Times. They were also authored by users who
presumably were okay with their identity being connected to their Tweets
(unlike the anonymous author behind the op-ed).

Second, the pool of comparison texts doesn’t even represent all of the
possible options of people who would fit the description of a *senior
official in the Trump administration*. For instance, this omits from
consideration any Cabinet member who doesn’t have or use Twitter. It
also omits anyone who works in the Trump administration but who is not
an official member of the Cabinet.

Third, the text similarity analysis assumes the author of the anonymous
op-ed didn’t try (or failed) to disguise their own communication
patterns. Even if they did try to disguise themselves, it’s certainly
possible that some communication patterns still slipped through the
cracks, but it’s also possible they provided enough false positives
(i.e., “lodestar”) that many algorithms would get it wrong.

Fourth, it also assumes the people who write the tweets are the actual
people who they purport to represent. For example, we have reason to
believe [Trump does **not** operate the @POTUS
account](https://nypost.com/2017/01/16/donald-trump-wont-be-using-the-potus-twitter-account/),
but in most cases we never know for sure. It’s also entirely possible
that some internal communications person influences the messages sent on
behalf of several of those accounts. Or it’s possible that
administrations tend to have overlapping communication patterns because
they strive for monolithic communication and, as a consequence, there
are a handful of near matches in any sample of texts composed by people
working in the White House.


