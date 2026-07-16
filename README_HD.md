1. clone repository
git clone https://github.com/dabralhd/242-neuralfeels.git
cd /root/242-neuralfeels

2. install micromamba
https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html

~~~
curl -Ls https://micro.mamba.pm/api/micromamba/$(uname)-$(uname -m)/latest | tar -xvj bin/micromamba
~~~

- add micromamba to path
~~~
export PATH=/root/242-neuralfeels/bin:$PATH
~~~

then do this once (why?)
~~~
eval "$(micromamba shell hook --shell bash)"
~~~

3. do the correction for pre-commit package in environment.yaml
correction is to replace - by ==

3. create micromamba environment and instantiate it

~~~
micromamba create -n neuralfeels python=3.10 -c conda-forge -y
micromamba activate neuralfeels
./install.sh -e neuralfeels
eval "$(micromamba shell hook --shell bash)"

~~~

5. download dataset
https://huggingface.co/datasets/suddhu/Feelsight/tree/main


~~~
wget -c --tries=0 https://huggingface.co/datasets/suddhu/Feelsight/resolve/main/assets.tar.gz
wget -c --tries=0 https://huggingface.co/datasets/suddhu/Feelsight/resolve/main/feelsight.tar.gz
wget -c --tries=0 https://huggingface.co/datasets/suddhu/Feelsight/resolve/main/feelsight_occlusion.tar.gz
wget -c --tries=0 https://huggingface.co/datasets/suddhu/Feelsight/resolve/main/feelsight_real.tar.gz
~~~

6. git param set

~~~
git config --global user.email dhemdutt@gmail.com
git config --global user.name "Hem Dutt Dabral"
~~~

7. download models

- tactile transformer

~~~
mkdir -p data/tactile_transformer
wget -c --tries=0 https://huggingface.co/suddhu/tactile_transformer/resolve/main/dpt_real.p
wget -c --tries=0 https://huggingface.co/suddhu/tactile_transformer/resolve/main/dpt_sim.p
~~~

- segment anything
~~~
mkdir -p data/segment-anything && cd data/segment-anything
for model in sam_vit_h_4b8939.pth sam_vit_l_0b3195.pth sam_vit_b_01ec64.pth; do
  gdown https://dl.fbaipublicfiles.com/segment_anything/$model
done
cd ../..
~~~