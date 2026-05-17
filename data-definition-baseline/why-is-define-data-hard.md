# Why Is Defining Data Hard?

Every labeler has their own standard of labeling, which causes inconsistency. Best practices for the data stage of a full ML project cycle involve:

- Defining what the data is
- Defining the mapping X -> Y
- Setting up a good baseline

---

## Label Ambiguity Examples

### Speech Recognition

- Filler words (e.g., 语气词) or unclear audio make consistent labeling difficult.

### User ID Merging

- When merging instances from two databases, an ML model determines whether two records refer to the same person.
- Human-level performance (HLP) becomes inconsistent when the underlying data is unclear.

---

## Data Definition Questions

**What is the input X?**
- For image/video/computer vision: lighting, contrast, resolution?
- For structured data: which features should be included?

**What is the target label Y?**
- How can we ensure labelers give consistent labels?

---

## Major Types of Data Problems

Data problems fall along two axes:

|                   | Small data (<= 10,000) | Big data (> 10,000) |
|-------------------|------------------------|----------------------|
| **Unstructured**  | Clean labels critical; can review manually | Data process is key; augmentation helps |
| **Structured**    | Clean labels critical; harder to get more data | Data process is key; harder to augment |

> 10,000 is the rough threshold because above it, it becomes impractical for a team to examine every example.

### Unstructured Data

- May or may not have a large collection of unlabeled examples.
- Humans can label more data.
- Data augmentation (synthesizing new images, audio, or text) is more likely to be helpful.

### Structured Data

- Harder to obtain more data.
- Human labeling may not be possible (with some exceptions).
- Harder to use data augmentation — you cannot easily synthesize new houses or new users that do not exist.

### Small vs. Big Data

- **Small data:** Clean labels are critical. Can manually review the dataset, fix labels, and have all labelers discuss directly.
- **Big data:** Emphasis on data process. Hard to unify labeling across many labelers; use consensus or voting as a last resort.

---

## Small Data and Label Consistency

**Why label consistency matters:**

- Small data with noisy labels produces a poorly fitted function with low confidence.
- Big data with noisy labels can be partially mitigated by averaging.
- Small data with clean, consistent labels allows confident function fitting.

### Big Data Problems Can Have Small Data Challenges Too

Problems with large datasets but a long tail of rare events face small-data challenges in those rare cases. Examples:

- Web search (low-frequency queries)
- Self-driving cars (rare edge-case events)
- Product recommendation systems (rarely seen items)

---

## Improving Label Consistency

**Process:**

1. Have multiple labelers label the same example.
2. When there is disagreement, have an MLE, subject matter expert, and/or labelers discuss and agree on the definition of Y.
   - Document the agreed-upon definition.
3. If labelers believe X does not contain enough information, consider changing X.
4. Iterate until it is difficult to significantly increase agreement further.

**Outcomes of this process:**

- Standardized labels
- Merged classes/categories where appropriate

### Technique: Introduce a Class to Capture Uncertainty

Instead of a binary label (0 or 1), use an intermediate class:

- Detection: `0 | borderline | 1` instead of just `0 | 1`
- Unintelligible audio: label as `[unintelligible]` rather than guessing

### Labeling Strategy by Scale

- **Small data:** Few labelers — ask them to discuss specific labels directly.
- **Big data:** Establish a consistent definition with a small group first, then distribute labeling instructions to the broader labeling team. Using multiple labelers per example with voting is a last resort.

---

## Human-Level Performance (HLP)

### Why Measure HLP?

HLP estimates the Bayes error (irreducible error) to guide error analysis and prioritization.

### Other Uses of HLP

- In academia: establish a respectable benchmark to support publication.
- In business: when a product owner asks for 99% accuracy, HLP helps establish a more realistic target.
- Note: using HLP solely to prove ML is "better than humans" to convince a business owner is not a recommended use.

---

## Raising HLP

When the ground truth label is externally defined, HLP gives an estimate for Bayes error.

However, when ground truth is itself a human label, the more important goal is to unify the labeling standard among labelers:

- HLP significantly below 100% likely indicates ambiguous labeling instructions.
- Improving label consistency raises HLP.
- This makes it harder for ML to beat HLP on paper, but the more consistent labels raise ML performance — which ultimately benefits the application.

### HLP on Structured Data

Structured data problems less frequently involve human labelers, so HLP is less commonly used. Some exceptions where human labeling is still required:

- User ID merging: are these the same person?
- Network traffic: is this computer compromised?
- Transaction data: is this fraud?
- Account behavior: is this a spam or bot account?
- GPS data: is the user on foot, bike, car, or bus?
