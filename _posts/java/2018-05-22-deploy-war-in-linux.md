---
layout: post
title: "Deploy Java War in Linux Server"
comments: true
categories: Java
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

```
sudo apt-get install oracle-java8-installer
or
sudo yum install oracle-java8-installer
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
```


