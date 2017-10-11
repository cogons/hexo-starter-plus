---
title: MacOS下Hadoop安装记
tags:
  - Originals
number: 7
date: 2017-04-30 12:34:28
---

# 安装Homebrew

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

官网：https://brew.sh/index_zh-cn.html

# 安装Hadoop

```
brew install hadoop
```

## 查看安装路径：

```
brew list hadoop
```

# 配置Hadoop

## 前往安装目录（默认为/usr/local/Cellar/hadoop/2.8.0）

```
cd /usr/local/Cellar/hadoop/2.8.0/libexec/etc/hadoop/
```

## 修改相关配置文件

### Core-site.xml

```
<configuration>
  <property>
     <name>hadoop.tmp.dir</name>  
     <value>/usr/local/Cellar/hadoop/hdfs/tmp</value>
    <description>A base for other temporary directories.</description>
  </property>
  <property>
     <name>fs.default.name</name>                                     
     <value>hdfs://localhost:9000</value>                             
  </property>                                                       
</configuration> 
```

### mapred-site.xml.templete

```
<configuration>
       <property>
         <name>mapred.job.tracker</name>
         <value>localhost:9010</value>
       </property>
 </configuration>
```

### hdfs-site.xml

```
<configuration>
    <property>
      <name>dfs.replication</name>
      <value>1</value>
     </property>
 </configuration>
```

# 运行Hadoop

## 格式化Namenode

```
cd /usr/local/Cellar/hadoop/2.8.0/bin
hadoop namenode -format
```

## 启动Hadoop

```
cd /usr/local/Cellar/hadoop/2.8.0/sbin
./start-all.sh
```

# 检查运行状态

## Jps

```
jps
```

查看以下服务是否正常启动

> 94945 DataNode
> 
> 95059 SecondaryNameNode
> 
> 94853 NameNode
> 
> 95318 Jps
> 
> 95181 ResourceManager
> 
> 95279 NodeManager

## 访问以下网址

Resource Manager: http://localhost:50070

JobTracker: http://localhost:8088

Specific Node Information: http://localhost:8042