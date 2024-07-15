# Amber_MPIch_container

Definition file to build Amber (and AmberTools) using a base Ubuntu image with MPIch supporting UCX and Cuda 

# Build

With `Amber24.tar.bz2` and `AmberTools24.tar.bz2` in the same folder as `ubuntu2204_mpich421_ucx17_cuda_121_amber24.def` run:

 apptainer build image.sif ubuntu2204_mpich421_ucx17_cuda_121_amber24.def

 # Usage (input data in `./data`, outputs in  `./data/outputs`)
 ## on GPU 

```
apptainer exec --nv --bind ./data:/opt/uio/data image.sif /usr/local/amber24/bin/pmemd.cuda -O -i /opt/uio/data/03_Prod.in -c /opt/uio/data/02_Heat.ncrst -p /opt/uio/data/parm7 -o /opt/uio/data/outputs/03_Prod.out -r /opt/uio/data/outputs/03_Prod.ncrst -x /opt/uio/data/outputs/03_Prod.nc -inf /opt/uio/data/outputs/03_Prod.info -AllowSmallBox
```

 ## on CPUs

```
srun -n $SLURM_NTASKS --mpi=pmi2 apptainer exec --bind ./data:/opt/uio/data image.sif /usr/local/amber24/bin/pmemd.cuda -O -i /opt/uio/data/03_Prod.in -c /opt/uio/data/02_Heat.ncrst -p /opt/uio/data/parm7 -o /opt/uio/data/outputs/03_Prod.out -r /opt/uio/data/outputs/03_Prod.ncrst -x /opt/uio/data/outputs/03_Prod.nc -inf /opt/uio/data/outputs/03_Prod.info
```

 
