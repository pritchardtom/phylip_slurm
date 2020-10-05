# Phylip and SLURM

Getting Phylip and SLURM to work together on SCW systems.

## Setting the `PATH` variable

- In your `foofile.txt` file you type the full path to `dnadist`.

- There is nothing wrong with this but if you wanted to use other executables from Phylip's `exe` folder, you would have to constantly write out the full path, so I added the location of Phylip's `exe` folder to my `PATH` environment variable.

- Doing this, enables me to just write `dnadist` instead of `/home/user/phylip/phylip-3.697/exe/dnadist`.


## My SLURM Script

```
#!/bin/bash --login

#SBATCH -p compute
#SBATCH --exclusive
#SBATCH --account=scw1567
#SBATCH --job-name=mafft1
#SBATCH --output=mafft1.out.%J
#SBATCH --error=mafft1.err.%J
#SBATCH --time=01:00:00
#SBATCH --ntasks=1
#SBATCH --nodes=1
#SBATCH --cpus-per-task=40
#SBATCH --threads-per-core=1
#SBATCH --mail-user=s.710994@swansea.ac.uk
#SBATCH --mail-type=END,FAIL

export PATH=/home/s.710994/phylip/phylip-3.697/exe:${PATH}

dnadist < input > output &
wait
```

##

- Firstly, I removed the need of the `foofile.txt` and put the contents of this into my SLURM script.
- I also

- Originally you sent me three files, which is fine, but I personally removed the `foofile.txt` and put the contents of those into my SLURM submission script, just to make it simpler.

- You were also
