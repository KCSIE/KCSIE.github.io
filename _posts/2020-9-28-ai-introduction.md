---
title: Brief Introduction to AI
tags: AI ML DL Notes
---
# Basic Concepts

## What's Artificial Intelligence

+ **Intelligence** might be defined as the ability to learn and perform suitable techniques to solve problems and achieve goals, appropriate to the context in an uncertain, ever-varying world. A fully pre-programmed factory robot is flexible, accurate, and consistent but not intelligent.

+ **Artificial Intelligence (AI)**, a term coined by emeritus Stanford Professor John McCarthy in 1955, was defined by him as “the science and engineering of making intelligent machines”. Much research has humans program machines to behave in a clever way, like playing chess, but, today, we emphasize machines that can learn, at least somewhat like human beings do.

## Related Concepts

+ **Autonomous systems** can independently plan and decide sequences of steps to achieve a specified goal without micro-management. A hospital delivery robot must autonomously navigate busy corridors to succeed in its task. In AI, autonomy doesn’t have the sense of being self-governing common in politics or biology.
+ **Machine Learning (ML)** is the part of AI studying how computer agents can improve their perception, knowledge, thinking, or actions based on experience or data. For this, ML draws from computer science, statistics, psychology, neuroscience, economics and control theory.
+ **Deep Learning (DL)** is the use of large multi-layer (artificial) neural networks that compute with continuous (real number) representations, a little like the hierarchically organized neurons in human brains. It is currently the most successful ML approach, usable for all types of ML, with better generalization from small data and better scaling to big data and compute budgets.

![](https://s1.ax1x.com/2020/11/01/BwKPJK.png)

# 基本概念

## 什么是人工智能？

+ **智能**可以定义为学习和执行恰当的技术以解决问题、实现目标的能力，且这些能力能够适用于不确定、不断变化的外部环境。经过完全预编程的工业机器人具有灵活性、准确性和一致性，但并不智能。
+ **人工智能（AI）**由斯坦福大学名誉教授 John McCarthy 在 1955 年提出，他将人工智能定义为「制造智能机器的科学与工程」。许多研究使人类编程的机器能够以聪明的方式执行任务，如下棋。但是如今，AI 领域致力于实现至少可以像人类一样学习的机器。

## 相关概念

+ **自主系统**能够独立地计划和确定操作步骤，以实现指定的目标，而无需进行微观管理。医院中的配送机器人必须在人来人往的走廊中自主导航才能成功完成任务。在人工智能领域中，「自主」并不意味着政治或生物学中常见的 “自治”。
+ **机器学习（ML）**是人工智能的一部分，旨在研究计算机智能体如何根据经验或数据改善其感知、知识、思维或行动。为此，机器学习领域的知识涉及计算机科学、统计学、心理学、神经科学、经济学和控制论。
+ **深度学习**指使用大型多层神经网络计算连续（实数）表示，与人脑中按层级结构组织的神经元略有相似。目前，深度学习是最成功的机器学习方法，可用于所有类型的机器学习，并且可基于少量数据实现更好的泛化性能，能够更好地扩展至大规模数据和算力。

![](https://s1.ax1x.com/2020/11/01/BwKry4.jpg)

# Machine Learning

## What‘s Machine Learning?

+ Machine learning is a field of computer science that gives computers the ability to learn without being explicitly programmed.
+ A machine learning algorithm is an algorithm that is able to learn from data.
+ The development of machine learning algorithms is one of the most important branches of AI.
+ A widely quoted and formal definition is “ **A** computer program is said to learn from experience **E** with respect to some task **T** *and some performance measure* **P**, if its performance on **T**, as measured by **P**, improves with experience **E** ” 

## Different ML methods

+ Supervised learning
+ Unsupervised learning
+ Reinforcement learning

![](https://s1.ax1x.com/2020/11/01/Bw13hq.png)

## How machine learning works?

1. Select and prepare a training data set
2. Choose an algorithm to run on the training data
3. Training the algorithm to create the model
4. Using and improving the model 

# 机器学习

## 什么是机器学习?

+ 机器学习是计算机科学的一个领域，它使计算机具有学习的能力，而不需要明确的编程。
+ 机器学习算法是一种能够从数据中学习的算法。
+ 机器学习算法的开发是人工智能最重要的分支之一。
+ 一个被广泛引用的正式定义是" 一个从经验中学习，对于一些任务进行性能评估的计算机程序，如果它在任务上的性能，表现如性能评估所测量的，它会随着经验的提高而提高" 。

## 不同的机器学习方法

+ 监督学习
+ 无监督学习
+ 增强学习

![](https://s1.ax1x.com/2020/11/01/Bw13hq.png)

## 机器学习如何工作?

1. 选择并准备训练数据集
2. 选择一种算法在训练数据上运行。
3. 训练算法以创建模型
4. 使用和改进模型 

![](https://s1.ax1x.com/2020/11/01/Bwttjx.png)

# Deep Learning

## What’s Deep Learning?

+ Deep learning is a subset of machine learning in which multi-layered neural networks—modeled to work like the human brain—'learn' from large amounts of data. Within each layer of the neural network, deep learning algorithms perform calculations and make predictions repeatedly, progressively 'learning' and gradually improving the accuracy of the outcome over time.
+ Deep learning models require large amounts of data that pass through multiple layers of calculations, applying weights and biases in each successive layer to continually adjust and improve the outcomes.
+ Deep learning models are typically unsupervised or semi-supervised. Reinforcement learning models can also be deep learning models. Certain types of deep learning models—including convolutional neural networks (CNN) and recurrent neural networks (RNN)—are driving progress in areas such as computer vision (CV), natural language processing (NLP), and self-driving cars. 

## How deep learning works

+ Deep learning neural networks (called deep neural networks) are modeled on the way scientists believe the human brain works. They process and reprocess data, gradually refining the analysis and results to accurately recognize, classify, and describe objects within the data.
+ Deep neural networks consist of multiple layers of interconnected nodes, each of which uses a progressively more complex deep learning algorithm to extract and identify features and patterns in the data. They then calculate the likelihood or confidence that the object or information can be classified or identified in one or more ways.
+ The input and output layers of a deep neural network are called visible layers. The input layer is where the deep learning model ingests the data for processing, and the output layer is where the final identification, classification, or description is calculated.
+ In between the input and output layers are hidden layers where the calculations of each previous layer are weighted and refined by progressively more complex algorithms to zero in on the final outcome. This movement of calculations through the network is called forward propagation.
+ Another process called backpropagation identifies errors in calculated predictions, assigns them weights and biases, and pushes them back to previous layers to train or refine the model. Together, forward propagation and backpropagation allow the network to make predictions about the identity or class of the object while learning from inconsistencies in the outcomes. The result is a system that learns as it works and gets more efficient and accurate over time when processing large amounts of data.

![](https://s1.ax1x.com/2020/11/01/Bwt55Q.jpg)

## Relation to ML

![](https://s1.ax1x.com/2020/11/01/BwYx1I.jpg)

# 深度学习

## 什么是深度学习?

+ 深度学习是机器学习的一个子集，是神经网络的升级，其中多层神经网络被建模为像人脑一样工作并从大量数据中"学习"。在神经网络的每一层中，深度学习算法反复进行计算和预测，逐步"学习"，并随着时间的推移逐步提高结果的准确性。
+ 深度学习模型需要大量的数据通过多层计算，在每一层连续应用权重和偏差，不断调整和改进结果。
+ 深度学习模型通常是无监督或半监督的。强化学习模型也可以是深度学习模型。某些类型的深度学习模型--包括卷积神经网络（CNN）和循环神经网络（RNN）正在推动计算机视觉（CV）、自然语言处理（NLP）和自动驾驶等领域的发展。

## 深度学习如何工作？

+ 深度学习神经网络（称为深度神经网络）是以科学家认为的人类大脑工作方式为模型的。它们对数据进行处理和再处理，逐步完善分析和结果，以准确识别、分类和描述数据中的对象。
+ 深度神经网络由多层相互连接的节点组成，每个节点使用逐渐复杂的深度学习算法来提取和识别数据中的特征和模式。然后，它们计算对象或信息可以以一种或多种方式进行分类或识别的可能性或置信度。
+ 深度神经网络的输入层和输出层称为可见层。输入层是深度学习模型摄取数据进行处理的地方，输出层是计算最终识别、分类或描述的地方。
+ 在输入层和输出层之间是隐藏的层，在这里，前一层的每一个计算都会通过逐渐复杂的算法进行加权和细化，使最终结果归零。这种计算结果在网络中的移动称为前向传播。
+ 另一个称为反向传播的过程识别计算预测中的错误，为它们分配权重和偏差，并将它们推回到前几层，以训练或完善模型。前向传播和后向传播共同使网络能够对对象的身份或类别进行预测，同时从结果的不一致中学习。其结果是一个边工作边学习的系统，在处理大量数据时，随着时间的推移，系统会变得更加高效和准确。

![](https://s1.ax1x.com/2020/11/01/Bwt9nf.jpg)

## 和机器学习的关系

![](https://s1.ax1x.com/2020/11/01/BwtCB8.jpg)

# Tribes of AI

![](https://s1.ax1x.com/2020/11/01/BwKnot.jpg)

+ **Symbolists** -  Folks who used symbolic rule-based systems to make inferences. Most of AI has revolved around this approach. The approaches that used Lisp and Prolog are in this group, as well as the SemanticWeb, RDF, and OWL. One of the most ambitious attempts at this is Doug Lenat’s Cyc that he started back in the 80’s, where he has attempted to encode in logic rules all that we understand about this world. The major flaw is the brittleness of this approach, one always seems to find edge cases where one’s rigid knowledge base doesn’t seem to apply. Reality just seems to have this kind of fuzziness and uncertainty that is inescapable. It is like playing an endless game of Whack-a-mole.
+ **Evolutionists** - Folks who apply evolutionary processes like crossover and mutation to arrive at emergent intelligent behavior. This approach is typically known as Genetic Algorithms. We do see GA techniques used in replacement of a gradient descent approach in Deep Learning, so it’s not a approach that lives in isolation. Folks in this tribe also study cellular automata such as Conway’s Game of Life [CON] and Complex Adaptive Systems (CAS).
+ **Bayesians**  -  Folks who use probabilistic rules and their dependencies to make inferences. Probabilistic Graph Models (PGMs) are a generalization of this approach and the primary computational mechanism is the Monte-Carlo method for sampling distributions. The approach has some similarity with the Symbolist approach in that there is a way to arrive at an explanation of the results. One other advantage of this approach is that there is a measure of uncertainty that can be expressed in the results. Edward is one library that mixes this approach with Deep Learning.
+ **Kernel Conservatives** - One of the most successful methods prior to the dominance of Deep Learning was SVM. Yann LeCun calls this glorified template matching. There is what is called a kernel trick that makes an otherwise non-linear separation problem into one that is linear. Practitioners in this field live in delight over the mathematical elegance of their approach. They believe *the Deep Learners are nothing but alchemists conjuring up spells without the* *vaguest of understanding of the consequences.
+ **Tree Huggers** - Folks who use tree-based models such as Random Forests and Gradient Boosted Decision Trees. These are essentially a tree of logic rules that slice up the domain recursively to build a classifier. This approach has actually been pretty effective in many Kaggle competitions. Microsoft has an approach that melds the tree based models with Deep Learning.
+ **Connectionists** - Folks who believe that intelligent behavior arises from simple mechanisms that are highly interconnected. The first manifestation of this were Perceptrons back in 1959. This approach died and resurrected a few times since then. The latest incarnation is Deep Learning.
+ **The Canadian Conspirators** - Hinton, LeCun, Bengio et al. End-to-end deep learning without manual feature engineering.
+ **Swiss Posse** - Basically LSTM and that consciousness has been solved by two cooperating RNNs. This posse will have you lynched if you ever claim that you invented something before they did. GANs, the “coolest thing in the last 20 years” according to LeCun are also claimed to be invented by the posse.
+ **British AlphaGoist** - Conjecture that AI = Deep Learning + Reinforcement Learning, despite LeCun’s claim that it is just the cherry on the cake. DeepMind is one of the major proponents in this area.
+ **Predictive Learners** - I’m using the term Yann LeCun conjured up to describe unsupervised learning. The cake of AI or the dark matter of AI. This is a major unsolved area of AI. I, however, tend to believe that the solution is in “Meta-Learning”.
+ **Compressionists** - Cognition and learning are compression (Actually an idea that is shared by other tribes). The origins of Information theory derives from an argument about compression. This is a universal concept that it is more powerful than the all too often abused tool of aggregate statistics.
+ **Complexity Theorists** - Employ methods coming from physics, energy-based models, complexity theory, chaos theory and statistical mechanics. Swarm AI likely fits into this category. If there’s any group that has a chance at coming up with a good explanation why Deep Learning works, then it is likely this group.
+ **Biological Inspirationalists** - Folks who create models that are closer to what neurons appear in biology. Examples are the Numenta folks and the Spike-and-Integrate folks like IBM’s TrueNorth chip.
+ **Connectomeist -** Folks who believe that the interconnection of the brain (i.e. Connectome) is where intelligence comes from. There’s a project that is trying to replicate a virtual worm and there is some ambitious heavily funded research [HCP] that is trying to map the brain in this way.
+ **Information Integration Theorists** - Argue that consciou-ness emerges from some internal imagination of machines that mirrors the causality of reality. The motivation of this group is that if we are ever to understand consciousness then we have to at least start thinking about it! I, however, can’t see the relationship of learning and consciousness in their approach. It is possible that they aren’t related at all! That’s maybe why we need sleep.
+ **PAC Theorists** - Are folks that don’t really want to discuss Artificial Intelligence, rather prefer just studying intelligence because at least they know it exists! Their whole idea is that adaptive systems perform computation expediently such that they are all probably approximately correct. In short, intelligence does not have the luxury of massive computation.

# AI 流派

![](https://s1.ax1x.com/2020/11/01/BwKnot.jpg)

+ **符号主义者** - 用逻辑符号系统进行推理。主要问题是，人们总能找到一些逻辑规则的例外情况。看起来现实世界的逻辑并不是泾渭分明的，而存在一定程度的灰色地带，因此该方法遇到了瓶颈。
+ **进化算法主义者** - 用基因进化算法进行人工智能运算，引入随机突变，保留最好的部分，并淘汰效果较差的部分。在深度学习算法中，也可以使用基因进化算法来部分取代梯度下降算法去做优化，因此进化算法和深度学习并非水火不容。
+ **贝叶斯流派** - 依靠概率去做推理，使用诸如概率图模型[Probabilistic Graph Models]和蒙特卡洛算法之类的工具。与符号主义者相类似的是，Bayes流做人工智能方法也可以在逻辑上得到解释，而且还能量化不确定性。目前有结合Bayes方法和深度学习算法的库Edward。
+ **Kernel保守主义者** - 深度学习之前，SVM是最火的算法，当时使用Kernel Trick可以把非线性的问题映射到线性平面。Kernel保守主义者对于Kernel方法的优雅性大加赞许，并且认为搞深度学习的无非就是一帮自己也不懂自己搞出来的是什么东西的炼金术士。
+ **抱树者** - 这帮人使用基于树的模型，例如随机森林，决策树等等事实上基于树的模型在Kaggle中的许多问题里很有用。微软有一个模型，融合了树模型和深度学习。
+ **联结主义者** - 一群相信智能行为来源于大规模神经元互联的人。第一波是1959年的Perceptron，之后经过起起伏伏，最近一次复兴就是目前风口浪尖的深度学习。联结主义内部也不是铁板一块，而是分为几个流派。
+ **加拿大派** - Hinton，LeCun，Bengio等等，绝技是不需要手工做feature engineering的端到端学习。
+ **瑞士帮** - LSTM的提出者以及宣称使用两个互相配合的RNN就能解决意识问题的帮派。任何敢宣称自己在他们之前就发明了什么东西的人都会被瑞士帮喷到死。比如，瑞士帮就号称其实是他们发明了GAN。
+ **英国AlphaGo派** - 搞出了AlphaGo的流派，认准了AI就是深度学习加增强学习[ 虽然LeCun说增强学习不过是蛋糕上的樱桃点缀]。DeepMind是英国AlphaGo派里面做得最出色的团队。
+ **预测主义学者** - 搞无监督学习的人，根据LeCun无监督学习是AI蛋糕中最大的部分，相当于宇宙中的暗物质，也是目前尚未解决的领域。
+ **压缩主义者** - 认为认知和学习的本质是信息压缩，和信息论的思想脉络一致。
+ **复杂系统理论家** - 使用从物理学，能量模型，复杂系统理论，混沌理论和统计力学等学科继承来的方法。他们最得意的作品就是Swarm AI。另外他们是最有希望能够给深度学习给出理论解释的人。
+ **仿生主义者** - 喜欢搞仿生学，做模仿真正生物神经元的模型，例如Numenta的那帮人，以及在IBM搞TrueNorth的团队。
+ **功能联结图谱论者** - 认为大脑里的互相联结，即功能联结图谱，是智能的真正来源。这方面的项目包括人造蠕虫和获得大量资助的脑功能映射项目。
+ **信息集成工程师** - 认为机器意识来源于机器内部对真实世界中因果性的映射。这个团体认为我们必须首先认识“意识”的本质，才能做人工智能。
+ **PAC主义者** - 这群人并不想真正讨论人工智能。他们的观点是，只要一个自适应系统能快速执行大几率近似正确的计算[probably approximately correct, PCA]就行。总而言之，智能根本不该基于大规模计算。



**Reference/参考**: 

[1]: https://hai.stanford.edu/sites/default/files/2020-09/AI-Definitions-HAI.pdf
[2]: https://medium.com/intuitionmachine/the-many-tribes-problem-of-artificial-intelligence-ai-1300faba5b60

<img style="display: block; margin: 0 auto;" src="" alt="" />

