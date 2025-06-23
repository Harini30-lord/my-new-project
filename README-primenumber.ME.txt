### Main Problem: Poor Performance at Scale

the CPU is the single librarian. The GPU, by launching thousands of threads that each check a different number simultaneously, is the team of librarians. This is why the GPU can handle the large-scale task so much more effectively, resulting in a significant "Speedup".


1.The main problem is the significant amount of time it takes for a traditional CPU to find all prime numbers up to a large limit, such as one million[cite: 90]. The code implements a trial-division method where each number is checked for primality one by one[cite: 100]. When the CPU does this, it must perform the test for each number sequentially, which is a computationally intensive and slow process for large ranges.

### Solution: Massive Parallelism on the GPU

The solution presented in the code is to use the parallel processing architecture of a GPU to drastically speed up the computation. This works because the primality test for any given number is completely independent of the test for any other number.

The solution is implemented as follows:
* A CUDA kernel, `findPrimesCUDA`, is launched on the GPU.
* The work is divided among a large number of GPU threads, with each thread being responsible for testing a single, unique number (`idx`) for primality.
* Instead of checking numbers one by one like the CPU, thousands of GPU threads check thousands of different numbers simultaneously[cite: 105].
* Each thread performs the trial division test on its assigned number and stores the result (true or false) in a shared array on the GPU.

By parallelizing the work in this manner, the GPU can find all the prime numbers in a fraction of the time it takes the CPU, resulting in a significant performance "Speedup".


OUTPUT:

Finding primes up to 10000000...

Sequential    : 664579 primes in 7580 ms
Multithreaded : 664579 primes in 1073 ms
CUDA          : 664579 primes in 959 ms

Speedups vs Sequential:
Multithreaded: 7.06431x
CUDA         : 7.90407x
