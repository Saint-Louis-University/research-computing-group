---
date: "2019-03-25"
title: "SLURM Examples"
type: post
---

### Submission script examples

Here are some quick sample submission scripts. For more detailed information, make sure to have a look at the [Slurm FAQ](http://www.ceci-hpc.be/slurm_faq.html) and to follow our [training sessions](http://www.ceci-hpc.be/training.html). There is also [Script Generation Wizard](http://www.ceci-hpc.be/scriptgen.html) you can use to help you in submission scripts creation.

### Message passing example (MPI)

    #!/bin/bash
    #
    #SBATCH --job-name=test_mpi
    #SBATCH --output=res_mpi.txt
    #
    #SBATCH --ntasks=4
    #SBATCH --time=10:00

    module load openmpi
    mpirun hello.mpi
    
Request four cores on the cluster for 10 minutes, using 100 MB of RAM per core. Assuming my_mpi_program was compiled with MPI support, <span style="background-color:#ffffff;font-family:Comic Sans MS">mpirun</span> will create four instances of it, on the nodes allocated by Slurm. 

You can try the above example by downloading the example [hello world program from Wikipedia](https://en.wikipedia.org/wiki/Message_Passing_Interface#Example_program) (name it for instance <span style="background-color:#ffffff;font-family:Comic Sans MS">wiki_mpi_example.c</span>), and compiling it with 

    module load openmpi
    mpicc wiki_mpi_example.c -o hello.mpi
The <span style="background-color:#ffffff">res_mpi.txt</span> file should contain something like

    0: We have 4 processors
    0: Hello 1! Processor 1 reporting for duty
    
    0: Hello 2! Processor 2 reporting for duty
    
    0: Hello 3! Processor 3 reporting for duty
### Shared memory example (OpenMP)

    #!/bin/bash
    #
    #SBATCH --job-name=test_omp
    #SBATCH --output=res_omp.txt
    #
    #SBATCH --ntasks=1
    #SBATCH --cpus-per-task=4
    #SBATCH --time=10:00
    
    export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
    ./hello.omp
The job it will be run in an allocation where four cores have been reserved on the same compute node. 

You can try it by using the [hello world program from Wikipedia](https://en.wikipedia.org/wiki/OpenMP#C) (name it for instance wiki_omp_example.c) and compiling it with 

    gcc -fopenmp wiki_omp_example.c -o hello.omp
The <span style="background-color:#ffffff">res_omp.txt</span> file should contain something like

    Hello World from thread 0
    Hello World from thread 3
    Hello World from thread 1
    Hello World from thread 2
    There are 4 threads
### Embarrassingly parallel workload example

    #!/bin/bash
    #
    #SBATCH --job-name=test_emb
    #SBATCH --output=res_emb.txt
    #
    #SBATCH --ntasks=4
    #SBATCH --time=10:00

    srun printenv SLURM_PROCID
In that configuration, the <span style="background-color:#ffffff">printenv</span> command will be run four times, and each will have its environment variable  <span style="background-color:#ffffff;font-family:Comic Sans MS">SLURM_PROCID</span> set to a distinct value. 

This setup is useful if the program is based on **random draws** (e.g. Monte-Carlo simulations): the application permitting, you can have four programs drawing 1000 samples and combine their output (with another program) to get the equivalent of drawing 4000 samples. 

Another typical use of this setting is **parameter sweep** where the same computation is carried on by each program except that some high-level parameter has distinct values in each case. Examples include optimisation of an integer-valued parameter through range scanning. In the latter case, each instance of the program simply has to lookup the <span style="background-color:#ffffff">$SLURM_PROCID</span> environment variable and decide, accordingly, what values of the parameter to test. 

The same can be set up to process **several data files** for instance. Each instance of the program just has to decide which file to read based upon the value set in its <span style="background-color:#ffffff">$SLURM_PROCID</span> environment variable.

Upon completion, the above job will create a file <span style="background-color:#ffffff">test_emp</span> with four lines:

    0
    1
    2
    3
### Master/slave program example

    #!/bin/bash
    #
    #SBATCH --job-name=test_ms
    #SBATCH --output=res_ms.txt
    #
    #SBATCH --ntasks=4
    #SBATCH --time=10:00
    #SBATCH --mem-per-cpu=100
    
    srun --multi-prog multi.conf
With file *multi.conf* being, for example, as follows

    0      echo     'I am the Master'
    1-3    bash -c 'printenv SLURM_PROCID'
The above instructs Slurm to create four tasks (or processes), one running <span style="background-color:#ffffff">echo 'I am the Master'</span>, and the other 3 running <span style="background-color:#ffffff">bash -c 'printenv SLURM_PROCID'</span>. This is typically used in a **producer/consumer** setup where one program (the master) create computing tasks for the other program (the slaves) to perform. 

Upon completion of the above job, file <span style="background-color:#ffffff">res_ms.txt</span> will contain

    I am the Master
    1
    2
    3
