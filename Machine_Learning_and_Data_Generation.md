# Machine Learning and Data Generation

### Outline
- What are synthesis problems?
- What does it mean to so;ve synthesis problem?
- How can we solve synthesis problems with ML?


### Part 1: What are synthesis problems?
- Synthesis tasks, generative tasks, or genenrative problems, are problems where the required ouput is defined on the feature space $\Omega$, the same space as the observations $x_i$.
- Solving these problems requires synthesis, a.k.a. data generation. 

```mermaid
graph LR;
A[Practical Utilities] & B[Art and entertainment] & C[Privacy and anonymisation]---|for humans|D[Synthesis use cases];
D[Synthesis use cases]---|for machines|E[Data imputation] & F[dataset augmentation];
```

#### Applications
- Practical utilities
    - prosthetic voices for the physical impaired
    - Text and speech synthesis for conversational AI
    - github copilot (AI assisted source code synthesis)
    - drug discovery
    - images synthesised by a deep neutral network(disco diffusion) based on a user provided text prompt
    - AI Dungeon
    - Privacy - Image anonymisation
    - Dataset augmentation - Synthesised images for training automomous driving systems
    - Data imputation: generate reasonable values while filling a form

#### Generative tasks are not generative models
- Generative tasks: can be solved without using generative(probablistic) models, sometimes even without ML
    - Example: recorded voiceover in games
- Generative model: can be used for other problems beyond data generation 
    - [models of the joint pdf $p_{x,y}(x,y)$]
    - Example: classification using Bayes' law

### Categories of synthesis problems
```mermaid
graph LR;
A[synthesis type]-->|unconditional|B[generate new examples x: e.g. dataset augmentation, entertainment, drug discovery];
A[synthesis type]-->|conditional|C[generate new examples x given the conditioning y: e.g. dataset imputation, text-to-speech, text-to-image, anyinteractive or controllable setting];
```
- conditional models are more general: they reduce to unconditional synthesis when y is empty
- Unconditional synthesis has fewer applications, because we lack control!
    - for example, an unconditional speech synthesiser just produces babble(含糊不清)

```mermaid
graph LR;
A[data space]-->|discrete|B[e.g.,images, text, symbol, graphs];
A[data space]-->|continuous|C[e.g. audio, motion, physical simulation];
```

- Continous dataset can be **quantised**(or **binned**, if you imagine a histogram);
    - This happens naturally when we store a photo digitally
- Discrete data can be **dequantised** or **embedded** in continuous spaces
    - This happens naturally when we play music from a computer

- Nevertheless, it may be better to choose a model that is tailored to the domain!

- The data space may be composed of multiple modalities(i.e. communciation channels) - then the problems is called **mutimodal synthesis**
    - Example: video generation(audio and image frames, possibly text captions), social robots(text, speech,motion), or tabular dataset(they can contain any combination of modalities)

- For practical applications, the data is usually very high-dimensional, because it extends in space(e.g.,images), time(e.g. audio), or both(e.g.,video). A 100*100 pixel RGB image is at least 30000-dimensional.

```mermaid
graph LR;
A[Usage requirements]--->|pre-synthesised|B[e.g. data augmentation, generative art, drug discovery];
A[Usage requirements]--->|real-time|C[e.g.interactive agents, writing assistant];
```

- Also called offline and online synthesis, respectively
- Offline sythesis can leverage big models running on multiple GPUs in parallel(e.g. in a data-centre)
- Online synthesis requires low latency and sequential processing(to react to the input), and it may have to be run on CPUs in monbile devices. 

### Part 2: What does it mean to solve a synthesis problem?
Outline
- synthesis evaluation
- synthesis evaluation
    - objective measures
    - subjective measures

##### Analysis and Synthesis - two sides of the same coin


```mermaid
graph LR;
A[observations]--->|analysis|B[attributes];
```

```mermaid
graph LR;
A[typically high-dimensional]--->|distill information|B[typically low-dimensional];
```
- typically high-dimensional:e.g. pipe.jpg
- typically low-dimensional: e.g,"A painting of a pipe."

```mermaid
graph RL;
B[typically low-dimensional]--->|hallucinate information|A[typically high-dimensional];
```
```mermaid
graph RL;
A[attributes]--->|synthesis|B[observations];
```

#### Analysis and synthesis can be used together
Analysis: find the one correct anser for diverse inputs(many to one)
Synthesis: generate any realistic sample given the fixed condition(one to many)

```mermaid
graph TD;
A[Spoken question]--->|automatic speech recognition|B[Text transcription]--->|conversational AI|C[generated reply]--->|text to speech|D[Spoken reply];
```

#### But synthesis is more difficult to evaluate

- Analysis: find the one correct anser for the diverse inputs(many-to-one)
    - Goal: Generate predictions that are correct, i.e. march the ground truth
- Synthesis: generate synthetic examples that are convincing, i.e. similar to the dataset
    - Goal: Generate synthesis examples that are convincing, i.e. similar to the dataset.

- Evaluation: Estimate the difference between ground truth and predictions, or real datapoints and synthetic examples.
    - Analysis: Aim for exact match in low dimensions
    - Synthesis: Aim for similarity in high dimensions
- Measuring similarity is difficult, especially in high dimensions

#### Similarity is only the tip of the iceberg
```mermaid
graph LR;
A[Realism] & B[Recognisability] & C[User preference]---D[Evaluation Aspects];
D[Evaluation Aspects]---E[Accuracy of control] & F[speed] & G[Downstream performance] & H[Computational load];
```
- Realism: human-likeness
- Recognisability: e.g. voice assistant
- User preference: e.g, collaborative synthesis(HCI)
- Accuracy of control: appropriateness for the context
- Speed: latency in real-time interactions
- Downstream performance: e.g. dataset augmentaion
- Computational load: can the model run on my phone?

#### Objective evaluation
- A mathematical approximation
- Quick and cheap
- but often unreliable or even misleading
- Mainly used during development
- examples:
    - MSE
    - Likelihood
    - FID

#### Subjective evaluation
- Asking people to do the work 
- Time-consuming and expensive
- The "gold standard" of evaluation

##### Objective evaluation via MSE
- Mean squared error in data space between real and synthetic is a common -  but bad!-performance measure
- It promotes excessive averaging
    - Example: The MSE-optimal unconditional image model is just a blur
- It penalise diversity
    - It is optimal to always predict the conditional mean every time
    - The true distribution is not MSE optimal!
- Small squared distance in data space does not imply perceptual similarity
    - Example: Nearest neighbours in image databases.

##### Objective evaluation via log-likelihood
- Widely used for benchmarking explicit deep generative methods
    - Example: Bits per dimension(or per pixel)
- Advantages: 
    - Consistent
    - The same idea works for any data space across in invertible transformation. 
- Limitations:
    - Requires the ability to compute probabilites, or ar least a lower bound(ELBO)
        - Dows not work for co-called implicit models(GANs)
    - Has quesionable priorties
        - Bettwe image dequantisation can increase log-likelihood a lot, despite its effects being invisible by definition

- High likelihood is not necessarily better
    - Takeaway: do not rely on objective metrics alone, if you can avoid it

### Objective evaluation via FID
- Fréchet inception distance(FID)
    - Improvements in FID usually correlate well with improvements in perceived quality
        - very common image benchmark
    - Perhapes the best objective metric we have right now
- First introduced for images, but the idea has been ported to other domains
    - Example: Fréchet audio distance
- Usually not used during model development, only for model assessment
    - Too computational expensive

#### How FID works
1. Start form two sets of obervations, real ${x_i}$ and fake $\hat{x_i}$