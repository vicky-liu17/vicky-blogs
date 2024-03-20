# The deep learning revolution

- What is driving this rapid progress of AI development (like GPT, sora, etc. )
- Deep Learning at massive scales 深度学习的大规模运用

- Progress also driven by:
    - Similar solutions for different tasks in different domains （相似任务在不同领域的解决方案：许多AI任务在不同的领域都存在相似的解决方案。一旦在一个领域中取得了进展，这些解决方案就可以迁移到其他领域，并进行相应的调整和优化。这种跨领域的知识共享和技术转移加速了AI技术的发展速度。）
    - General formula for improving results:（在深度学习中，一般的方法是通过增加神经网络的规模、提供更多的训练数据以及增加计算资源来改进结果）
        - bigger networks
        - more training data
        - more compute

![](Pictures/0101.png)

- Which methods are producing these results?
- At the start Neural Networks trained with lots of （labelled） data
- （Luckily many of the training mechanisms for “unlabelled” data are similar totraining in the labelled regime. Self-supervised learning covered later on in course.）


## Most successful example of self-supervision

- Self-supervised learning for Large Language Models: GPT-3, BERT variations, etc...
- How:
    - **Unlabelled data** :  Collect many valid sentences.
        - The man went to the shop to buy a pint of milk.
        - The rain in Spain falls mainly in the plain.
    - **Task** : 
        - Mask out input words in each sentence
            - The man went to the [MASK] to buy a pint of [MASK].
        - and train network to predict masked words:
            - The man went to the [shop] to buy a pint of [milk].

## What is a neural network?

![](Pictures/0102.png)

- Represents non-linear function from input to output space.

- Neural network functions have a deceptively simple form:

![](Pictures/0103.png)