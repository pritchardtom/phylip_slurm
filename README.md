# Phylip and SLURM

Getting Phylip and SLURM to work together on SCW systems.

## My SLURM Script

- I've adapted this script for you, but is the same as the one I used to successfully calculate the test file: `r5b1.phy`

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
#SBATCH --mail-user=710994@swansea.ac.uk
#SBATCH --mail-type=END,FAIL

export PATH=/home/s.710994/phylip/phylip-3.697/exe:${PATH}

dnadist < input > output &
wait
```

### Discussion of SLURM Script

#### Removal of `foofile.txt`

- You will notice that I've included the contents of `foofile.txt` inside the script itself, so we no longer need that file.

#### Setting the `PATH` variable

- The `export PATH=/home/s.710994/phylip/phylip-3.697/exe:${PATH}` line in the above script means you no longer have to type out the full path to the location of `dnadist` and can, instead, just type `dnadist` or any other of Phylip's `exe` files without typing `/home/s.710994/phylip...` and so on.

- There's nothing wrong with the way you did it, I'm just lazy.

#### The `input` File
