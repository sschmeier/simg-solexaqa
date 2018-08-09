Bootstrap: docker
From: continuumio/miniconda3:4.5.4

%labels
   AUTHOR schmeier@tuta.io

%environment
# ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# This sets global environment variables for anything run within the container
  export PATH="/opt/conda/bin:/usr/local/bin:/usr/bin:/bin"
  unset CONDA_DEFAULT_ENV
  export ANACONDA_HOME=/opt/conda
  export LANG=C.UTF-8
  export LC_ALL=C.UTF-8

%post
   export PATH=/opt/conda/bin:$PATH
   echo "We add conda channels."
   conda config --add channels defaults
   conda config --add channels conda-forge
   conda config --add channels bioconda
   echo "We install some utils."
   apt-get update --fix-missing && apt-get install -y apt-utils && apt-get install -y unzip && apt-get clean
   ## SolexaQA++
   echo "Download SolexaQA++ from https://svwh.dl.sourceforge.net/project/solexaqa/src/SolexaQA%2B%2B_v3.1.7.1.zip"
   curl -o solexaqa.zip https://svwh.dl.sourceforge.net/project/solexaqa/src/SolexaQA%2B%2B_v3.1.7.1.zip
   unzip solexaqa.zip 
   mv /Linux_x64/SolexaQA++ /usr/local/bin
   ## R
   echo "We install conda-based tools."
   conda install --yes r-base=3.5.1
   conda clean --index-cache --tarballs --packages --yes