conda info --envs
conda env list

conda activate qlib_py38

conda create -n qtrader python=3.7
conda activate qtrader


conda create -n env_zipline python=3.6
conda activate env_zipline
conda install -c conda-forge zipline
zipline ingest -b quantopian-quandl

conda remove -n env_zipline --all