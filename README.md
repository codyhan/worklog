# worklog

## 2016-11-15

#### Read Torch tutorial

   (https://github.com/soumith/cvpr2015/blob/master/Deep%20Learning%20with%20Torch.ipynb)

   (https://github.com/soumith/cvpr2015/blob/master/Char-RNN.ipynb)

#### Read train.lua

#### Learn Lua in 15 minutes

   (http://tylerneylon.com/a/learn-lua/)
```lua
num = 42  -- All numbers are doubles.

t = nil -- Undefines t; Lua has garbage collection.

while num ## 50 do
  num = num + 1  -- No ++ or += type operators.
end

if num ## 40 then
  print('over 40')
elseif s ~= 'walternate' then  -- ~= is not equals.
  -- Equality check is == like Python; ok for strs.
  io.write('not over 40\n')  -- Defaults to stdout.
else

-- How to make a variable local:
  local line = io.read()  -- Reads next stdin line.
```

#### Install Cuda on the new Server:

   problem: fail to log into gui. /dev/nvidia####  has nothing.

   solved by not install opengl

---

## 2016-11-16
#### Continue read torch tutorial

(https://github.com/soumith/cvpr2015/blob/master/NNGraph%20Tutorial.ipynb)
```lua
function get_rnn(input_size, rnn_size)
  
    -- there are n+1 inputs (hiddens on each layer and x)
    local input = nn.Identity()()
    local prev_h = nn.Identity()()

    -- RNN tick
    local i2h = nn.Linear(input_size, rnn_size)(input)
    local h2h = nn.Linear(rnn_size, rnn_size)(prev_h)
    local added_h = nn.CAddTable()({i2h, h2h}) --performs an element-wise addition
    local next_h = nn.Tanh()(added_h)
    nngraph.annotateNodes()
    return nn.gModule({input, prev_h}, {next_h})
end
```

   (https://www.cs.ox.ac.uk/people/nando.defreitas/machinelearning/practicals/practical5.pdf)

   (https://www.cs.ox.ac.uk/people/nando.defreitas/machinelearning/practicals/practical6.pdf)

   (https://github.com/oxford-cs-ml-2015/practical6)

```lua
--the model can be found at https://en.wikipedia.org/wiki/Long_short-term_memory
function LSTM.lstm(opt)
    local x = nn.Identity()()
    local prev_c = nn.Identity()()
    local prev_h = nn.Identity()()

    function new_input_sum()
        -- transforms input
        local i2h            = nn.Linear(opt.rnn_size, opt.rnn_size)(x)
        -- transforms previous timestep's output
        local h2h            = nn.Linear(opt.rnn_size, opt.rnn_size)(prev_h)
        return nn.CAddTable()({i2h, h2h})
    end

    local in_gate          = nn.Sigmoid()(new_input_sum())
    local forget_gate      = nn.Sigmoid()(new_input_sum())
    local out_gate         = nn.Sigmoid()(new_input_sum())
    local in_transform     = nn.Tanh()(new_input_sum())

    local next_c           = nn.CAddTable()({
        nn.CMulTable()({forget_gate, prev_c}),
        nn.CMulTable()({in_gate,     in_transform})
    })
    local next_h           = nn.CMulTable()({out_gate, nn.Tanh()(next_c)})

    return nn.gModule({x, prev_c, prev_h}, {next_c, next_h})
end
return LSTM
```

#### Prepare data for news generator task

1.description:this task uses news text to produce train data. The source sentences are cleaned sentences from news documents and the target sentences are the next sentence after the source sentence.

2.delete sentences of length <5 or >25

#### Install python hdf5
```
sudo pip install cython
sudo apt-get install libhdf5-dev
sudo pip install h5py
```
---

## 2016-11-17

#### Install torch on Telsa server

follow instructions on torch.ch

#### Learn torch

(https://github.com/torch/nn/blob/master/doc/table.md)

(https://github.com/torch/torch7/blob/master/doc/tensor.md)

(https://github.com/torch/torch7/blob/master/doc/maths.md)

---
##2016-11-18

(https://github.com/torch/torch7/wiki/Cheatsheet)

(http://hunch.net/~nyoml/torch7.pdf)

---

## 2016-11-21

#### write lab report

#### conduct experiments to tune parameters.
---

## 2016-11-22

(http://www.wildml.com/2016/01/attention-and-memory-in-deep-learning-and-nlp/)

#### installed my new desktop however failed 

   after diable nouveau driver and reboot the system, cannot enter into text mode.

---

## 2016-11-23
#### Neural Turing Machines:https://arxiv.org/pdf/1410.5401v2.pdf

#### 多层lstm前向传播顺序:先纵后横

#### understand ResNet

#### understand multi-attn
---

## 2016-11-24
#### Word error rate

minimum number of editing steps to transform output to reference.

1. match: words match, no cost

2. substitution: replace one word with another

3. insertion: add word

4. deletion: drop word

5. WER=(substitutions+insertions+deletions)/reference-length

6. bleu:n-gram overlap between machine translation output and reference translation

   (http://www.statmt.org/book/slides/08-evaluation.pdf)

---

## 2016-11-28

#### Strategies for paraphrasing:
(https://arxiv.org/pdf/cs/0112005v1.pdf)

1.Synonyms:

   Original: 65 is the traditional age for workers to retire in the U.S.

   Paraphrase: 65 is the traditional age for employees to retire in the U.S.

2.Condensation:

   Original: 65 is the traditional age for workers to retire in the U.S.

   Paraphrase: 65 is the traditional retirement age in the U.S.

3.Circumlocution

   Original: 65 is the traditional age for worker to retire in the U.S.

   Paraphrase: 65 is the traditional age for workers to end their professional career in the U.S.

4.Phrase Reversal

   Original: 65 is the traditional age for workers to retire in the U.S.

   Paraphrase: In the U.S., the traditional age for workers to retire is 65.

5.Active-Passive Voice

   Original: The company fired 15 workers.

   Paraphrase: 15 workers were fired by the company.

6.Alternate Word Form

   Original: A manager’s success is often due to perseverance.

   Paraphrase: A manager often succeeds because of perseverance. Managers’ success is often because they persevere.


---
## 2016-12-01

#### read train.lua
when attn=0 use the hidden state of the last rnn unit as the context vector.
---

## 2016-12-02

#### read Semantic Parsing via Paraphrasing

## 2016-12-12

#### read [Tagger: Deep Unsupervised Perceptual Grouping](https://arxiv.org/pdf/1606.06724v2.pdf)

#### read [GAN tutorial](http://www.jiqizhixin.com/article/1969)
---

## 2016-12-13

#### read [Generating Sentences From a Continuous Space](https://arxiv.org/pdf/1511.06349v2.pdf)

#### read [Reasoning With Neural Tensor Networks for Knowledge Base Completion](https://papers.nips.cc/paper/5028-reasoning-with-neural-tensor-networks-for-knowledge-base-completion.pdf#cite.Graupmann)

#### read [A Neural Conversational Model](https://arxiv.org/pdf/1506.05869v3.pdf)
---

## 2016-12-14

#### Seven possible relations between phrases/sentences.

(http://web.stanford.edu/class/cs224u/materials/cs224u-2016-bowman.pdf) slide:23

1. equivalence

2. forward entailment

3. reverse entailment 

4. negation

5. alternation

6. cover

7. independence

#### Readings

#### read [Generating Natural Language Inference Chains](https://arxiv.org/pdf/1606.01404v1.pdf)

#### read [Paraphrase-Driven Learning for Open Question Answering](http://knowitall.cs.washington.edu/paralex/acl2013-paralex.pdf)

#### read [A Roadmap towards Machine Intelligence](https://arxiv.org/abs/1511.08130)

#### read [SeqGAN: Sequence Generative Adversarial Nets with Policy Gradient](https://arxiv.org/pdf/1609.05473v5.pdf)

---
## 2016-12-16

#### read [Data Generation as Sequential Decision Making](https://arxiv.org/pdf/1506.03504v3.pdf)

#### read [Generating Chinese Classical Poems with RNN](https://arxiv.org/pdf/1604.01537.pdf)

#### read [Tracking The World State With Recurrent Entity Networks](https://arxiv.org/pdf/1612.03969v1.pdf)

---
##2016-12-19
#### read [Learning Distributed Word Representations for Natural Logic Reasoning](http://www.aaai.org/ocs/index.php/SSS/SSS15/paper/view/10221/10027)

---

## 2016-12-20

#### read [A Neural Attention Model for Abstractive Summarization](https://arxiv.org/pdf/1509.00685v2.pdf)

#### read [Monolingual Machine Translation for Paraphrase Generation](https://www.microsoft.com/en-us/research/publication/monolingual-machine-translation-for-paraphrase-generation/)

---

## 2016-12-22

#### read [DIRT – Discovery of Inference Rules from Text](https://pdfs.semanticscholar.org/511c/439c59f9bbfeb3be135d85ee75bef5594ad2.pdf)

Ideas: words that tend to occur in the same contexts tend  to  have  similar  meanings.

#### read [Character-Aware Neural Language Models](https://arxiv.org/pdf/1508.06615v4.pdf)

Ideas: each filter of the CharCNN is essentially learning to detect particular character n-grams.

---

## 2016-12-23

#### read [Dual Learning for Machine Translation](https://arxiv.org/pdf/1611.00179.pdf)

#### read [中文信息处理发展报告](http://cips-upload.bj.bcebos.com/cips2016.pdf)

#### read [Connectionist Temporal Classification: Labelling Unsegmented Sequence Data with Recurrent Neural Networks](http://www.cs.toronto.edu/%7Egraves/icml_2006.pdf)

---

## 2016-12-26

####繁简转换

opencc -i wiki.zh.text -o wiki.zh.text.jian -c zht2zhs.ini

---

## 2016-12-27

#### read [Phased LSTM: Accelerating Recurrent Network Training for Long or Event-based Sequences](https://arxiv.org/pdf/1610.09513v1.pdf)

#### read [Chinese sentence segmentation as comma classification](http://www.aclweb.org/anthology/P11-2111)

The punctuation comma in Chinese sometimes functions as a period causing the diffuculty of segmenting sentences in a paragraph.

---

## 2016-12-30

#### read [Data Programming:Creating Large Training Sets, Quickly](https://arxiv.org/pdf/1605.07723v2.pdf)

#### read [Sentence Boundary Detection for Social Media Text](http://amitavadas.com/Pub/SBD_ICON_2015.pdf)

---

## 2016-01-02

#### read [text segmentation](https://en.wikipedia.org/wiki/Text_segmentation)

#### read [Elephant:Sequence Labelling for Word and Sentence Segmentation](http://www.aclweb.org/anthology/D13-1146)

IOB tokenization

Label tokens of a sentence.

#### install ruby 2.3.3

```
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev

cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL

rbenv install 2.3.3
rbenv global 2.3.3
ruby -v
#optional:
echo "gem: --no-ri --no-rdoc" > ~/.gemrc
```

---

## 2017-01-05

#### read [Semantic Parsing: The Task, the State-of-the-Art and the Future](http://www.aclweb.org/anthology/P10-5006)

#### read [Unsupervised Semantic Parsing](http://research.microsoft.com/en-us/um/people/hoifung/papers/poon09.pdf)

---

## 2017-01-06

#### read [The Ubuntu Dialogue Corpus: A Large Dataset for Research in Unstructured Multi-Turn Dialogue Systems](https://arxiv.org/pdf/1506.08909v3.pdf)

Retrieve-based chatbot. Use dual encoders to predict whether a context and a response is a match.

---

## 2017-01-09

#### read [Show and Tell](https://arxiv.org/pdf/1609.06647v1.pdf)

#### read [Deep Visual-Semantic Alignments for Generating Image Descriptions](http://cs.stanford.edu/people/karpathy/cvpr2015.pdf)

---

## 2017-01-10

#### find a repo which is able to convert pdf into html (https://github.com/coolwanglu/pdf2htmlEX)

magic installation:(https://gist.github.com/rajeevkannav/d07f822e209a22d07176)

#### Install Docker

(https://docs.docker.com/engine/installation/linux/ubuntulinux/)

```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates
sudo apt-key adv \
               --keyserver hkp://ha.pool.sks-keyservers.net:80 \
               --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" | sudo tee /etc/apt/sources.list.d/docker.list
sudo apt-get update
sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virtual
sudo apt-get update
sudo apt-get install docker-engine
sudo service docker start
sudo docker run hello-world
```

---

## 2017-01-13
#### install tomcat

```
tar -zxvf apache-tomcat-7.0.73.tar.gz
sudo mv apache-tomcat-7.0.73 /opt/
cd /opt/apache-tomcat-7.0.73/bin/

sudo gedit setclasspath.sh
//add the following text to setclasspath.sh in the beginning
//export CATALINA_HOME=/opt/apache-tomcat-7.0.73
//export JAVA_HOME=/usr/local/java/jdk1.7.0_80

sudo ./startup.sh
//Using CATALINA_BASE:   /opt/apache-tomcat-7.0.73
//Using CATALINA_HOME:   /opt/apache-tomcat-7.0.73
//Using CATALINA_TMPDIR: /opt/apache-tomcat-7.0.73/temp
//Using JRE_HOME:        /usr/lib/jdk/jdk1.7.0_80
//Using CLASSPATH:       /opt/apache-tomcat-//7.0.73/bin/bootstrap.jar:/opt/apache-tomcat-7.0.73/bin/tomcat-juli.jar
//Tomcat started.

sudo ./shutdown.sh
//Using CATALINA_BASE:   /opt/apache-tomcat-7.0.73
//Using CATALINA_HOME:   /opt/apache-tomcat-7.0.73
//Using CATALINA_TMPDIR: /opt/apache-tomcat-7.0.73/temp
//Using JRE_HOME:        /usr/lib/jdk/jdk1.7.0_80
//Using CLASSPATH:       /opt/apache-tomcat-//7.0.73/bin/bootstrap.jar:/opt/apache-tomcat-7.0.73/bin/tomcat-juli.jar
```

---

## 2017-01-16

#### install opencv2.4.11 for nvidia gtx series card with cuda 8.0
Useful blog(http://blog.csdn.net/xuzhongxiong/article/details/52717285)
```
sudo apt-get install build-essential  
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev


cd opencv-2.4.11
gedit modules/gpu/src/graphcuts.cpp
replace line 45 with "#if !defined (HAVE_CUDA) || defined (CUDA_DISABLER) || (CUDART_VERSION>=8000)"
mkdir build
cd build


cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D CUDA_GENERATION=Kepler ..
make -j8
sudo make install
#sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'  
#sudo ldconfig 

sudo apt-get install ant
#export JAVA_HOME=/usr/lib/jvm/java-6-oracle
cmake -DBUILD_SHARED_LIBS=OFF ..
make -j8
sudo make install
```

---

## 2017-01-17

#### Configure opencv library path in IDEA:
1. open "file/project structure/dependencies", add opencv jar.

2. open "file/project structure/libraries/+/java", add opencv jar.

3. in vm option, write: -Djava.library.path=/your_opencv_path/release/lib

4. add "System.loadLibrary(Core.NATIVE_LIBRARY_NAME);" in java file

## 2017-01-22

#### Install CUDA-8.0 on ubuntu14.04 with kernel:4.2.0-27-generic
```
sudo apt-get update
sudo apt-get install nvidia-367
sudo apt-get install mesa-common-dev
sudo apt-get install freeglut3-dev
sudo reboot

sudo apt-get install g++
sudo service lightdm stop
#don't install driver in the next step!!!
sudo sh cuda_8.0.44_linux.run
sudo reboot

sudo gedit /etc/profile
source /etc/profile

uname -r
nvcc -V
```
---

## 2017-01-23

#### Install cuDNN5.1
```
tar xvzf cudnn-8.0-linux-x64-v5.1-ga.tgz
sudo cp -P cuda/include/cudnn.h /usr/local/cuda-8.0/include
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-8.0/lib64
sudo chmod a+r /usr/local/cuda-8.0/include/cudnn.h /usr/local/cuda-8.0/lib64/libcudnn*
```

#### Install tensorflow with gpu support for python 2.7
```
sudo apt-get install python-pip python-dev
export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-0.12.1-cp27-none-linux_x86_64.whl
sudo pip install --upgrade $TF_BINARY_URL
```

#### Configure Shiny Server
```
sudo gedit /etc/shiny-server/shiny-server.conf
change "run_as shiny" to "run_as username"
sudo ufw allow 3838/tcp
```
---

## 2017-01-24

#### Deploy web application environment with Gradle and Idea

1. Follow instructions (https://my.oschina.net/u/1010578/blog/390094)

2. Set artifact (http://blog.csdn.net/petershusheng/article/details/52382216)

3. Add jsp-api.jar and servlet-api.jar

---

## 2017-02-08

#### Read [A Neural Network for Factoid Question Answering over Paragraphs](https://cs.umd.edu/~miyyer/pubs/2014_qb_rnn.pdf)

#### Read [Multi-Perspective Context Matching for Machine Comprehension](https://arxiv.org/pdf/1612.04211.pdf)

#### Read [Question Answering](https://web.stanford.edu/~jurafsky/slp3/28.pdf)

##### IR-based question answering

##### knowledge-based question answering
Why QA?
What kind of questions should be answered by a  domain specific QA system?

---

## 2017-02-09

#### Read [A Rule-based Question Answering System for Reading Comprehension Tests](https://www.cs.utah.edu/~riloff/pdfs/quarc.pdf)

#### Read [Stanford QA slides](https://www.fosteropenscience.eu/sites/default/files/pdf/2930.pdf)

#### Read [Stanford chatbot slides](https://web.stanford.edu/class/cs124/lec/chatbot.pdf)
---

## 2017-02-10

#### Read [StalemateBreaker: A Proactive Content-Introducing Approach to Automatic Human-Computer Conversation](https://arxiv.org/pdf/1604.04358.pdf)

#### Read [Building End-To-End Dialogue Systems Using Generative Hierarchical Neural Network Models](https://arxiv.org/pdf/1507.04808.pdf)

## 2017-02-13

#### Install ffmpeg
```
sudo add-apt-repository ppa:kirillshkrogalev/ffmpeg-next
sudo apt-get update
sudo apt-get install ffmpeg
``` 

## 2017-02-20

#### Read [Bilateral Multi-Perspective Matching for Natural Language Sentences](https://arxiv.org/pdf/1702.03814.pdf)

## 2017-02-23

#### Read [Paraphrase Pattern Acquisition by Diversifiable Bootstrapping](http://www.lti.cs.cmu.edu/sites/default/files/research/thesis/2015/hideki_shima_paraphrase_pattern_acquisition_by_diversifiable_bootstrapping.pdf)

## 2017-02-24

#### Hypothesis

1. Distributional Hypothesis: Words that occur in similar contexts tend to have similar meanings
2. Extended Distributional Hypothesis: Patterns that co-occur with similar pairs tend to have similar meanings.
3. Latent  Relation  Hypothesis: Pairs  of  words  that  co-occur in similar patterns tend to have similar semantic relations.
4. a multi-instance learning assumption (Dietterich et al., 1997) that two sentences under the same topic (we highlight topics in bold) are paraphrases if they contain at least one word pair.

#### Read [Modeling Sentences in the Latent Space](http://www.aclweb.org/anthology/P12-1091v2)

## 2017-02-27

#### Read [Baidu lecture on Paraphrasing](http://www.aclweb.org/anthology/C10-4001)


## 2017-02-28
Met a problem when creating a project by scrapy. 
```
AttributeError: 'module' object has no attribute 'OP_NO_TLSv1_1'
```
Solution:
```
sudo pip install openssl
sudo pip install --upgrade pyOpenSSl
```
---
## 2017-03-08
copy random N files to a directory
```
ls | shuf -n 11 | xargs cp -t /home/han/Desktop/
```
---
## 2017-03-24

#### Read [Incorporating Copying Mechanism in Sequence-to-Sequence Learning](http://cn.arxiv.org/pdf/1603.06393v2.pdf)
---
## 2017-03-27

#### Read [TextRank:Bringing Order into Texts](https://web.eecs.umich.edu/~mihalcea/papers/mihalcea.emnlp04.pdf)
---
## 2017-03-28

#### Read [You Only Look Once:Unified, Real-Time Object Detection](https://arxiv.org/pdf/1506.02640.pdf)


"Sum-squared error also equally weights errors in large boxes and small boxes. Our error metric should reflect that small  deviations  in  large  boxes  matter  less  than  in  small boxes.  To partially address this we predict the square root of the bounding box width and height instead of the width and height directly."

#### Read [Learning Mixtures of Submodular Shells with Application to Document Summarization](https://arxiv.org/pdf/1210.4871.pdf)

#### Read [A Class of Submodular Functions for Document Summarization](http://www.aclweb.org/anthology/P11-1052)

---
## 2017-03-29
```
#rename all files in a directory
n=1
for f in `ls ./`;do mv $f $n.jpg; echo $n; n=$[$n+1]; done
```

---
## 2017-03-30
```
mydir = check
mkdir $mydir
cat result.txt | awk -F " " '{if($2<="0.5") print $0}' > prob_less_50.list
n=1;for f in `cat prob_less_50.list`;do cp $f ./$mydir/$n.jpg; echo $n; n=$[$n+1]; done
ls ./mydir > rest.txt
python sel.py prob_less_50.list rest.txt todel.txt
cat todel.txt norpl.txt > negd.txt
python del.py poss2.txt todel.txt poss3.txt
python del.py xg1.txt todel.txt xg2.txt 
```

---
## 2017-04-13

#### Read [Mask R-CNN](https://arxiv.org/pdf/1703.06870.pdf)

#### Read [Global Contrast based Salient Region Detection](http://vecg.cs.ucl.ac.uk/Projects/SmartGeometry/contrast_saliency/paper_docs/contrast_saliency_small_cvpr11.pdf)

## 2017-04-19

#### Read [TextTiling:Segmenting Text into Multi-paragraph Subtopic Passages](http://anthology.aclweb.org/J/J97/J97-1003.pdf)

## 2017-04-24
#### Read [Neural Paraphrase Generation with Stacked Residual LSTM Networks](https://arxiv.org/pdf/1610.03098.pdf)

## 2017-04-27
#### Read [When Are Tree Structures Necessary for Deep Learning of Representations](https://nlp.stanford.edu/pubs/emnlp2015_2_jiwei.pdf)

#### Read [Neural Machine Translation and Sequence-to-sequence Models:A Tutorial](https://arxiv.org/pdf/1703.01619.pdf)

## 2017-05-08
#### Read [Generating Sentences from a Continuous Space](https://arxiv.org/pdf/1511.06349.pdf)

## 2017-05-10
#### Read [Convolutional Sequence to Sequence Learning](https://arxiv.org/pdf/1705.03122.pdf#cite.wu2016google)

#### Read [A Convolutional Encoder for Neural Machine Translation](https://arxiv.org/pdf/1611.02344.pdf)

## 2017-05-15
check disk space
```
df -h
```

## 2017-05-23
use Kaldi
```
#install Kaldi
git clone https://github.com/suzhoushr/kaldi-shr.git
cd kaldi-shr/
chmod +x -R extras/
chmod +x configure
cd ./tools
#tar -xvzj openfst-1.3.4.tar.gz
./extras/check_dependencies.sh
#sudo apt-get install  subversion
sudo ln -s -f bash /bin/sh
make -j4
cd ../src
./configure
make -j4
#cd ../nnetbin/
#make -j4
#preprocess data
./shr_scripts/chw/utils/img2condata.py train.list "train" | copy-feats ark:- ark,scp:./data/data.tr.ark,./data/data.tr.scp
./shr_scripts/chw/utils/img2condata.py val.list "test" | copy-feats ark:- ark,scp:./data/data.cv.ark,./data/data.cv.scp
```


## 2017-06-05

#### Read [A fast learning algorithm for deep belief nets](https://www.cs.toronto.edu/~hinton/absps/fastnc.pdf)

#### Read [Greedy Layer-Wise Training of Deep Networks](http://www.iro.umontreal.ca/~lisa/pointeurs/BengioNips2006All.pdf)

#### Read [Efficient Learning of Sparse Representations with an Energy-Based Model](http://machinelearning.wustl.edu/mlpapers/paper_files/NIPS2006_804.pdf)

## 2017-06-23

deploy war package in tomcat. encountered a problem "java.lang.UnsatisfiedLinkError: no segmentor_jni in java.library.path"

solved by 
```
sudo gedit /opt/apache-tomcat-7.0.78/bin/catalina.sh
\#write
JAVA_OPTS=" -Djava.library.path=/home/han/Software/ltp4j/libs"
```

compile ltp4j on centos
```
cmake -DLTP_HOME=`pwd`/ltp/ .
make
```

## 2017-07-11

#### Read[Recursive Recurrent Nets with Attention Modeling for OCR in the Wild](https://arxiv.org/pdf/1603.03101v1.pdf)


## 2017-08-03

compile java from shell

```
javac -classpath /path/to/jar test.java
java -Djava.ext.dirs=/path/to/jar/ test
```


## 2017-08-15

train a language model using irsltm
```
/disk03/czj_workspace/irstlm/build/bin/build-lm.sh -i data_ltp.txt -n 4 -f 3,3,2,2 -k 10 -v -o train.irstlm.gz
```

## 2017-08-16

```
\#check tomcat process id 

ps -ef | grep tomcat

\#check tomcat log

tail -100f ./logs/catalina.out
```

## 2017-08-17

zip and upload file at the same time
```
rsync -z -P data_ltp.txt -e "ssh -p 59522" root@###.###.##.###:/data/czj_workspace
```

```
cat data_sentence.txt | sed 's/[ ]*[,，][ ]*/，\n/g' | awk '{if(length($0)>5) print}' | grep -E "大有.*之势" | less
```

#### Read[Lexicon-Free Conversational Speech Recognition with Neural Networks](http://deeplearning.stanford.edu/lexfree/lexfree.pdf)



### 2017-11-03

#### Read[A systematic study of the class imbalance problem in convolutional neural networks](https://arxiv.org/pdf/1710.05381.pdf)

Methods for addressing data imbalance

### 2017-11-06

#### Read[Don't Decay the Learning Rate, Increase the Batch Size](https://arxiv.org/pdf/1711.00489.pdf)



### 2017-11-07

read paper abstractions on NIPS 2016

##### Scan Order in Gibbs Sampling: Models in Which it Matters and Bounds on How Much

gibbs sampling, scan order, random scan, systematic scan.

#####  Deep ADMM-Net for Compressive Sensing MRI

ADMM-net, to reconstruct MRI data from a small number of under-sampled data

#####  A scaled Bregman theorem with applications

Bregman theorem

#####  Swapout: Learning an ensemble of deep architectures

swapout, a regularization method, combination of dropout and stochastic depth.

#####  On Regularizing Rademacher Observation Losses

introduced rado loss for classification problems

#####  Without-Replacement Sampling for Stochastic Gradient Methods

as the name of the paper suggests.

#####  Fast and Provably Good Seedings for k-Means

provide fast and competitive seedings for k-Means clustering without prior assumptions on the data

#####  Unsupervised Learning for Physical Interaction through Video Prediction

learn about physical object motion without labels

#####  High-Rank Matrix Completion and Clustering under Self-Expressive Models

#####  Learning a Probabilistic Latent Space of Object Shapes via 3D Generative-Adversarial Modeling

generate 3D objects 

#####  Visual Dynamics: Probabilistic Future Frame Synthesis via Cross Convolutional Networks

use a single input frame to generate future frames.

#####  Human Decision-Making under Limited Time

Human decision-making practically is not optimal under constraints such as time.

#####  Incremental Boosting Convolutional Neural Network for Facial Action Unit Recognition

Boosting CNN for facial action recognition.

#####  Natural-Parameter Networks: A Class of Probabilistic Neural Networks

a bayesian treatment for NN, to alleviate the problem of insufficient data.

#####  Tree-Structured Reinforcement Learning for Sequential Object Localization

existing object detection algorithms ignore interdependency among different objects and deviate from the human perception procedure

#####  Unsupervised Domain Adaptation with Residual Transfer Networks

transfer learning

#####  Verification Based Solution for Structured MAB Problems

mutli-armed bandit?

#####  Minimizing Regret on Reflexive Banach Spaces and Nash Equilibria in Continuous Zero-Sum Games

#####  Linear dynamical neural population models through nonlinear embeddings

##### SURGE: Surface Regularized Geometry Estimation from a Single Image

predict pixel depth in a image.

#####  Interpretable Distribution Features with Maximum Testing Power

distinguish distributions

#####  Sorting out typicality with the inverse moment matrix SOS polynomial

#####  Multi-armed Bandits: Competing with Optimal Sequences

#####  Multivariate tests of association based on univariate tests

Test the independence of two random vectors, convert multivariate test to univariate test by imposing a distance measure.

#####  Learning What and Where to Draw

Sythesize images using GAN given what and where to draw.

#####  The Sound of APALM Clapping: Faster Nonsmooth Nonconvex Optimization with Stochastic Asynchronous PALM

a block coordinate stochastic proximal-gradient method for solving nonconvex, nonsmooth optimization problems

##### Integrated perception with recurrent multi-task neural networks

multi-task learning

#####  Learning from Small Sample Sets by Combining Unsupervised Meta-Training with CNNs

#####  CNNpack: Packing Convolutional Neural Networks in the Frequency Domain

compressing CNN
