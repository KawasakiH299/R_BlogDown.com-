---
title: Flume listens to hive logs
author: Xin Lu
date: '2022-10-14'
slug: Flume listens to hive logs
categories: []
tags: []
---
报错现象
```
21 五月 2022 17:08:53,228 INFO  [SinkRunner-PollingRunner-DefaultSinkProcessor] (org.apache.flume.sink.hdfs.BucketWriter.open:246)  - Creating hdfs://hadoop102:9870/flume/20220521/17/logs-.1653124088090.tmp
21 五月 2022 17:08:53,249 WARN  [hdfs-k2-call-runner-0] (org.apache.hadoop.net.NetUtils.wrapWithMessage:834)  - Unable to wrap exception of type class org.apache.hadoop.ipc.RpcException: it has no (String) constructor
java.lang.NoSuchMethodException: org.apache.hadoop.ipc.RpcException.<init>(java.lang.String)
	at java.lang.Class.getConstructor0(Class.java:3082)
	at java.lang.Class.getConstructor(Class.java:1825)
	at org.apache.hadoop.net.NetUtils.wrapWithMessage(NetUtils.java:830)
	at org.apache.hadoop.net.NetUtils.wrapException(NetUtils.java:806)
	at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1549)
	at org.apache.hadoop.ipc.Client.call(Client.java:1491)
	at org.apache.hadoop.ipc.Client.call(Client.java:1388)
	at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
	at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:118)
	at com.sun.proxy.$Proxy12.create(Unknown Source)
	at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.create(ClientNamenodeProtocolTranslatorPB.java:366)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:422)
	at org.apache.hadoop.io.retry.RetryInvocationHandler$Call.invokeMethod(RetryInvocationHandler.java:165)
	at org.apache.hadoop.io.retry.RetryInvocationHandler$Call.invoke(RetryInvocationHandler.java:157)
	at org.apache.hadoop.io.retry.RetryInvocationHandler$Call.invokeOnce(RetryInvocationHandler.java:95)
	at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:359)
	at com.sun.proxy.$Proxy13.create(Unknown Source)
	at org.apache.hadoop.hdfs.DFSOutputStream.newStreamForCreate(DFSOutputStream.java:276)
	at org.apache.hadoop.hdfs.DFSClient.create(DFSClient.java:1212)
	at org.apache.hadoop.hdfs.DFSClient.create(DFSClient.java:1191)
	at org.apache.hadoop.hdfs.DFSClient.create(DFSClient.java:1129)
	at org.apache.hadoop.hdfs.DistributedFileSystem$8.doCall(DistributedFileSystem.java:531)
	at org.apache.hadoop.hdfs.DistributedFileSystem$8.doCall(DistributedFileSystem.java:528)
	at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
	at org.apache.hadoop.hdfs.DistributedFileSystem.create(DistributedFileSystem.java:542)
	at org.apache.hadoop.hdfs.DistributedFileSystem.create(DistributedFileSystem.java:469)
	at org.apache.hadoop.fs.FileSystem.create(FileSystem.java:1118)
	at org.apache.hadoop.fs.FileSystem.create(FileSystem.java:1098)
	at org.apache.hadoop.fs.FileSystem.create(FileSystem.java:987)
	at org.apache.hadoop.fs.FileSystem.create(FileSystem.java:975)
	at org.apache.flume.sink.hdfs.HDFSDataStream.doOpen(HDFSDataStream.java:81)
	at org.apache.flume.sink.hdfs.HDFSDataStream.open(HDFSDataStream.java:108)
	at org.apache.flume.sink.hdfs.BucketWriter$1.call(BucketWriter.java:257)
	at org.apache.flume.sink.hdfs.BucketWriter$1.call(BucketWriter.java:247)
	at org.apache.flume.sink.hdfs.BucketWriter$8$1.run(BucketWriter.java:727)
	at org.apache.flume.auth.SimpleAuthenticator.execute(SimpleAuthenticator.java:50)
	at org.apache.flume.sink.hdfs.BucketWriter$8.call(BucketWriter.java:724)
	at java.util.concurrent.FutureTask.run(FutureTask.java:266)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
21 五月 2022 17:08:53,250 WARN  [SinkRunner-PollingRunner-DefaultSinkProcessor] (org.apache.flume.sink.hdfs.HDFSEventSink.process:454)  - HDFS IO error
java.io.IOException: Failed on local exception: org.apache.hadoop.ipc.RpcException: RPC response exceeds maximum data length; Host Details : local host is: "hadoop102/192.168.121.129"; destination host is: "hadoop102":9870; 
```
报错原因：hadooop之间通信端口与flume的 agent对sink的配置端口不符！！

hadoop/etc/hadoop/core.site.xml中

defaultFS端口与sink配置下agent.sink.xx(实例化的sink）.hdfs.path=hdfs://hadoop_node:(deafaultFS）的端口

更改之后，实时监听flume的日志文件，显示如下证明成功！！！！
```
21 五月 2022 17:29:12,727 INFO  [SinkRunner-PollingRunner-DefaultSinkProcessor] (org.apache.flume.sink.hdfs.BucketWriter.open:246)  - Creating hdfs://hadoop102:8020/flume/20220521/17/logs-.1653125352712.tmp
21 五月 2022 17:29:16,467 INFO  [Thread-15] (org.apache.hadoop.hdfs.protocol.datatransfer.sasl.SaslDataTransferClient.checkTrustAndSend:239)  - SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
21 五月 2022 17:30:12,751 INFO  [hdfs-k2-roll-timer-0] (org.apache.flume.sink.hdfs.HDFSEventSink$1.run:393)  - Writer callback called.
21 五月 2022 17:30:12,751 INFO  [hdfs-k2-roll-timer-0] (org.apache.flume.sink.hdfs.BucketWriter.doClose:438)  - Closing hdfs://hadoop102:8020/flume/20220521/17/logs-.1653125352712.tmp
21 五月 2022 17:30:12,771 INFO  [hdfs-k2-call-runner-0] (org.apache.flume.sink.hdfs.BucketWriter$7.call:681)  - Renaming hdfs://hadoop102:8020/flume/20220521/17/logs-.1653125352712.tmp to hdfs://hadoop102:8020/flume/20220521/17/logs-.1653125352712
```