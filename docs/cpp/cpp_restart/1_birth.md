# 1 C++ 的诞生

C++ 他爹 Bjarne Stroustrup 上学的时候用 Simula 写了个模拟器。他写得十分开心，因为 Simula 提供了 **类 (class)** 的概念；这使得他能把具体问题中的概念直接映射到语言结构中，从而提供非常好的可读性。

!!! note inline end ""
    这里提到的「类」会在下一节具体讨论；「协程」的讨论可能会更晚一些。

他提到，Simula 的类、**协程 (coroutine)** 和广泛深入的类型检查非常有助于编写大规模的程序；这些特性使得代码的可维护性并没有随着代码规模增加而降低。整个程序更像是若干小程序的组合，因而更容易写、理解和排除错误。

不过，Simula 的性能很差。其编译和链接很慢，运行时的表现也因为广泛存在的运行时类型检查、动态内存分配、垃圾回收 (GC) 等等而非常差。这使得 BS 不得不用 BCPL 重新写了一遍他的模拟器；从而给他留下了深刻的心理阴影。他发誓：「在没有合适工具的情况下绝不去冲击一个问题。」

关于什么是「合适的工具」，他主张三个方面：

1. 类似 Simula 的对程序组织的支持。他希望一个好的工具应该有类似「类」的分层结构，从而能够接近具体问题中的概念，并将程序切分为独立的单元；同时希望有良好的类型检查。这样的语言编写出来的程序才能适应迅速增长的规模和复杂性。
2. 编译、链接、运行应当像 BCPL 一样高效。他希望各种优雅的特性相对于朴素的写法不应付出额外的运行时间和空间作为代价。同时也应当方便和其他语言写成的单元链接在一起。
3. 应当保证良好的可移植性。

很快，BS 在 1979 年就遇到了「没有合适工具」的问题，因此他开始按照上述观点开发一个工具。为了上述「可移植性」，他自然不会去开发一个崭新的语言；他选择基于某种已经存在的语言开发一套预处理器，从而将支持了类的语言变体处理成对应语言本身就接受的程序。

选择哪门语言呢？BS 在各种系统程序编程语言中比较喜欢 C，因为它灵活（通用）、高效、各种平台都有 C 编译器、可移植。他后来指出，希望 C++ 一方面能够像 C 一样接近机器，另一方面又能接近需要解决的问题。

!!! note
    我画了张图！

    <center>![](2023-01-31-23-59-28.png){width=500}</center>

    容易理解，随着抽象程度的增加，程序的性能很有可能受到损失。例如 Python 中能保存任意整数的 bignum 的性能一定不会优于 CPU 原生支持的整型。而 C++ 的期望则是，把握这里的「or equal」，即在不损失性能的前提下提供必要的数据抽象。

于是，他设计出了 C with Classes（其中的名字「class」来自 Simula），并设计了一个预处理程序 Cpre（1981/12 首次发布），来将 C with Classes 处理成 C。

BS 到 1982 年的时候认为，C with Classes 是成功的，但是又不太成功：它确实很有用，而且有不少人用，从而也能支持维护成本；但是用的人又不够多，因此不足以支持一个开发组织。这样的情况会使得 BS 本人被困在这里，因此他决定基于在 C with Classes 的经验，开发一种新的、更好的语言。经过一些讨论和发展，这门语言被命名为 C++。

BS  讨论了「用户会是哪些人」「他们使用什么样的系统」「作者如何避免负责提供工具」，从而讨论「这些问题将如何影响语言的定义」。最后一个问题的结论是，C++ 不能带有特别复杂的编译的或运行时的 feature，同时必须能使用原来的链接器，并且产生的代码一开始就要和 C 的一样高效。

1982~83 年，BS 设计了 Cfront。它是一个完整的编译器前端，负责对 C++ 程序进行语法和语义的分析和检查，在 1984/8 首次发布 (Release 1.0)。源代码会先通过预处理器 Cpp 完成预处理，然后交给 Cfront 检查并生成 C 代码。生成 C 代码是为了可移植性的保证。

从此之后，C++ 逐步发展，在 1989 年发布了 Release 2.0；1991 年发布了 Release 3.0。1990 年开始，C++ 也走上了标准化之路；C++98 成为了第一个标准化的发布。此后，C++98, C++03, C++11, C++14, C++17, C++20 逐步迭代，下一代标准 C++23 也会在不久后发布。

!!! info "相关链接"
    - [History of C++ | cppreference](https://en.cppreference.com/w/cpp/language/history)
    - [C++ # History | wikipedia](https://en.wikipedia.org/wiki/C%2B%2B#History)

*[BS]: Bjarne Stroustrup
*[GC]: Garbage Collection