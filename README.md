# Phylip and SLURM

Getting Phylip and SLURM to work together on SCW systems.

## My SLURM Script

- I've adapted this script for you, but it's the same as the one I used to successfully calculate the test file: `r5b1.phy`

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

- I've included the `input` file in the same directory as my SLURM script, so I don't need to type the full path to it, which you did in your `foofile.txt` file.  

- Again, there's nothing wrong with the way you did it, or editing the script above to alter `dnadist < input > ouput &` to something like: `dnadist < /scratch/example/phylip/input > /scratch/example/phylip/output` or something like that.

- For clarity, here's the contents of `input` that I used to test Phylip and SLURM together:

```
r5b1.phy
F
r5b1.dist
I
Y
```

- Again, I didn't need to write the full path to the files `r5b1.phy` and `r5b1.dist` because they were being read from, and written to, the same directory as my SLURM script.  You might want to do this (type full paths) as you're reading/writing files from/to `scratch` - this is fine to do.

#### The `wait` Command

- This is used to ensure the background job `dnadist < input > ouput` has time to read the contents of `input` before it proceeds/cancels.

- Without this, the job always failed.  With it, my script now produces the output file `r5b1.dist`.
