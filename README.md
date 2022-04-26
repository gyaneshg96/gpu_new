## Set dueling in GPU Caches

We explore set dueling GPU Caches in GPGPU-Sim v3.3. We are using docker containers
to run the above code, as the above runs on Cuda 4.

Simply use the Dockerfile to build the image like so

``

The container will then have all the necessary
files to run the code, including the benchmarks. After running the container like so

``

And then follow the usual steps in GPGPU-Sim to make and build. For
everyones convenience, the commands are below

``cd gpgpu-sim_distribution; 
make clean;
source setup_environment;
make``

If the make proceeds normally, we need to copy the configs 
of the gpu we need to run on.

``cp configs/GTX480/* ~/test/.``

Now run any test case, 
``cd ~/test/
~/ispass2009-benchmarks/bin/release/NN 28``

For more info visit here
[GPGPU-Sim](https://github.com/gpgpu-sim/gpgpu-sim_distribution)
[ISPAAS2009-Benchmarks](https://github.com/gpgpu-sim/ispass2009-benchmarks)


The default policy is LRU cache. To change the L2-cache algorithm,
find the line containing "-gpgpu_cache:dl2" in the gpgpusim.config file.
This should be line 59 in the GTX480

The letter just after first comma is the cache policy letter. L stands for LRU
policy. 

64:128:8,**L**:B:M:W:L,A:32:4,4:0,32

Change this L letter for different policies

Keys for other policies are:

| Policy     | Code |
| ----------- | ----------- |
| FIFO      | F       |
| LFU   | X        |
| MRU   | M |
| SRRIP | S |
| BRRIP | B |
| DRRIP | D |
