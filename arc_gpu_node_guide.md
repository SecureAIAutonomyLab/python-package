# Logging into arc and starting an interactive session with a single v100 GPU node
```bash
ssh abc123@arc.utsa.edu
srun -p gpu1v100 -n 1 -t 01:30:00 -c 40 --pty bash
module load anaconda3

# make sure your code goes to /work/abc123 dir (it can also goto /home/abc123 if you want)
# but your data MUST go to /work/abc123
cd /work/abc123

git clone https://github.com/SecureAIAutonomyLab/LLM-Utils.git
cd LLM-Utils # you will now be ready to set up a conda environment
```

# Creating new conda environment, and then installing what you need manually
```bash
conda create -p env python=3.10

conda activate ./env

# install pytorch, go here for other versions (https://pytorch.org/get-started/locally/)
# The following are needed for this example.
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch-nightly -c nvidia
conda install -c huggingface transformers
conda install -c conda-forge datasets

# install any other dependies with conda, if they don't exist, you can use pip install instead
# limit the use of pip install unelss it is necessary. If you have a requirements.txt you can do the following

pip install <other_stuff> # if you have any modules that are not on conda (usually wont happen)
```

# Creating existing conda environment from `environment.yml` file
Use this section if you already have a conda `environment.yml` file that specifys all your dependencies

```bash
conda env create --prefix ./env --file environment.yml

conda activate ./env

```

## Now your environment is set up, and you are ready to run your code