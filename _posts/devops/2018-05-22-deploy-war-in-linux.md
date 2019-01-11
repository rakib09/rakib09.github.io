---
layout: post
title: "Deploy Java War in Linux Server"
comments: true
categories: devops
---

## Deploy Java War in Linux Server

1. First, update the package index.

```
sudo apt-get update
or
sudo yum update
```

2. Oracle JDK 8
This is the latest stable version of Java at time of writing, and the recommended version to install. You can do so using the following command:

To show packages:
```
yum search java | grep 'java-'
```
To install if packages are available:
```
yum install java-1.8.0
```

and then:

```
alternatives --config java
```
and check:

```
java -version
```


or can download from [oracle site](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
by 

```
wget --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u171-b11/512cd62ec5174c3487ac17c61aaa89e8/jdk-8u171-linux-i586.tar.gz
```
Here you can get the latest url (wget --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.tar.gz) from the orcle site.

Then
```
tar xzvf jdk.tar.gz
sudo mkdir /usr/local/java
sudo mv jdk1.8.0_45 /usr/local/java/
sudo ln -s /usr/local/java/jdk1.8.0_45 /usr/local/java/jdk

sudo vi /etc/profile.d/java.sh
export PATH="$PATH:/usr/local/java/jdk/bin"
export JAVA_HOME=/usr/local/java/jdk

source /etc/profile.d/java.sh
```

```
cd /usr
sudo -s (for root access)
mkdir rakib
chmod -R 777 rakib/

```

```
Uninstall java
sudo yum remove jdk
```

```
Run the following command to find out process associated with yum command:
# ps aux | grep -i yum
For killing process:
kill 15401
```




