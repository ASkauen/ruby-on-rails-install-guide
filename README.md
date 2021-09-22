# Ruby on Rails development environment setup guide
 ## ***How to follow this guide:***
* Choose your operating system\
    &nbsp; &nbsp; &nbsp;- [Ubuntu](#ubuntu)\
    &nbsp; &nbsp; &nbsp;- [MacOS](#macos)\
    &nbsp; &nbsp; &nbsp;- [Windows 10](#windows-10)
* Read the instructions under your chosen oparating system

    &nbsp; &nbsp; When you come across a code block:

      This is
      a code block

  > *You can copy the entire code block at once. No need to run each command individually*
  &nbsp;
  1. copy the commands inside the block
  2. Paste the commands in your terminal
  3. Run the commands by pressing enter\
&nbsp;
* Complete the steps in order from top to bottom\
&nbsp;
## **Ubuntu:**
---
&nbsp;
>### **Tips:**
>* Press &nbsp;``Ctrl + Alt + T`` &nbsp; to open a new terminal
>* Press &nbsp;``Ctrl + Shift + V`` &nbsp; to paste text in your terminal
>* Press &nbsp;``Ctrl + Shift + C`` &nbsp; to copy text from your terminal\
&nbsp;

&nbsp;
## ***Installing Ruby:***
### **First we'll install some Ruby on Rails dependencies:**
Run the following commands in your terminal:
```c
sudo apt install curl
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt-get update
sudo apt-get install git-core zlib1g-dev build-essential libssl-dev 
libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-
dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs 
yarn
```
This will add the &nbsp;``Yarn`` &nbsp;and&nbsp; ``Node.js``&nbsp; repositories to your system.\
&nbsp;
### **Then, install ``rbenv`` and ``ruby-build``:**
Run the following commands in your terminal:
```c
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL

rbenv install 3.0.2
rbenv global 3.0.2
```
&nbsp;
### **Finally, install ``bundler``:**
Run the following commands in your terminal:
```c
gem install bundler

rbenv rehash
```
&nbsp;\
Congatulations! ``Ruby 3.0.2`` is now installed.\
Now, onto the next step.\
&nbsp;\
&nbsp;

## ***Configuring Git:***
>**For this step you will need a Github account. [Register here](https://github.com/) if you don't have one already.**

&nbsp;
### **Configure username and email:**
Run the following commands in your terminal:
```c
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
ssh-keygen -t rsa -b 4096 -C "YOUR@EMAIL.com"
```
><span style="color: #06CF96">***Make sure you replace "YOUR NAME" and "YOUR@EMAIL<span>.com</span>" with your Github username and email.***</span>

&nbsp;
### **Add SSH key:**
Run the following command in your terminal:
```c
cat ~/.ssh/id_rsa.pub
```
&nbsp;\
The output should look something like this:
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDds5vtGDIppyR6qsyf+m0xYfq2WxieBBBlZBrZo4Ku9KpjVtY1v7I
6fLUgtJsxzuMMoxUwav1FG4gqkiSE26PCm1gBmlYuRxIV5XvYZRmVhkapPerLGCf1KQUhCU/9qxivSNDYo
zj5DxQjxIeF3THXFvijLtLtpFfA68ZoFbfakM672md7dyn0JTSugYzToQR48mLbKcFYGbfF2XjGLnFYePFV4
UYEaIO6oo1mq4oMZ9Qqsa25Nq6yLL4AO+tOcZzEV6Qt9iRlRCUg/FZ5CFHb6w/joOZlE2H3CilOV/q3XTfs
+iqhhsK0i7cuJMGljpaysDOIJDPjsd9uasjdoasdoDAUH12pDH990adDSJ8Qg6YkNWWh/qLEy+jiTZVNXVbJAllOaMQSmkE7/
Z6241+rYjZa5G3LLrrK1tViQxJaUsWk/VUAJJDhiuas88u2yt7ydQtF/gbBbMZQNHsu5Qw6N4BZOr9hTez+txosovDb20rE2
+oPdM= your@email.com
```
&nbsp;\
**Add the SSH key to your Github:**
>1. Copy the output
>2. Go to [this link](https://github.com/settings/keys)
>3. Click <button style="background-color: green; border: none; color: white; border-radius: 4px; height: 23px">New SSH key</button>
>4. Enter any name under **Title**
>5. Paste the output you copied earlier under **Key**
>6. Click <button style="background-color: green; border: none; color: white; border-radius: 4px; height: 23px">Add SSH key</button>
&nbsp;

&nbsp;\
To verify that it worked, run this command in your terminal:
```c
ssh -T git@github.com
```
&nbsp;\
You should get a message like this:
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```
&nbsp;\
&nbsp;

## ***Installing Rails:***

Run the following commands in your terminal:
```c
gem install rails -v 6.1.4.1

rbenv rehash
```
To verify the installation, run this command in your terminal:
```c
rails -v
```
It should output:
```
Rails 6.1.4.1
```
> *If you're getting a different output, your environment may not be set up properly.*\
*Make sure you have completed all previous steps correctly.*

&nbsp;\
&nbsp;
## ***Setting up PostgreSQL:***
### **Install ``PostgreSQL``:**
Run the following command in your terminal:
```c
sudo apt install postgresql-11 libpq-dev
```
&nbsp;
### **Create a user:**
Run the following command in your terminal:
```c
sudo -u postgres createuser username -s
```
>*You can replace ``username`` with any name you like.*

&nbsp;\
&nbsp;
## ***Testing your installation:***
Create a new Rails application by running the following commands in your terminal:
```c
rails new myapp -d postgresql #creates a new Rails app called myapp with a PostgreSQL database
cd myapp                      #sets the working directory to the application directory
rake db:create                #creates a new database
rails server                  #starts the server
```
> *You can copy the comments as well. They will be ignored.*

&nbsp;\
Go to http://localhost:3000 to look at your new app!