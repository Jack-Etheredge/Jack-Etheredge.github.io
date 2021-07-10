---
layout: post
title: Extra things you need to know after a data science bootcamp
subtitle: MLE skills beyond DS bootcamp - educational
image:
---

So, you've taken a data science bootcamp or you've taken a course on machine learning? Great. But where do you go from here?

These are some of the highest ROI things you can study, which is to say they don't take long to understand sufficiently well to be effective with them but understanding and using them will dramatically increase how competent you appear to potential employers.

1. Package structure
2. Logging
3. Unit tests and mocks
4. Object oriented programming
5. Debugging with pdb/ipdb

At one of the banks where I interviewed, I was asked what I knew about object oriented programming and had to stumble my way through a garbage explanation.

OOP interview questions often seem to me to devolve into a vocabulary quiz. What's inheritance? What's polymorphism? What's encapsulation? What's a constructor? What's overriding? What's overloading?

If you're familiar with sci-kit learn, which you likely are after some practical ML exposure, then you're already familiar with object oriented programming, even if you don't realize it. SKLearn models are classes, instances of which must first be instantiated as an object that has methods and attributes, including the .fit and .predict methods. If that terminology doesn't feel familiar to you, then you probably just need to upskill your vocabulary surrounding object oriented programming as a first step.

Per section I've listed the resources in rough order of how important I personally found each resource, but your mileage may vary. There's a lot of redundancy per section.

Package structure:

[https://realpython.com/python-application-layouts/](https://realpython.com/python-application-layouts/)

- related importing modules in packages:

[https://realpython.com/python-modules-packages/](https://realpython.com/python-modules-packages/)

- relative vs absolute imports:

[https://realpython.com/absolute-vs-relative-python-imports/](https://realpython.com/absolute-vs-relative-python-imports/)

- “narrative flow” order of defining functions:

[https://dbader.org/blog/how-to-structure-python-programs](https://dbader.org/blog/how-to-structure-python-programs)

Logging:

[https://realpython.com/python-logging/](https://realpython.com/python-logging/)

[https://stackoverflow.com/questions/15727420/using-logging-in-multiple-modules](https://stackoverflow.com/questions/15727420/using-logging-in-multiple-modules)

[https://docs.python.org/3/howto/logging.html#advanced-logging-tutorial](https://docs.python.org/3/howto/logging.html#advanced-logging-tutorial)

[https://www.machinelearningplus.com/python/python-logging-guide/](https://www.machinelearningplus.com/python/python-logging-guide/)

Unit tests and mocks:

[https://realpython.com/python-testing/](https://realpython.com/python-testing/)

[https://realpython.com/python-mock-library/](https://realpython.com/python-mock-library/)

[https://realpython.com/testing-third-party-apis-with-mocks/](https://realpython.com/testing-third-party-apis-with-mocks/)

Object oriented Python:

[https://realpython.com/python3-object-oriented-programming/](https://realpython.com/python3-object-oriented-programming/)

[https://www.reddit.com/r/learnpython/comments/2j1lx1/when_is_it_necessary_for_a_derived_class_to_call/](https://www.reddit.com/r/learnpython/comments/2j1lx1/when_is_it_necessary_for_a_derived_class_to_call/)

[https://realpython.com/python-super/](https://realpython.com/python-super/)

[https://realpython.com/inheritance-composition-python/](https://realpython.com/inheritance-composition-python/)

There are also good youtube videos on logging and unit testing and using the debugger by Corey Schafer and others.

The Python Tricks book and Effective Python 2nd edition book are both excellent books on Python SWE tips and tricks as well.

Each of these topics is rather important to creating maintainable production code. While each of these topics is actually rather large, particularly object oriented programming, you will derive tremendous benefit from knowing even just the bare basics of each of them.

There are of course much larger topics that require much longer study that are also important to successful interviewing for the various positions within the data jobs ecosystem, such as coding interview prep (mostly data structures and algorithms), and system design (depending on the company and your experience level/the experience level of the position wrt software engineering).

*This post is a work in a progress.*