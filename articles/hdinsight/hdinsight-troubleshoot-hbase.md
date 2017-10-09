---
title: "使用 Azure HDInsight aaaTroubleshoot HBase |Microsoft 文件"
description: "取得解答 toocommon 疑問 HBase 與 Azure HDInsight 工作。"
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="763b1-103">使用 Azure HDInsight 為 HBase 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="763b1-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="763b1-104">了解 hello 最常發生的問題和其解析度使用 Apache HBase 裝載 Apache Ambari 中時。</span><span class="sxs-lookup"><span data-stu-id="763b1-104">Learn about hello top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="763b1-105">如何執行回報多個未指派區域的 hbck 命令</span><span class="sxs-lookup"><span data-stu-id="763b1-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="763b1-106">常見的錯誤訊息，您可能會看到當您執行 hello`hbase hbck`命令是 「 多個成為未指派的區域的 hello 鏈結中的漏洞。 」</span><span class="sxs-lookup"><span data-stu-id="763b1-106">A common error message that you might see when you run hello `hbase hbck` command is "multiple regions being unassigned or holes in hello chain of regions."</span></span>

<span data-ttu-id="763b1-107">在 hello HBase 主要 UI，您可以看到 hello 數目不對稱的所有區域的伺服器之間的區域。</span><span class="sxs-lookup"><span data-stu-id="763b1-107">In hello HBase Master UI, you can see hello number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="763b1-108">然後，您可以執行`hbase hbck`命令 toosee hello 區域鏈結中的漏洞。</span><span class="sxs-lookup"><span data-stu-id="763b1-108">Then, you can run `hbase hbck` command toosee holes in hello region chain.</span></span>

<span data-ttu-id="763b1-109">漏洞可能被因 hello 離線區域，因此修正 hello 分派第一次。</span><span class="sxs-lookup"><span data-stu-id="763b1-109">Holes might be caused by hello offline regions, so fix hello assignments first.</span></span> 

<span data-ttu-id="763b1-110">toobring hello 後 tooa 正常狀態時，未指派的區域，請完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="763b1-110">toobring hello unassigned regions back tooa normal state, complete hello following steps:</span></span>

1. <span data-ttu-id="763b1-111">登入 toohello HDInsight HBase 叢集使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="763b1-111">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="763b1-112">與 hello 動物園管理員命令介面中，執行 hello tooconnect`hbase zkcli`命令。</span><span class="sxs-lookup"><span data-stu-id="763b1-112">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="763b1-113">執行 hello`rmr /hbase/regions-in-transition`命令或 hello`rmr /hbase-unsecure/regions-in-transition`命令。</span><span class="sxs-lookup"><span data-stu-id="763b1-113">Run hello `rmr /hbase/regions-in-transition` command or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="763b1-114">從 hello tooexit`hbase zkcli`殼層，請使用 hello`exit`命令。</span><span class="sxs-lookup"><span data-stu-id="763b1-114">tooexit from hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="763b1-115">開啟 hello Apache Ambari UI，並再重新啟動 hello 主動 HBase 主機服務。</span><span class="sxs-lookup"><span data-stu-id="763b1-115">Open hello Apache Ambari UI, and then restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="763b1-116">執行 hello`hbase hbck`命令一次 （不含任何選項）。</span><span class="sxs-lookup"><span data-stu-id="763b1-116">Run hello `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="763b1-117">請檢查所有區域會被都指派這個命令 tooensure hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="763b1-117">Check hello output of this command tooensure that all regions are being assigned.</span></span>


## <span data-ttu-id="763b1-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>如何修正使用 hbck 命令進行區域指派時發生的逾時問題</span><span class="sxs-lookup"><span data-stu-id="763b1-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="763b1-119">問題</span><span class="sxs-lookup"><span data-stu-id="763b1-119">Issue</span></span>

<span data-ttu-id="763b1-120">當您使用 hello 的逾時問題的潛在原因`hbck`命令可能是數個區域處於 「 轉換 」 中的 hello 狀態很長的時間。</span><span class="sxs-lookup"><span data-stu-id="763b1-120">A potential cause for timeout issues when you use hello `hbck` command might be that several regions are in hello "in transition" state for a long time.</span></span> <span data-ttu-id="763b1-121">您可以為離線 hello HBase 主要 UI 中看到這些區域。</span><span class="sxs-lookup"><span data-stu-id="763b1-121">You can see those regions as offline in hello HBase Master UI.</span></span> <span data-ttu-id="763b1-122">因為嘗試 tootransition 大量的區域，請 HBase 主機可能會逾時，而且是無法 toobring 這些區域恢復上線。</span><span class="sxs-lookup"><span data-stu-id="763b1-122">Because a high number of regions are attempting tootransition, HBase Master might timeout and be unable toobring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="763b1-123">解決步驟</span><span class="sxs-lookup"><span data-stu-id="763b1-123">Resolution steps</span></span>

1. <span data-ttu-id="763b1-124">登入 toohello HDInsight HBase 叢集使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="763b1-124">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="763b1-125">與 hello 動物園管理員命令介面中，執行 hello tooconnect`hbase zkcli`命令。</span><span class="sxs-lookup"><span data-stu-id="763b1-125">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="763b1-126">執行 hello`rmr /hbase/regions-in-transition`或 hello`rmr /hbase-unsecure/regions-in-transition`命令。</span><span class="sxs-lookup"><span data-stu-id="763b1-126">Run hello `rmr /hbase/regions-in-transition` or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="763b1-127">tooexit hello`hbase zkcli`殼層，請使用 hello`exit`命令。</span><span class="sxs-lookup"><span data-stu-id="763b1-127">tooexit hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="763b1-128">在 hello Ambari UI，重新啟動 hello 主動 HBase 主機服務。</span><span class="sxs-lookup"><span data-stu-id="763b1-128">In hello Ambari UI, restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="763b1-129">執行 hello`hbase hbck -fixAssignments`命令一次。</span><span class="sxs-lookup"><span data-stu-id="763b1-129">Run hello `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="763b1-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>如何在叢集中強制停用 HDFS 安全模式</span><span class="sxs-lookup"><span data-stu-id="763b1-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="763b1-131">問題</span><span class="sxs-lookup"><span data-stu-id="763b1-131">Issue</span></span>

<span data-ttu-id="763b1-132">hello 本機 Hadoop 分散式檔案系統 (HDFS) 陷入 hello HDInsight 叢集上的安全模式。</span><span class="sxs-lookup"><span data-stu-id="763b1-132">hello local Hadoop Distributed File System (HDFS) is stuck in safe mode on hello HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="763b1-133">詳細描述</span><span class="sxs-lookup"><span data-stu-id="763b1-133">Detailed description</span></span>

<span data-ttu-id="763b1-134">當您執行下列命令 HDFS hello 失敗可能會造成這個錯誤：</span><span class="sxs-lookup"><span data-stu-id="763b1-134">This error might be caused by a failure when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="763b1-135">當您嘗試 toorun hello 命令時，您可能會看到 hello 錯誤看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="763b1-135">hello error you might see when you try toorun hello command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="763b1-136">可能的原因</span><span class="sxs-lookup"><span data-stu-id="763b1-136">Probable cause</span></span>

<span data-ttu-id="763b1-137">hello HDInsight 叢集已縮小 tooa 很少節點。</span><span class="sxs-lookup"><span data-stu-id="763b1-137">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="763b1-138">hello 節點數目低於或關閉 toohello HDFS 複寫因數。</span><span class="sxs-lookup"><span data-stu-id="763b1-138">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="763b1-139">解決步驟</span><span class="sxs-lookup"><span data-stu-id="763b1-139">Resolution steps</span></span> 

1. <span data-ttu-id="763b1-140">取得的 hello HDFS 上 hello HDInsight 叢集，執行下列命令的 hello hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="763b1-140">Get hello status of hello HDFS on hello HDInsight cluster by running hello following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="763b1-141">您也可以檢查 hello 完整性 hello HDFS 上 hello HDInsight 叢集使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="763b1-141">You also can check hello integrity of hello HDFS on hello HDInsight cluster by using hello following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   hello filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="763b1-142">如果您判斷有無遺失、 損毀，或 under-複寫的區塊，或可以略過這些區塊，請執行下列命令 tootake hello 名稱節點移出安全模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="763b1-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="763b1-143">如何修正與 Apache Phoenix 的 JDBC 或 SQLLine 連線問題</span><span class="sxs-lookup"><span data-stu-id="763b1-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="763b1-144">解決步驟</span><span class="sxs-lookup"><span data-stu-id="763b1-144">Resolution steps</span></span>

<span data-ttu-id="763b1-145">與 Phoenix tooconnect，您必須提供 hello 的作用中的動物園管理員節點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="763b1-145">tooconnect with Phoenix, you must provide hello IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="763b1-146">請確定該 hello 動物園管理員正在嘗試服務 toowhich sqlline.py tooconnect 已啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="763b1-146">Ensure that hello ZooKeeper service toowhich sqlline.py is trying tooconnect is up and running.</span></span>
1. <span data-ttu-id="763b1-147">登入 toohello HDInsight 叢集使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="763b1-147">Sign in toohello HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="763b1-148">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="763b1-148">Enter hello following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="763b1-149">您可以從 hello Ambari UI 取得 hello active 動物園管理員節點 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="763b1-149">You can get hello IP address of hello active ZooKeeper node from hello Ambari UI.</span></span> <span data-ttu-id="763b1-150">跳過**HBase** > **快速連結** > **ZK\* （使用中）** > **動物園管理員資訊**.</span><span class="sxs-lookup"><span data-stu-id="763b1-150">Go too**HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="763b1-151">如果 hello sqlline.py 連接 tooPhoenix，並不會逾時，執行的 hello 下列命令 toovalidate hello 可用性和健全狀況 in Phoenix:</span><span class="sxs-lookup"><span data-stu-id="763b1-151">If hello sqlline.py connects tooPhoenix and does not timeout, run hello following command toovalidate hello availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="763b1-152">如果此命令能夠運作，就表示沒有問題。</span><span class="sxs-lookup"><span data-stu-id="763b1-152">If this command works, there is no issue.</span></span> <span data-ttu-id="763b1-153">hello hello 使用者所提供的 IP 位址可能會不正確。</span><span class="sxs-lookup"><span data-stu-id="763b1-153">hello IP address provided by hello user might be incorrect.</span></span> <span data-ttu-id="763b1-154">不過，如果 hello 命令暫停一段時間，則會顯示下列錯誤 hello 繼續 toostep 5。</span><span class="sxs-lookup"><span data-stu-id="763b1-154">However, if hello command pauses for an extended time and then displays hello following error, continue toostep 5.</span></span>

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="763b1-155">執行 hello hello 前端節點 (hn0) toodiagnose hello 條件的 hello in Phoenix 系統中的下列命令。目錄的資料表：</span><span class="sxs-lookup"><span data-stu-id="763b1-155">Run hello following commands from hello head node (hn0) toodiagnose hello condition of hello Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="763b1-156">hello 命令應該會傳回類似 toohello 下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="763b1-156">hello command should return an error similar toohello following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="763b1-157">在 hello Ambari UI，完成下列步驟 toorestart hello HMaster 服務動物園管理員的所有節點上的 hello:</span><span class="sxs-lookup"><span data-stu-id="763b1-157">In hello Ambari UI, complete hello following steps toorestart hello HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="763b1-158">在 hello**摘要**> 一節的 HBase，跳過**HBase** > **主動 HBase Master**。</span><span class="sxs-lookup"><span data-stu-id="763b1-158">In hello **Summary** section of HBase, go too**HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="763b1-159">在 hello**元件**區段中，重新啟動 hello HBase 主機服務。</span><span class="sxs-lookup"><span data-stu-id="763b1-159">In hello **Components** section, restart hello HBase Master service.</span></span>
    3. <span data-ttu-id="763b1-160">針對所有其餘的 **Standby HBase Master** 服務，重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="763b1-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="763b1-161">它可以佔用 toofive hello HBase 主要服務 toostabilize 分鐘的時間，並完成 hello 復原程序。</span><span class="sxs-lookup"><span data-stu-id="763b1-161">It can take up toofive minutes for hello HBase Master service toostabilize and finish hello recovery process.</span></span> <span data-ttu-id="763b1-162">在幾分鐘之後, 重複 hello sqlline.py 命令 tooconfirm 該 hello 系統。類別目錄的資料表已啟動，且它可以進行查詢。</span><span class="sxs-lookup"><span data-stu-id="763b1-162">After a few minutes, repeat hello sqlline.py commands tooconfirm that hello SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="763b1-163">當 hello 系統。類別目錄資料表後 toonormal，hello 連線問題 tooPhoenix 應自動解決。</span><span class="sxs-lookup"><span data-stu-id="763b1-163">When hello SYSTEM.CATALOG table is back toonormal, hello connectivity issue tooPhoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-toofail-toostart"></a><span data-ttu-id="763b1-164">什麼情況會讓主要伺服器 toofail toostart</span><span class="sxs-lookup"><span data-stu-id="763b1-164">What causes a master server toofail toostart</span></span>

### <a name="error"></a><span data-ttu-id="763b1-165">錯誤</span><span class="sxs-lookup"><span data-stu-id="763b1-165">Error</span></span> 

<span data-ttu-id="763b1-166">發生不可部分完成的重新命名失敗。</span><span class="sxs-lookup"><span data-stu-id="763b1-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="763b1-167">詳細描述</span><span class="sxs-lookup"><span data-stu-id="763b1-167">Detailed description</span></span>

<span data-ttu-id="763b1-168">在 hello 啟動過程中，HMaster 完成許多初始化步驟。</span><span class="sxs-lookup"><span data-stu-id="763b1-168">During hello startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="763b1-169">這些活動包括將資料移 (.tmp) 從頭 hello toohello 資料資料夾。</span><span class="sxs-lookup"><span data-stu-id="763b1-169">These include moving data from hello scratch (.tmp) folder toohello data folder.</span></span> <span data-ttu-id="763b1-170">HMaster 也會尋找在 hello 預寫記錄檔 (WALs) 資料夾 toosee 如果沒有任何回應區域的伺服器，依此類推。</span><span class="sxs-lookup"><span data-stu-id="763b1-170">HMaster also looks at hello write-ahead logs (WALs) folder toosee if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="763b1-171">在啟動期間，HMaster 會對這些資料夾執行基本 `list` 命令。</span><span class="sxs-lookup"><span data-stu-id="763b1-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="763b1-172">如果任何時間 HMaster 在任一資料夾中看到未預期的檔案，則會擲回例外狀況，而且不會啟動。</span><span class="sxs-lookup"><span data-stu-id="763b1-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="763b1-173">可能的原因</span><span class="sxs-lookup"><span data-stu-id="763b1-173">Probable cause</span></span>

<span data-ttu-id="763b1-174">Hello 區域伺服器記錄檔、 tooidentify hello 時間表建立 hello 檔案，再試一次，然後查看是否發生周圍 hello 階段 hello 檔案的處理序損毀已建立。</span><span class="sxs-lookup"><span data-stu-id="763b1-174">In hello region server logs, try tooidentify hello timeline of hello file creation, and then see if there was a process crash around hello time hello file was created.</span></span> <span data-ttu-id="763b1-175">(請連絡 HBase 支援 tooassist 您這項作業。)這可協助我們提供更健全的機制，讓您可以避免發生這個錯誤 (bug)，並確保處理序順利關閉。</span><span class="sxs-lookup"><span data-stu-id="763b1-175">(Contact HBase support tooassist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="763b1-176">解決步驟</span><span class="sxs-lookup"><span data-stu-id="763b1-176">Resolution steps</span></span>

<span data-ttu-id="763b1-177">檢查 hello 呼叫堆疊，然後再次嘗試的 toodetermine 資料夾可能會造成 hello 問題 （例如，它可能是 hello WALs 資料夾或 hello.tmp 資料夾）。</span><span class="sxs-lookup"><span data-stu-id="763b1-177">Check hello call stack and try toodetermine which folder might be causing hello problem (for instance, it might be hello WALs folder or hello .tmp folder).</span></span> <span data-ttu-id="763b1-178">然後，在 Cloud Explorer 中，或使用 HDFS 命令嘗試 toolocate hello 問題的檔案。</span><span class="sxs-lookup"><span data-stu-id="763b1-178">Then, in Cloud Explorer or by using HDFS commands, try toolocate hello problem file.</span></span> <span data-ttu-id="763b1-179">這通常是 \*-renamePending.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="763b1-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="763b1-180">(hello \*-renamePending.json 檔案是筆記本檔案中使用過 tooimplement hello 不可部分完成的重新命名作業 hello WASB 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="763b1-180">(hello \*-renamePending.json file is a journal file that's used tooimplement hello atomic rename operation in hello WASB driver.</span></span> <span data-ttu-id="763b1-181">由於 toobugs 在此實作中，這些檔案可以保留一段之後，處理序當機等。)請在 Cloud Explorer 中或使用 HDFS 命令強制刪除此檔案。</span><span class="sxs-lookup"><span data-stu-id="763b1-181">Due toobugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="763b1-182">這個位置有時候還可能有名稱類似 *$$$.$$$* 的暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="763b1-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="763b1-183">您有 toouse HDFS`ls`指令 toosee 此檔案; 您無法看到在 Cloud Explorer 中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="763b1-183">You have toouse HDFS `ls` command toosee this file; you cannot see hello file in Cloud Explorer.</span></span> <span data-ttu-id="763b1-184">toodelete 這個檔案，使用 hello HDFS 命令`hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`。</span><span class="sxs-lookup"><span data-stu-id="763b1-184">toodelete this file, use hello HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="763b1-185">執行這些命令之後，HMaster 應立即啟動。</span><span class="sxs-lookup"><span data-stu-id="763b1-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="763b1-186">錯誤</span><span class="sxs-lookup"><span data-stu-id="763b1-186">Error</span></span>

<span data-ttu-id="763b1-187">區域 xxx 的 *hbase: meta* 中未列出任何伺服器位址。</span><span class="sxs-lookup"><span data-stu-id="763b1-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="763b1-188">詳細描述</span><span class="sxs-lookup"><span data-stu-id="763b1-188">Detailed description</span></span>

<span data-ttu-id="763b1-189">您可能會看到一則訊息，指出該 hello Linux 叢集上*hbase： 中繼*資料表不在線上。</span><span class="sxs-lookup"><span data-stu-id="763b1-189">You might see a message on your Linux cluster that indicates that hello *hbase: meta* table is not online.</span></span> <span data-ttu-id="763b1-190">執行 `hbck` 可能會回報「在任何區域上找不到 hbase: meta 資料表 replicaId 0」。</span><span class="sxs-lookup"><span data-stu-id="763b1-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="763b1-191">hello 問題可能是 HMaster 無法初始化之後重新啟動 HBase。</span><span class="sxs-lookup"><span data-stu-id="763b1-191">hello problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="763b1-192">Hello HMaster 記錄檔，您可能會看到 hello 訊息: 「 hbase 中列出的任何伺服器位址： 區域 hbase 的中繼： 備份\<地區名稱\>"。</span><span class="sxs-lookup"><span data-stu-id="763b1-192">In hello HMaster logs, you might see hello message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="763b1-193">解決步驟</span><span class="sxs-lookup"><span data-stu-id="763b1-193">Resolution steps</span></span>

1. <span data-ttu-id="763b1-194">在 hello HBase 殼層中，輸入下列命令 （使用視需要變更實際值） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="763b1-194">In hello HBase shell, enter hello following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="763b1-195">刪除 hello *hbase： 命名空間*項目。</span><span class="sxs-lookup"><span data-stu-id="763b1-195">Delete hello *hbase: namespace* entry.</span></span> <span data-ttu-id="763b1-196">此項目可能 hello 相同的錯誤報告時 hello *hbase： 命名空間*資料表掃描。</span><span class="sxs-lookup"><span data-stu-id="763b1-196">This entry might be hello same error that's being reported when hello *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="763b1-197">toobring 向上 HBase hello Ambari UI 處於執行狀態，重新啟動 hello Active HMaster 服務。</span><span class="sxs-lookup"><span data-stu-id="763b1-197">toobring up HBase in a running state, in hello Ambari UI, restart hello Active HMaster service.</span></span>  

4. <span data-ttu-id="763b1-198">在 hello HBase 殼層，toobring 所有離線的資料表，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="763b1-198">In hello HBase shell, toobring up all offline tables, run hello following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="763b1-199">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="763b1-199">Additional reading</span></span>

[<span data-ttu-id="763b1-200">無法 tooprocess hello HBase 資料表</span><span class="sxs-lookup"><span data-stu-id="763b1-200">Unable tooprocess hello HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="763b1-201">錯誤</span><span class="sxs-lookup"><span data-stu-id="763b1-201">Error</span></span>

<span data-ttu-id="763b1-202">與嚴重的例外狀況的類似 too"java.io.IOException HMaster 逾時： 等候指定的命名空間資料表 toobe Timedout 300000ms。 」</span><span class="sxs-lookup"><span data-stu-id="763b1-202">HMaster times out with a fatal exception similar too"java.io.IOException: Timedout 300000ms waiting for namespace table toobe assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="763b1-203">詳細描述</span><span class="sxs-lookup"><span data-stu-id="763b1-203">Detailed description</span></span>

<span data-ttu-id="763b1-204">如果您有許多資料表和區域在重新啟動 HMaster 服務時尚未排清，則可能會遇到此問題。</span><span class="sxs-lookup"><span data-stu-id="763b1-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="763b1-205">重新啟動可能會失敗，而且您會看到上述錯誤訊息的 hello。</span><span class="sxs-lookup"><span data-stu-id="763b1-205">Restart might fail, and you'll see hello preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="763b1-206">可能的原因</span><span class="sxs-lookup"><span data-stu-id="763b1-206">Probable cause</span></span>

<span data-ttu-id="763b1-207">這是 hello HMaster 服務的已知的問題。</span><span class="sxs-lookup"><span data-stu-id="763b1-207">This is a known issue with hello HMaster service.</span></span> <span data-ttu-id="763b1-208">一般叢集啟動工作可能需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="763b1-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="763b1-209">HMaster 關閉，因為尚未指派 hello 命名空間資料表。</span><span class="sxs-lookup"><span data-stu-id="763b1-209">HMaster shuts down because hello namespace table isn’t yet assigned.</span></span> <span data-ttu-id="763b1-210">這只會在存在大量未排清資料的情況下發生，因此五分鐘的逾時並不足夠。</span><span class="sxs-lookup"><span data-stu-id="763b1-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="763b1-211">解決步驟</span><span class="sxs-lookup"><span data-stu-id="763b1-211">Resolution steps</span></span>

1. <span data-ttu-id="763b1-212">在 hello Ambari UI，移過**HBase** > **Configs**。</span><span class="sxs-lookup"><span data-stu-id="763b1-212">In hello Ambari UI, go too**HBase** > **Configs**.</span></span> <span data-ttu-id="763b1-213">在 hello 自訂 hbase-site.xml 檔案中，新增 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="763b1-213">In hello custom hbase-site.xml file, add hello following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="763b1-214">重新啟動所需的 hello 服務 （HMaster，以及可能還有其他 HBase 服務）。</span><span class="sxs-lookup"><span data-stu-id="763b1-214">Restart hello required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="763b1-215">什麼情況導致區域伺服器上的重新啟動失敗</span><span class="sxs-lookup"><span data-stu-id="763b1-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="763b1-216">問題</span><span class="sxs-lookup"><span data-stu-id="763b1-216">Issue</span></span>

<span data-ttu-id="763b1-217">區域伺服器上的重新啟動失敗可透過遵循最佳做法來加以防止。</span><span class="sxs-lookup"><span data-stu-id="763b1-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="763b1-218">我們建議您在規劃 toorestart HBase 區域伺服器時，暫停工作負載過重的活動。</span><span class="sxs-lookup"><span data-stu-id="763b1-218">We recommend that you pause heavy workload activity when you are planning toorestart HBase region servers.</span></span> <span data-ttu-id="763b1-219">Shutdown 正在進行中時，應用程式就會繼續 tooconnect 與區域的伺服器，如果 hello 區域伺服器重新啟動作業就會變慢幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="763b1-219">If an application continues tooconnect with region servers when shutdown is in progress, hello region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="763b1-220">此外，它是個不錯的主意 toofirst 排清所有 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="763b1-220">Also, it's a good idea toofirst flush all hello tables.</span></span> <span data-ttu-id="763b1-221">如需如何參考 tooflush 資料表，請參閱[HDInsight HBase： 如何 tooimprove hello HBase 叢集重新啟動的時間清除資料表](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/)。</span><span class="sxs-lookup"><span data-stu-id="763b1-221">For a reference on how tooflush tables, see [HDInsight HBase: How tooimprove hello HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="763b1-222">如果起始於 hello Ambari UI HBase 區域伺服器上的 hello 重新啟動作業時，立即看到 hello 區域伺服器已關閉，但是它們立即不要重新啟動。</span><span class="sxs-lookup"><span data-stu-id="763b1-222">If you initiate hello restart operation on HBase region servers from hello Ambari UI, you immediately see that hello region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="763b1-223">以下是發生什麼事幕後 hello:</span><span class="sxs-lookup"><span data-stu-id="763b1-223">Here's what's happening behind hello scenes:</span></span> 

1. <span data-ttu-id="763b1-224">hello Ambari 代理程式傳送停止要求 toohello 區域伺服器。</span><span class="sxs-lookup"><span data-stu-id="763b1-224">hello Ambari agent sends a stop request toohello region server.</span></span>
2. <span data-ttu-id="763b1-225">hello Ambari 代理程式會等候 30 秒的向下 hello 區域伺服器 tooshut 依正常程序。</span><span class="sxs-lookup"><span data-stu-id="763b1-225">hello Ambari agent waits for 30 seconds for hello region server tooshut down gracefully.</span></span> 
3. <span data-ttu-id="763b1-226">如果您的應用程式會繼續與 hello 區域伺服器 tooconnect，hello 伺服器將不會立即關閉。</span><span class="sxs-lookup"><span data-stu-id="763b1-226">If your application continues tooconnect with hello region server, hello server won't shut down immediately.</span></span> <span data-ttu-id="763b1-227">hello 30 秒逾時過期之前的關機。</span><span class="sxs-lookup"><span data-stu-id="763b1-227">hello 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="763b1-228">30 秒之後，hello Ambari 代理程式會將強制終止 (`kill -9`) 命令 toohello 區域伺服器。</span><span class="sxs-lookup"><span data-stu-id="763b1-228">After 30 seconds, hello Ambari agent sends a force-kill (`kill -9`) command toohello region server.</span></span> <span data-ttu-id="763b1-229">您可以看到此 hello ambari 代理程式記錄檔 （hello /var/記錄檔目錄中的 hello 個別的背景工作節點） 中：</span><span class="sxs-lookup"><span data-stu-id="763b1-229">You can see this in hello ambari-agent log (in hello /var/log/ directory of hello respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="763b1-230">Hello 突然關機，hello 與 hello 程序相關聯的連接埠可能不會釋放，即使 hello 區域伺服器處理序已停止。</span><span class="sxs-lookup"><span data-stu-id="763b1-230">Because of hello abrupt shutdown, hello port associated with hello process might not be released, even though hello region server process is stopped.</span></span> <span data-ttu-id="763b1-231">這種情況時可能會導致 tooan AddressBindException hello 區域伺服器啟動時，hello 下列記錄檔中所示。</span><span class="sxs-lookup"><span data-stu-id="763b1-231">This situation can lead tooan AddressBindException when hello region server is starting, as shown in hello following logs.</span></span> <span data-ttu-id="763b1-232">您可以確認這在 hello 區域-server.log hello 背景工作節點出 hello 區域伺服器無法 toostart hello /var/log/hbase 目錄中。</span><span class="sxs-lookup"><span data-stu-id="763b1-232">You can verify this in hello region-server.log in hello /var/log/hbase directory on hello worker nodes where hello region server fails toostart.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="763b1-233">解決步驟</span><span class="sxs-lookup"><span data-stu-id="763b1-233">Resolution steps</span></span>

1. <span data-ttu-id="763b1-234">請嘗試 tooreduce hello 負載 hello HBase 區域的伺服器上，才能起始重新啟動。</span><span class="sxs-lookup"><span data-stu-id="763b1-234">Try tooreduce hello load on hello HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="763b1-235">或者使用 hello 背景工作節點上的伺服器 hello 之後再試一次 toomanually 重新啟動區域 （如果步驟 1 不會說明），命令：</span><span class="sxs-lookup"><span data-stu-id="763b1-235">Alternatively (if step 1 doesn't help), try toomanually restart region servers on hello worker nodes by using hello following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

