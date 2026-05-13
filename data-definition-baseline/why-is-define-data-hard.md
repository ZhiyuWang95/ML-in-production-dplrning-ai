# Why is define data hard?

- Every labeler has their own standard of labeling.
- Labeling becomes inconsistent.

It would be discussed about the best practices for the data stage of the full cycle of a machine learning project.
- Define what is the data.
- Define X -> Y.
- Set up a good baseline.

# More label ambiguilty examples.

## Speech recognition example
- the 语气词 or unclear words.

## User ID merge example
- Instances from 2 databases, when merge, the ML model would be used to figure whether 2 are the same one.

- HLP would be inconsistent when data are not clear.

# Data definition questions
* What is the input x?
  * Lighting? Contract? Resolution?
  * For image or video or compute vision
  * For structured data, what features need to be included?
* What is the target label y?
  * How can we ensure labelers give consistent labels?

# Major types of data problems

* Unstructured and Structured data
 X
* Small data and Big data
Small <= 10000; Big > 10000;
10000 is set because this number starts to be challenging for individual person to examine every example.

```
For a lot of unstructured data problems, people can help you to label data, and data augmentation, such as synthesizing new images or synthesizing new audio, and there's some emerging techniques for synthesizing new text as well, but data augmentation can help.
```
* In contrast, for structured data problems, it can be harder to obtain more data and also harder to use data augmentation. If only 50 houses have been sold recently in that geography, well, it's hard to synthesize new houses that don't exist, or if you have a million users in your database, again, it's hard to synthesize new users that don't really exist.
* Small dataset, clean labels are critical.
