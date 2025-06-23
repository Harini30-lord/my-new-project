### Main Problem: Sequential Processing Bottleneck

The main problem is the **poor performance of the CPU when adding very large vectors**. The task involves adding corresponding elements of two vectors to create a third. [cite: 64] When a CPU performs this task, it uses a `for` loop to add one pair of elements at a time, sequentially. 

While this is fast for small vectors, the code tests sizes up to 10,000,000 elements. At this large scale, performing ten million additions one-by-one becomes a significant performance bottleneck, leading to a long execution time (`cpu_time`). 

### Solution: Massive Parallelism on the GPU

The solution presented in the code is to use the **massively parallel processing power of a GPU** to perform all the additions simultaneously. This is effective because the calculation for each element in the vector is completely independent of the others.

The solution is implemented as follows:
* A CUDA kernel, `vectorAddCUDA`, is launched on the GPU. 
* This kernel creates thousands of threads, with each thread responsible for adding a single pair of elements.
* Each thread calculates its own unique index `i`. 
* It then performs the addition for that specific index: `c[i] = a[i] + b[i]`. 

Instead of a single core doing all the work sequentially, thousands of GPU cores perform their individual additions at the same time. This parallel approach dramatically reduces the overall computation time (`gpu_time`) , resulting in a significant "Speedup" over the CPU. 



OUTPUT:

CUDA vs CPU Vector Addition Performance (Command Line Method)
Vector Size: 1000       | Correct: PASS | CPU Time: 0.002 ms    | GPU Time: 0.749 ms    | Speedup: 0.003x
Vector Size: 100000     | Correct: PASS | CPU Time: 0.261 ms    | GPU Time: 0.637 ms    | Speedup: 0.410x
Vector Size: 1000000    | Correct: PASS | CPU Time: 2.208 ms    | GPU Time: 4.078 ms    | Speedup: 0.541x
Vector Size: 10000000   | Correct: PASS | CPU Time: 31.934 ms   | GPU Time: 52.754 ms   | Speedup: 0.605x
Vector Size: 20000000   | Correct: PASS | CPU Time: 56.961 ms   | GPU Time: 74.029 ms   | Speedup: 0.769x
