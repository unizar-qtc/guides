# BIFI's HPC Clusters

The BIFI institute has one main HPC clusters (aka *supercomputers*) under the management of [CESAR](http://cesar.unizar.es) (*Centro de Supercomputación de Aragón*). To connect, use [ssh](./ssh.md#Hosts).


## Infrastructure

The main cluster, built in 2023 and named *agustina*, is composed by several types of nodes with different hardware specifications. They are accesible through their corresponding queues. Combined, the CPU nodes can deliver a peak performance of 510 TFLOPS.

|                  |  *thin*  |  *fat*  |  *ada*  |  *hopper*  |
| :--------------: | :------: | :-----: | :-----: | :--------: |
| # nodes          |  93  |  3  |  9  |  3  |
| | | | | |
| CPU arch         |  x86_64  |  x86_64  |  x86_64  |  x86_64  |
| CPU brand        |  AMD  |  AMD |  INTEL  |  INTEL  |
| CPU model        |  EPYC 7513  |  EPYC 7513  |  Xeon Gold 6548Y+  |  Platinum 8462Y+  |
| CPU freq         |  2.6 GHz  | 2.6 GHz  |  2.5 GHz  |  2.8 GHz  |
| # physical cores |  32  |  32  |  32  |  32  |
| # threads        |  32  |  32  |  32  |  32  |
| sockets/node     |  2  |  2  |  2  |  2  |
| cores/node       |  64  |  64  |  64  |  64  |
| | | | | |
| RAM mem/node     |  256 GB  |  512 GB  |  1.5 TB  |  2 TB  |
| | | | | |
| # GPUs/node      |  |  |  4  |  4  |
| GPU brand        |  |  |  NVIDIA  |  NVIDIA  |
| GPU model        |  |  |  L40S  |  H100  |
| GPU vmem         |  |  |  48 GB  |  80 GB  |

|                  |  |
| :--------------: | :--: |
| OS               |  Rocky Linux 8.6  |
| kernel           |  4.18.0-372.9.1  |
| storage          |  ~600 TB (LUSTRE)  |
| memory arch      |  distributed  |


## Job scheduler

To send a calculation job to the computing nodes, it must be submitted through a manager software that will hold the job waiting in the queue until they requested resources are available. The time limit in all the queues is 7 days.

*Agustina* uses [SLURM](https://slurm.schedmd.com/) job scheduler. Here are listed the essentials commands:

|                  |  *SLURM* command  |
| :--------------: | :---------------: |
| submitted jobs status |  squeue  |
| queues status |  sinfo  |
| submit job    |  sbatch \<.job>  |
| cancel job    |  scancel \<.job>  |

Useful ready-to-use scripts to launch calculations for the most common programs can be found in this [launchers](https://github.com/unizar-qtc/launchers) repository.


## Software manager

Although many programs are installed in the clusters, a user can only access the ones currently loaded in the user profile. To manage this, the [Environment Modules](http://modules.sourceforge.net/) software is used. Custom modules can be used if they are located in the path of `$MODULEPATH` variable. Example: `module load gaussian/g16`

|                    |  *module* command  |
| :----------------: | :--------------: |
| list available modules |  module avail  |
| list loaded modules |  module list |
| add module         |  module load \<module> |
| remove module      |  module unload \<module> |
| information        |  module show \<module> |
