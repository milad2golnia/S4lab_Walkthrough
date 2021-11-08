*Double-fetch* is one main attacks which can leads to kernel’s information leaking.Double-fetch unlike other bugs is not an error really but **it’s a logical bug** and that’s why it’s hard to resolve it. *Double-fetch* can results in serious security problems, for example we can address to: *Sanity check bypassing*, *Buffer
Overflow* and *confused deputy*.  

---

Before continuing this research, let’s see what is Double-fetch bug really by an example? To find out answer of this question you can watch this [video][v] to understand it completely or refer to background section in main article, I can’t explain it here
because it’s not part of my summary.

Also, we assume you know the **differences between *multi-read* and *Double-fetch bug***, if you don’t know it, we again recommend to watch this [video][v].

***
Some previous works tried to address and then solve this bug but all of them are unsatisfying because they have so many `false-positive` and `false-negative` results which forces users to check each result manually. By noticing that there is more than 1000 *multi-reads* in kernel’s source code make us sure the **previous works are infeasible**. This problem motivated us to conduct this research.

The problem with previous works was that there wasn’t any formal Definition or model for *Double-fetch bug* and it was leading to weak results. So first off, we decided to define a formal and mathematical
model for *double-fetch* and develop our research based on it.
The formal definition which we offer is as below.

**A *multi-read* is a *double-fetch bug* if it has 3 below conditions**:
1. Twice reading from memory with overlap.
2. Second fetch should depends on first fetch.
3. It should be possible to overwrite the overlap section after first fetch and before second fetch (**exploitability condition**).

Base on this definition we designed our mathematical model and developed **DEADLINE service to detect
the *double-fetch bugs* automatically**.

DEADLINE uses **static analysis** to techniques to find the *multi-read* sections regardless of being *double-fetch bug or not*. After finding all *multi-read* sections, we build *execution path* for all of them.

As second step, we follow the execution paths and try using **symbolic checking** to find out if that *multi-read* is a *double-fetch bug* or not. To show the power of DEADLINE, we should mention that **we was able to find 23 new double-fetch bug in Linux kernel and 1 bug in FreeBSD kernel**.

As the last step, we offer 4 general ways to fix *double-fetch bugs*. These 4 solution are obtained by discussion at this article and consulting to kernel maintainers.

[v]: https://www.youtube.com/watch?v=B1JEE84f8G0&ab_channel=IEEESymposiumonSecurityandPrivacy