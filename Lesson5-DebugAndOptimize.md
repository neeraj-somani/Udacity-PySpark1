### Lesson 5 - Debugging and Optimization

- We can't run print statement on spark code thats why spark gives another way to debug code, that is accumlators.
- The reason, print statement doesn't work on spark, because print statement can be run on each worker node and we can see print output from each worker node directly.
- So, we use accumlators to do so.
- 
What are Accumulators?
As the name hints, accumulators are variables that accumulate. Because Spark runs in distributed mode, the workers are running in parallel, but asynchronously. For example, worker 1 will not be able to know how far worker 2 and worker 3 are done with their tasks. With the same analogy, the variables that are local to workers are not going to be shared to another worker unless you accumulate them. Accumulators are used for mostly sum operations, like in Hadoop MapReduce, but you can implement it to do otherwise.

For additional deep-dive, here is the Spark documentation on accumulators if you want to learn more about these.
