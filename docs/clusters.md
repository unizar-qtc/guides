# BIFI's HPC Clusters

The BIFI institute has two main HPC clusters (aka *supercomputers*) under the management of [CESAR](http://cesar.unizar.es) (*Centro de Supercomputación de Aragón*). To connect, use [ssh](./ssh.md#Hosts).


## Infrastructure

|                  |  *~~MEMENTO~~*  |  *CIERZO*  |  *AGUSTINA*  |
| :--------------: | :---------: | :--------: | :----------: |
| year             |    ~~2011~~     |    2014    |     2023     |
| | | |
| TFLOPS (Rmax)    |  ~~~20~~  |  ~80  | |
| | | |
| CPU arch         |  ~~x86_64~~  |  x86_64  |  x86_64  |
| brand            |  ~~AMD~~  |  Intel  |  AMD  |
| model            |  ~~Opteron 6272~~  |  Xeon E5-2680v3  |  EPYC 7513  |
| freq             |  ~~2.1 GHz~~  |  2.5 GHz  |  2.6 GHz  |
| SIMD extensions  |  ~~SSE4.2 AVX~~  |  SSE4.2 AVX AVX2  |  SSE4.2 AVX AVX2  |
| # physical cores |  ~~8~~  |  12  |  32  |
| # threads        |  ~~16~~  |  12  |  32  |
| sockets/node     |  ~~4~~  |  2  |  2  |
| cores/node       |  ~~64~~  |  24  |  64  |
| # nodes          |  ~~47~~  |  70  |  96  |
| # cores total    |  ~~3008~~  |  1680  |  6144  |
| | | |
| memory arch      |  ~~shared~~  | distributed  |  distributed  |
| RAM              |  ~~DDR3~~  |  DDR4 ECC REG  | |
| freq             |  ~~667 MHz~~  |  2133 MHz  | |
| mem/node         |  ~~-~~  |  64 GB  |  256 GB  |
| # mem total      |  ~~12 TB~~  |  -  |  -  |
| | | |
| InfiniBand       |  ~~QDR 40Gbps~~  |  FDR  56Gbps  | |
| ethernet         |  ~~10 GbE~~  |  10 GbE  | |
| | | |
| storage          |  ~~56 TB~~  |  288 TB (LUSTRE)  | |
| | | |
| OS               |  ~~Scientific Linux 6.3~~  |  Scientific Linux 6.6  |  Rocky Linux 8.6  |
| kernel           |  ~~2.6.32-431.23.3~~  |  2.6.32-504.8.1  |  4.18.0-372.9.1  |

There are also six special nodes at *cierzo*: \
 4- *gpu* : with 2 GPUs NVIDIA Tesla K40m per node \
 1- *phi* : with 2 co-processors Intel Xeon Phi 5110P \
 1- *fat* : with 2TB of RAM and 4 CPUs Intel Xeon E5-4627v3 @ 2.6GHz

There are also three special nodes at *agustina*: \
 3- *fat* : with 516GB of RAM


## Job scheduler

To send a calculation job to the computing nodes, it must be submitted through a manager software that will hold the job waiting in the queue until they requested resources are available.

Each cluster uses a different job scheduler: [SGE](http://gridscheduler.sourceforge.net/htmlman/manuals.html) in *memento* and [SLURM](https://slurm.schedmd.com/) in *cierzo* and *agustina*. Different commands and parameters are employed. There are tables with their [equivalences](https://srcc.stanford.edu/sge-slurm-conversion), and here are listed the essentials.

|                  |  *~~MEMENTO~~*  |  *CIERZO*/*AGUSTINA*   |
| :--------------: | :---------: | :---------: |
| job scheduler    |  *~~SGE~~*      |  *SLURM*    |
| submitted jobs status |  ~~qstat~~  |  squeue  |
| queue status |  ~~qstat -g c~~  |  sinfo  |
| submit job |  ~~qsub \<.job>~~  |  sbatch \<.job>  |
| cancel job |  ~~qdel \<.job>~~  |  scancel \<.job>  |


### Queues

In *cierzo* there are 5 different queues:

|  *CIERZO* queue  |  time limit  |  #nodes  |
| :--------------: | :----------: | :------: |
|  bifi            |  10 days     |  70      |
|  test            |  15 min      |  6       |
|  gpu             |  7 days      |  4       |
|  phi             |  inf         |  1       |
|  fat             |  inf         |  1       |

In *agustina* there are 2 different queues:

|  *AGUSTINA* queue  |  time limit  |  #nodes  |
| :----------------: | :----------: | :------: |
|  thin              |  inf         |  93      |
|  fat               |  inf         |  3       |



## Software manager

Although many programs are installed in the clusters, a user can only access the ones currently loaded in the user profile (none by default). To manage this, the [Environment Modules](http://modules.sourceforge.net/) software is used. Example: `module load gaussian/g09_D01`

|                    |  *module* command  |
| :----------------: | :--------------: |
| list available modules |  module avail  |
| list loaded modules |  module list |
| add module        |  module load \<module> |
| remove module      |  module unload \<module> |
| information        |  module show \<module> |
