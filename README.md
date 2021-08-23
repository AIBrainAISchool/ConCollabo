# ConCollabo

Collaborate with friends in this AI powered twitter like application. Share poems, updates and photos. Collaborate and contend with friends and find your soulmate

Product Architecture

![image](https://user-images.githubusercontent.com/86698483/130388891-15106291-344d-48d8-afbc-f61b9ffa9daf.png)

1. Overview
In this project we will portray how a model can be fine-tunned and trained and linked to a mobile application  with an API . This project involved three main parts. Here is a brief outline.

Part 1. Model Overview
Overview – Brief overview
GPT-2 – Explanation on model to be trained.
Dataset Preparation – How the data will be prepared.
Google Colab Setup – Notebook Setup and Cloning
Model Training –  Finetunning GPT-2
Inferencing – Inferencing Model
Part 2. Application – App Template Installation
App Setup – Complete Setup and Build

2. GPT-2
We will start this section with an overview about GPT-2. GPT-2 is a popular transformer based model developed by Open AI. The original GPT-2 model released by OpenAI was trained on English webpages linked to from Reddit, with a strong bias toward longform content (multiple paragraphs).

If that is not your use case, you may get a better generation quality and speed by training your own model and Tokenizer. Examples of good use cases:

Short-form content (e.g. Tweets, Reddit post titles)
Non-English Text
Heavily Encoded Text
It still will require a massive amount of training time (several hours) but will be more flexible.

Paper: “Language Models are Unsupervised Multitask Learners”
“advanced version of a transformer-based model that was trained to generates synthetic text samples from a variety of user-prompts as input”

4 Models:
1.5B XL (pre-trained model not released)
774M Large
355M Medium
124M Small (Also referred to as 117M)
Referenced GitHub: https://github.com/nshepperd/gpt-2

Different GPT-2 Models

3. Dataset Preparation
Gathering great quality data is one of the most critical stages in machine learning.
We could use any English data or even data from Novels

In this tutorial, we will use Haiku Poems Data;
We could later extend the model on other datasets such as;
Song lyrics or
News articles
The dataset is just one single text file
After every sample, delimit each sample with:

<|endoftext|> (this could be done with a python script)

Automatable with python scripts (crawling)

Sample Dataset
last red in the sky
a small girl's moon face rises
over the counter
<|endoftext|>

christmas services
a cellular phone rings out
handel's messiah
<|endoftext|>

Passover darkness -
before the buds burst open;
a child's eyes in death.
<|endoftext|>

Last night of Summer
the bright full moon of last night
hidden by a cloud
<|endoftext|>
Here's the data set.
About Our Data

It’s one single text file
It could be noted that after every sample, the data is being seperated with:
<|endoftext|>

This helps the model when training to understand the data.
Data was crawled from the internet using python scripts. But also, other data sources could be used like Kaggle or Github.
 
4. Collab Setup
Google Colab is a Jupyter notebook like environment developed and maintained by Google with the ability to choose between CPUs and GPUs and also TPUs. It’s just like all other Jupyter notebooks with the ability to code in Python and also markdown. 

We will setup Google Colab for cloning the github repository and GPT Model Training.

 To get started with Google Colab, all you need to do is go to https://colab.research.google.com/ and select:

NEW PYTHON 3 NOTEBOOK from the popup menu.

Platform independence: As the Jupyter notebooks can be accessed directly from a browser, we can have any machine, Mac, Windows, Linux etc. and it’ll work exactly the same.

Free resource availability: Training models for deep learning require a lot of power and hence, not all laptops and desktops are equipped for it. Google Colab provides free acce

5. Training
Here's a link of the complete setup in Google Collab.
Train Preparation

First we need to download the pre-trained model

$ python download_model.py 117M
Once downloaded, we should have a <gpt-2/models/117M> folder with the following files:

checkpoint
encoder.json
hparams.json
model.ckpt.data-00000-of-00001
model.ckpt.index
model.ckpt.meta
Vocab.bpe
Place the dataset file into the cloned folder

Before we start training, move the train.py from into <gpt-2/src> folder

Let’s start training

$ cd src

$ python src/train.py --dataset input.txt --model_name 117M
The code will automatically save checkpoints every 1,000 steps

How to stop training?

Ctrl + C

This will automatically save the current checkpoint to <gpt-2/checkpoint>

How to resume training?

$ python train.py –dataset input.txt –model_name 117M

This will automatically resume fine tuning from where we left off.

 
$ cd src

$ python src/train.py --dataset input.txt --model_name 117M

6. Inference
After training, let’s infer from our fine-tuned model

Go into <gpt-2/checkpoint/run1> and copy the following files to <gpt-2/models/117M>:

checkpoint
model-xxx.data-00000-of-00001
model-xxx.index
model-xxx.meta

Here, xxx refers to the step number. We should end up with 8 files

Above 4 files
counter
encoder.json
hparams.json
vocab.vpe

For inference, paste the 8 files into <gpt-2/models/117M> Then run:
$ python src/interactive_conditional_samples.py truncate="<|endoftext|>" --nsamples=1 --top_k 40 --top_p 40 --temperature 0.01 --model_name 117M
 

Flag breakdown

top_k : Integer value controlling diversity (40 is good)

temperature : float value; Lower temperature results in less random completions

nsamples : number of samples

truncate print until the first <|endoftext|> (try with and without this flag)

Final Results :

Here are AI Generated Haikus from our input.

(Please try in Google Colab)


Open and Clone the complete Notebook here.
P2. App Template
The next part of this tutorial will be developing a mobile app that we could with the model.

We will use an App Template called Tweetster, This is a twitter clone. 

Here’s a complete video how to setup this app. 


Download the template here.
You could proceed with app setup in this order;

Open Tweetster Project in Android Studios
Proceed with the order in the video guide above 
Ignore Update warnings from Android Studio.
Copy only google-services.json when connecting to firebase, ignore copy/paste buildgradle (ignore from the video)
Link Admob API token, Please create an account if you don’t have one.
Link Agora API token. Create an account if you don’t have one (Ignore payment registration)
In order to prevent errors unlike the video, comment the next line in the picture below.
Running the app in android studio may be slow. Using a phone may be better.
 


Build the app.


In the  last section of this tutorial, we will setup an API In the cloud and link to the Model.
Heres the setup;

Setup 1: Basic
Sign up for AWS
Create a key pair
Create a security group
Setup 2: Instance
Launch an instance
Configure / Edit security group
Connect to instance
Windows, Mac / Linux
Clean instance
Terminate
Setup 1: Basics
Base Documentation: 

https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html

 

Sign up for AWS
 

Create a key pair
Format should be <.pem>
This is a private key. Do not lose this, nor share with anyone else
Create a security group
Setup 2: Instance

Base Documentation: https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/EC2_GetStarted.html

 

Launch
AMI: Amazon Linux 2 (free tier)
Instance type: t2.micro (free tier)
Next: Configure Instance Details (Default)
Next: Add Storage (Around 50 GB)
Next: Add Tags (Default)
Configure Security Group: Enable Inbound ports 
Connect
https://docs.aws.amazon.com/en_us/AWSEC2/latest/UserGuide/AccessingInstances.html
For this example, I am using Windows Terminal – PowerShell
Take note of:
Path to the key pair on the local machine
Instance user name
Instance public dns
$ ssh -i /path/my-key-pair.pem my-instance-user-name@my-instance-public-dns-name
Windows

$ ssh -i “C:\Users\user\.ssh\MyKeyPair.pem” ec2-user@13.125.230.222

Linux / Mac

$ ssh -i “~/.ssh/MyKeyPair.pem” ec2-user@13.125.230.222

Basic Setup
Environment Setup (Miniconda)

Go to home directory, create a “Downloads” folder to manage downloaded files

 

Update
$ sudo yum update

Install Epel
$ sudo amazon-linux-extras install epel

Install p7zip
$ sudo yum install p7zip

Copy local files to the instance:
To copy <gpt-2-api.zip> to instance, open a new terminal and type:
$ scp -i "path/to/keypair.pem" "path/to/file/to/copy" ec2-user@13.125.230.222:"path/to/destination/file"

Swap – Memory Allocation

Running GPT-2 requires more memory than the default provided by t2.micro free tier (1GB)
Without allocating more memory, the GPT-2 app will crash due to out of memory error
To allocate more memory, we will use a method called “swap space”
Swap space is assigning and using a portion of storage as RAM

Follow the instructions here, or in short:

$ sudo dd if=/dev/zero of=/swapfile bs=128M count=32

$ sudo chmod 600 /swapfile

$ sudo mkswap /swapfile

$ sudo swapon /swapfile

$ sudo swapon -s

$ sudo nano /etc/fstab
Add the following new line at the end of the file, and then exit:

/swapfile swap swap defaults 0 0
Install and Adjust

To install gpt-2-api, follow the instructions from Pg. 12 (Environment Setup) of Part 2: API
app was originally developed for local test use, and now that we want to deploy it on Cloud, we need to make adjustments
We need to direct the communication
to 0.0.0.0:5000 instead of 127.0.0.1:5000
in
Open the file and edit:

$ nano server.py

We have multiple python scripts to run simultaneously
gpt-2-api/gpt-2/server.py
gpt-2-api/types/app.py

Solution: open multiple terminals and connect each to the instance!

[Running the scripts is the same as in Part 2]

Whenever a new connection is created, make sure you are activate the virtual (conda) environment

Interact
http://x.x.x.x:5000/?Text=a beautiful weather tonight&Type=poem&Genre=haiku
Text=
Type= Genre=<haiku, poetry_mix, kids, rnb, pop>

Interacting with the app is the same as in Part 2; just the IP address changes
Replace the dummy IP address (x.x.x.x) with your Public IPv4 address
This address is identical to the address which you have used to SSH into
Conclusions

If you arrived here congratulations. You completed this tutorial. Please be sure to try every section of this tutorial and check back for updates.

Next Steps : Link everysection into an application

Learn More: http://aifactory.global/factory-detail/
