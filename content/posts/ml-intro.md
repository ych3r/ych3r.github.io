+++
title = 'Machine Learning Introduction'
date = 2025-11-28T17:00:29-05:00
draft = false
toc = false
categories = ['machine learning']
tags = ['']
series = ['']
+++

> I completed Andrew Ng's Machine Learning Specialization course.
> And somehow, I'm still confused...

- Course 1: I've learned supervised machine learning, including regression and classification. 
- Course 2: I've learned some advanced learning algorithms, like neural network and decision trees.
- Course 3: I've learned unsupervised machine learning, recommender systems, and reinforcement learning.

But hey, I understood each concept (at some level), but my understanding is not holistic. I still have no idea how to use machine learning as a tool.

So, let's try to connect all ML concepts.

> First of all, what does machine learning do?

We humans always want to use formulas to explain the patterns of the world. However, not everyone is Ramanujan, figuring out the right formula is hard. So, computer scientists started to think, if we have enough data, why not let the computer brute force the correct function? Turns out it works.

Machine learning tries to find the right function by learning the data.

Some ML models can predict house price, some can detect spam emails, some can recommend movies, etc.

> So, what model can we use?

We have **classical** ML models, like:
- Linear regression
- Logistic regression
- Decision Tree
- Random Tree
- XGBoost

All these models require some feature engineering, i.e., we need to figure out what features matter. To predict house price, we need to know house type, size, year built, etc.

If the problem is too complicated, we can't easily find features, then we let model to find more features. That's **Neural Networks**, it includes:
- MLP (Basic neural network)

And **Deep Learning** is just neural networks with many layers (deeper).
- CNN
- RNN
- Transformer

```
Machine Learning Models
├── Classical ML Models
│
└── Neural Network Models
    ├── Shallow Neural Networks
    └── Deep Learning Models (Deep Neural Networks)
```

> Next, how to train the models?

There are roughly three learning types:
- Supervised Learning: we know the right answer, so we clearly know how well the model does.
- Unsupervised Learning: we don't know the answer, but we hope the model can find some patterns.
- Reinforcement Learning: we give rewards if the model does well.

```
                       LEARNING TYPE
                ┌─────────────┬─────────────┬──────────────────┐
MODEL TYPE      │ Supervised  │ Unsupervised│ Reinforcement    │
────────────────┼─────────────┼─────────────┼──────────────────┤
Classical ML    │ ✔ (most)    │ ✔ (some)    │ ✖ (rare)         │
                │ regression  │ k-means/PCA │                  │
                │ trees       │             │                  │
────────────────┼─────────────┼─────────────┼──────────────────┤
Neural Network  │ ✔ (common)  │ ✔ (autoenc) │ ✔ (deep RL)      │
                │ MLP/CNN/RNN │ autoencoder │ DQN, PPO         │
────────────────┼─────────────┼─────────────┼──────────────────┤
Deep Learning   │ ✔ (very common)          
                │ CNN, Transf │ ✔ (GAN,VAE) │ ✔ (DQN,PPO)      │
                └─────────────┴─────────────┴──────────────────┘
```

> Wait, I'm more confused. What model should I choose to train?

That depends on the problem, every model solves a particular type of pattern in data.

`Pattern complexity: Classical < Neural networks < Deep learning`

```
                          START
                            |
                            v
                  Identify DATA Type
                            |
    ┌───────────────────────┼────────────────────────┬────────────────────┐
    v                       v                        v                    v
TABULAR                  IMAGES                  TEXT/NLP            TIME SERIES
(spreadsheets)           (pixels)                (language)          (sequences)
    |                       |                        |                    |
    v                       v                        v                    v
Small dataset?          Use CNN                Use Transformer        Use LSTM /
    |                                          (BERT/GPT/T5)          Transformer
Yes | No                                                                  |
 v     v                                                              Predict?
Use   Use NNs/Deep ML                                               (Next value?)
Classical ML                                                              |
(XGBoost)                                                                 v
                                                                   LSTM/Transformer
```

This chart can help you solve 90% of ML problems.

> Now, let's think about how to solve real world problem or win a Kaggle competition.

1. Define the problem
   - Supervised
   - Unsupervised
   - Reinforcement
2. Pick a baseline model
   - tabular -> XGBoost
   - images -> CNN
   - text -> Transformer
3. Feature engineering 
4. Train, fine tuning, evaluate
5. Deploy (for real world project)

By writing this blog, I realized that machine learning isn't about memorizing all the model, but about understanding the problem and finding the right tool.

Actually, Machine learning is quite similar to Data Structure and Algorithm. You can use whatever method you want to solve the problem, but there must be a more suitable algorithm for that particular problem.

Thanks for reading!

---

* all the flowcharts are generated by a famous Transformer AI model