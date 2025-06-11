---
title: The Bitter Lesson
layout: single
---

In this post, I’d like to share a short and simple perspective on learning. I tried to keep Rich Sutton’s original message as close as possible, with only small changes. This post is organized into three parts:

1. The main lesson from 70 years of AI  
2. Real-world examples  
3. What this means for how we think about AI  

---

#### 1. The main lesson from 70 years of AI

The biggest lesson from decades of AI research is that general methods using computation are the most powerful—and by a large margin. This is because of Moore’s Law, which says the cost of computing keeps going down over time.

Most AI researchers have acted like computing power is fixed. That’s why they often rely on human knowledge to improve performance. But over time, computing power grows quickly. In the long run, the best improvements come from using that extra computing.

Trying to use human knowledge and trying to use raw computing aren't always in conflict, but in practice, focusing on one means less effort on the other. People also get attached to the approach they’re invested in. But methods built on human knowledge tend to become too complex and harder to scale. Many researchers have learned this lesson too late—the hard way.

---

#### 2. Real-world examples

Rich Sutton gives four examples to back up his point.

##### 2.1. Chess

In 1997, Deep Blue beat world champion Kasparov using deep, brute-force search. Many researchers were upset. They had been working on systems that used human strategies and insights. But those systems lost. Even though brute-force search didn’t play like a human, it worked better. This showed that raw computing power can beat human-designed strategies.

##### 2.2. Go

The same story happened in the game of Go, just 20 years later. Early Go systems tried to use human knowledge to reduce the need for search. But once powerful search and learning methods (like self-play) were used at scale, they won. Learning and search allow systems to make the most of computing power. That’s why Go systems only started winning once they moved away from human knowledge and fully embraced learning.

##### 2.3. Speech recognition

Back in the 1970s, speech systems based on human knowledge (like how the mouth shapes sounds) were tested against new, statistical models like hidden Markov models (HMMs). The statistical methods, which used more computing, performed better. This led to a long-term shift: natural language processing moved away from expert knowledge toward data and computation.

Today, deep learning in speech recognition follows the same trend. It uses less human knowledge, more data, and a lot of computing to achieve far better results.

##### 2.4. Computer vision

Computer vision used to be about detecting edges, shapes, and handcrafted features like SIFT. Today, all of that has been replaced. Deep learning systems now rely only on learned features like convolution and invariance—and they perform better.

---

#### 3. What this means for how we think about AI

This is a big lesson. But many researchers haven’t fully learned it. We still try to build knowledge into systems, even though history shows it doesn't work well long term.

The "bitter lesson" is this: trying to build systems based on how we think we think might help a little at first, but it eventually holds us back. Real breakthroughs come from a different direction—using search and learning to scale with more computing.

This can feel disappointing, especially if you’ve spent years building systems with human insight. But the lesson is clear: **search and learning win in the long run**.

There’s another big idea here. The contents of our minds—the way we think about the world—are too complex and messy to build in. Instead of trying to hard-code concepts like space, objects, or rules, we should build systems that can find those things on their own.

The goal is not to build systems that contain what we know, but to build systems that can discover new things—maybe even things we can’t understand yet.

---

**Reference**

Sutton, R. (2019). [*The Bitter Lesson*](https://github.com/isopink/isopink.github.io/blob/master/_posts/pdf/bitter%20lesson.pdf).
