---
title: "Fedora 25 + Maven + Java-1.8.0-openjdk: core dumps"
layout: post
date: 2017-01-28 16:30
image: /assets/images/markdown.jpg
headerImage: false
tag:
- java
- maven
- fedora 25
- bug
blog: true
star: false
description: How to solve core dump bug with Fedora
---

## Fedora 25 + Maven + Java-1.8.0-openjdk: core dumps

Yesterday I update my Fedora 25 distro. Today I was trying to compile a java plugin with Maven and I received this bizarre error message:

```
mvn install
[INFO] Scanning for projects...
Downloading: https://repo.maven.apache.org/maven2/external/atlassian/jgitflow/jgitflow-maven-plugin/1.0-m5.1/jgitflow-maven-plugin-1.0-m5.1.pom
#
# A fatal error has been detected by the Java Runtime Environment:
#
#  SIGSEGV (0xb) at pc=0x00007f7022f0c711, pid=2530, tid=0x00007f7023bc5700
#
# JRE version: OpenJDK Runtime Environment (8.0_111-b16) (build 1.8.0_111-b16)
# Java VM: OpenJDK 64-Bit Server VM (25.111-b16 mixed mode linux-amd64 compressed oops)
# Problematic frame:
# C  [libc.so.6+0x14f711]  __memmove_avx_unaligned_erms+0x211
#
# Failed to write core dump. Core dumps have been disabled. To enable core dumping, try "ulimit -c unlimited" before starting Java again
#
# An error report file with more information is saved as:
# /home/scb/Development/casalebrunet/orcc/eclipse/plugins/hs_err_pid2530.log
#
# If you would like to submit a bug report, please visit:
#   http://bugreport.java.com/bugreport/crash.jsp
#
/usr/bin/mvn: line 20:  2530 Aborted                 (core dumped) $M2_HOME/bin/mvn "$@"
```

So I just tried out to compile another plugin from another project: same strange error. What's that?!! 

Googling I found that this is a known bug: [https://bodhi.fedoraproject.org/updates/FEDORA-2017-4076cf8494](https://bodhi.fedoraproject.org/updates/FEDORA-2017-4076cf8494).
The problem has been fixed but the patch is still on the testing fedora repository. So, in order to install the patch and successfully fix the problem you have to do that:

- Dowload the fix from [here](http://koji.fedoraproject.org/koji/search?terms=java-1.8.0-openjdk-1.8.0.121-1.b14.fc25&type=build&match=glob)
- Run ```sudo dnf install java-1.8.0-openjdk-1.8.0.121-1.b14.fc25.x86_64.rpm --enablerepo=updates-testing```

That's all!
Cheers,
S.



 

