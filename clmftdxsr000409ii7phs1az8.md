---
title: "Maven Dependency Resolution: The BF and Skipper Algorithm"
seoTitle: "Maven: BF and Skipper Algorithm for Faster Dependency Resolution"
seoDescription: "Discover how the BF and Skipper algorithm accelerates Maven's dependency resolution process for faster builds"
datePublished: Tue Sep 12 2023 04:30:09 GMT+0000 (Coordinated Universal Time)
cuid: clmftdxsr000409ii7phs1az8
slug: maven-dependency-resolution-the-bf-and-skipper-algorithm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694253393630/e5bc144a-c707-459a-ba46-db2b77ea3366.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1694253993651/c7b7f58a-0f05-401a-a26c-3e50190ee376.png
tags: optimization, algorithms, java, maven, breadth-fist-search

---

Note: This article is a continuation of our Maven series. If you haven't explored the previous articles, [you can find them here.](https://blog.anilgulati.tech/maven-made-simple-your-guide-to-effortless-project-management)

![](https://cdn-images-1.medium.com/max/1000/1*HWJb_IVd38D5eSP2lQo0wQ.jpeg align="left")

### Introduction

Maven, a fundamental tool in Java project management, plays a pivotal role in handling dependencies and creating the intricate web of libraries that modern software projects rely on. In our quest for faster software development, we encountered a challenge — Maven’s dependency resolution process was far from optimized. Complex projects suffered from excruciatingly long build times, primarily due to the time-consuming nature of resolving intricate dependencies.

![](https://cdn-images-1.medium.com/max/1000/1*s3RNNsYC6aaTAHJBV7I-Fw.png align="left")

To address this challenge, eBay developed an innovative Maven extension called Zeus, designed to collect and visualize Maven build data. However, eBay’s exploration revealed that Maven’s built-in dependency resolver had performance bottlenecks when dealing with intricate dependency graphs. In some cases, it took over 30 minutes and 20GB of memory just to print the dependency tree. This was unacceptable, prompting them to dig deeper into Maven’s dependency resolution.

### Understanding Maven Dependency Resolution

Maven, by default, uses a Depth-First Search (DFS) algorithm to traverse the dependency tree and resolve dependencies. It propagates all child dependencies recursively, creating a hierarchical structure. While this approach works well, it can lead to severe slowness and memory consumption when dealing with large and complex dependency graphs.

### The Challenge: Slowness and Memory Overhead

As the software ecosystem grew in complexity, so did project’s Transitive dependencies multiplied exponentially, resulting in an intricate and conflict-ridden dependency graph. This complexity translated into severe slowness during dependency resolution and excessive memory usage.

#### The culprits behind these issues included:

1. Heavy Dependencies: Some low-level libraries depended on heavyweight dependencies, introducing hundreds of transitive dependencies.
    
2. Outdated Libraries: Certain libraries relied on outdated technology stacks with transitive dependencies no longer managed by the parent POM.
    
3. Circular Dependencies: Circular dependencies, although typically skipped, could still lead to performance bottlenecks.
    

To address these challenges, we needed an optimized approach.

### The BF (Breadth-First Traversal) and Skipper Algorithm

To tackle the slowness in dependency resolution, eBay introduced the BF and Skipper algorithm. Its primary goal was to reduce unnecessary calculations and enhance performance. Here’s how it works:

#### 1\. Transition from Depth-First to Breadth-First Traversal

Maven’s default DFS strategy follows a depth-first sequence. In contrast, the BF algorithm traverses nodes from top to bottom and from left to right, mimicking the order in which Maven mediates conflicts. This alteration allows us to predict and skip unnecessary calculations.

#### 2\. Predicting Conflicts: BF Approach

In the BF algorithm, nodes with the same Group ID and Artifact ID (GA) are resolved in the order they appear. The first resolved node becomes the winner, while subsequent nodes with the same GA are conflict losers and can be skipped.

#### 3\. Skipper: Avoiding Unnecessary Resolution

The Skipper component tracks resolved nodes and employs principles to determine if a node can be safely skipped:

* If a node with the same Group ID, Artifact ID, and Version (GAV) has already been resolved, the current node is considered a duplicate and may be skipped.
    
* If a node with the same GA has already been resolved, and the version of the current node differs, it’s a version conflict that can be safely ignored.
    

This optimization dramatically reduces the number of nodes that require resolution, leading to faster and more efficient dependency resolution.

### Force Resolution for Edge Cases

In some scenarios, it employs force resolution to ensure compatibility. For example, if a node is on the left side of a previously force-resolved node, it needs to be force-resolved as well to maintain consistent conflict mediation.

### Achieving Performance and Compatibility

The BF and Skipper algorithm was rigorously tested on thousands of Java applications, demonstrating its effectiveness. It was initially deployed as part of eBay’s project, significantly improving dependency resolution speed.

Recognizing its potential value for the broader Maven community, eBay decided to contribute this algorithm back to the Apache Maven project. Working closely with the community, fine-tuned the code, improved test cases, and successfully incorporated the changes into maven-resolver (v1.8.0).

As a result, Maven 3.9.0, released in February 2023, now includes BF and the Skipper algorithm as part of its core features. This contribution not only enhances dependency resolution speed but also aligns with the open-source spirit of collaborative development.

### Conclusion

The BF and Skipper algorithm, born out of the need for faster and more efficient dependency resolution, has now become a valuable addition to the Maven ecosystem. It empowers developers to build Java applications with unprecedented speed and reliability.

By identifying and addressing the performance bottlenecks within Maven’s dependency resolution process, eBay unlocked new possibilities for software development. This open-source contribution not only benefits our organization but also the wider software development community, showcasing the power of collaborative innovation in the world of Maven.  
  
Enjoyed This Article?

> ***If you enjoy reading this post, got help, knowledge through it, and want to support my efforts please like this article and follow.  
> To explore more of my work, visit my portfolio at*** [***anilgulati.tech***](https://anilgulati.tech?utmSource=hashnode&article=/maven-dependency-resolution-the-bf-and-skipper-algorithm)***.***