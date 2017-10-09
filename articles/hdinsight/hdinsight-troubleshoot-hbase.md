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
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>使用 Azure HDInsight 為 HBase 進行疑難排解

了解 hello 最常發生的問題和其解析度使用 Apache HBase 裝載 Apache Ambari 中時。

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>如何執行回報多個未指派區域的 hbck 命令

常見的錯誤訊息，您可能會看到當您執行 hello`hbase hbck`命令是 「 多個成為未指派的區域的 hello 鏈結中的漏洞。 」

在 hello HBase 主要 UI，您可以看到 hello 數目不對稱的所有區域的伺服器之間的區域。 然後，您可以執行`hbase hbck`命令 toosee hello 區域鏈結中的漏洞。

漏洞可能被因 hello 離線區域，因此修正 hello 分派第一次。 

toobring hello 後 tooa 正常狀態時，未指派的區域，請完成下列步驟的 hello:

1. 登入 toohello HDInsight HBase 叢集使用 SSH。
2. 與 hello 動物園管理員命令介面中，執行 hello tooconnect`hbase zkcli`命令。
3. 執行 hello`rmr /hbase/regions-in-transition`命令或 hello`rmr /hbase-unsecure/regions-in-transition`命令。
4. 從 hello tooexit`hbase zkcli`殼層，請使用 hello`exit`命令。
5. 開啟 hello Apache Ambari UI，並再重新啟動 hello 主動 HBase 主機服務。
6. 執行 hello`hbase hbck`命令一次 （不含任何選項）。 請檢查所有區域會被都指派這個命令 tooensure hello 輸出。


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>如何修正使用 hbck 命令進行區域指派時發生的逾時問題

### <a name="issue"></a>問題

當您使用 hello 的逾時問題的潛在原因`hbck`命令可能是數個區域處於 「 轉換 」 中的 hello 狀態很長的時間。 您可以為離線 hello HBase 主要 UI 中看到這些區域。 因為嘗試 tootransition 大量的區域，請 HBase 主機可能會逾時，而且是無法 toobring 這些區域恢復上線。

### <a name="resolution-steps"></a>解決步驟

1. 登入 toohello HDInsight HBase 叢集使用 SSH。
2. 與 hello 動物園管理員命令介面中，執行 hello tooconnect`hbase zkcli`命令。
3. 執行 hello`rmr /hbase/regions-in-transition`或 hello`rmr /hbase-unsecure/regions-in-transition`命令。
4. tooexit hello`hbase zkcli`殼層，請使用 hello`exit`命令。
5. 在 hello Ambari UI，重新啟動 hello 主動 HBase 主機服務。
6. 執行 hello`hbase hbck -fixAssignments`命令一次。

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>如何在叢集中強制停用 HDFS 安全模式

### <a name="issue"></a>問題

hello 本機 Hadoop 分散式檔案系統 (HDFS) 陷入 hello HDInsight 叢集上的安全模式。

### <a name="detailed-description"></a>詳細描述

當您執行下列命令 HDFS hello 失敗可能會造成這個錯誤：

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

當您嘗試 toorun hello 命令時，您可能會看到 hello 錯誤看起來像這樣：

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

### <a name="probable-cause"></a>可能的原因

hello HDInsight 叢集已縮小 tooa 很少節點。 hello 節點數目低於或關閉 toohello HDFS 複寫因數。

### <a name="resolution-steps"></a>解決步驟 

1. 取得的 hello HDFS 上 hello HDInsight 叢集，執行下列命令的 hello hello 狀態：

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
2. 您也可以檢查 hello 完整性 hello HDFS 上 hello HDInsight 叢集使用 hello 下列命令：

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

3. 如果您判斷有無遺失、 損毀，或 under-複寫的區塊，或可以略過這些區塊，請執行下列命令 tootake hello 名稱節點移出安全模式的 hello:

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>如何修正與 Apache Phoenix 的 JDBC 或 SQLLine 連線問題

### <a name="resolution-steps"></a>解決步驟

與 Phoenix tooconnect，您必須提供 hello 的作用中的動物園管理員節點的 IP 位址。 請確定該 hello 動物園管理員正在嘗試服務 toowhich sqlline.py tooconnect 已啟動並執行。
1. 登入 toohello HDInsight 叢集使用 SSH。
2. 輸入下列命令的 hello:
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > 您可以從 hello Ambari UI 取得 hello active 動物園管理員節點 hello IP 位址。 跳過**HBase** > **快速連結** > **ZK\* （使用中）** > **動物園管理員資訊**. 

3. 如果 hello sqlline.py 連接 tooPhoenix，並不會逾時，執行的 hello 下列命令 toovalidate hello 可用性和健全狀況 in Phoenix:

   ```apache
           !tables
           !quit
   ```      
4. 如果此命令能夠運作，就表示沒有問題。 hello hello 使用者所提供的 IP 位址可能會不正確。 不過，如果 hello 命令暫停一段時間，則會顯示下列錯誤 hello 繼續 toostep 5。

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. 執行 hello hello 前端節點 (hn0) toodiagnose hello 條件的 hello in Phoenix 系統中的下列命令。目錄的資料表：

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   hello 命令應該會傳回類似 toohello 下列錯誤： 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. 在 hello Ambari UI，完成下列步驟 toorestart hello HMaster 服務動物園管理員的所有節點上的 hello:

    1. 在 hello**摘要**> 一節的 HBase，跳過**HBase** > **主動 HBase Master**。 
    2. 在 hello**元件**區段中，重新啟動 hello HBase 主機服務。
    3. 針對所有其餘的 **Standby HBase Master** 服務，重複這些步驟。 

它可以佔用 toofive hello HBase 主要服務 toostabilize 分鐘的時間，並完成 hello 復原程序。 在幾分鐘之後, 重複 hello sqlline.py 命令 tooconfirm 該 hello 系統。類別目錄的資料表已啟動，且它可以進行查詢。 

當 hello 系統。類別目錄資料表後 toonormal，hello 連線問題 tooPhoenix 應自動解決。


## <a name="what-causes-a-master-server-toofail-toostart"></a>什麼情況會讓主要伺服器 toofail toostart

### <a name="error"></a>錯誤 

發生不可部分完成的重新命名失敗。

### <a name="detailed-description"></a>詳細描述

在 hello 啟動過程中，HMaster 完成許多初始化步驟。 這些活動包括將資料移 (.tmp) 從頭 hello toohello 資料資料夾。 HMaster 也會尋找在 hello 預寫記錄檔 (WALs) 資料夾 toosee 如果沒有任何回應區域的伺服器，依此類推。 

在啟動期間，HMaster 會對這些資料夾執行基本 `list` 命令。 如果任何時間 HMaster 在任一資料夾中看到未預期的檔案，則會擲回例外狀況，而且不會啟動。  

### <a name="probable-cause"></a>可能的原因

Hello 區域伺服器記錄檔、 tooidentify hello 時間表建立 hello 檔案，再試一次，然後查看是否發生周圍 hello 階段 hello 檔案的處理序損毀已建立。 (請連絡 HBase 支援 tooassist 您這項作業。)這可協助我們提供更健全的機制，讓您可以避免發生這個錯誤 (bug)，並確保處理序順利關閉。

### <a name="resolution-steps"></a>解決步驟

檢查 hello 呼叫堆疊，然後再次嘗試的 toodetermine 資料夾可能會造成 hello 問題 （例如，它可能是 hello WALs 資料夾或 hello.tmp 資料夾）。 然後，在 Cloud Explorer 中，或使用 HDFS 命令嘗試 toolocate hello 問題的檔案。 這通常是 \*-renamePending.json 檔案。 (hello \*-renamePending.json 檔案是筆記本檔案中使用過 tooimplement hello 不可部分完成的重新命名作業 hello WASB 驅動程式。 由於 toobugs 在此實作中，這些檔案可以保留一段之後，處理序當機等。)請在 Cloud Explorer 中或使用 HDFS 命令強制刪除此檔案。 

這個位置有時候還可能有名稱類似 *$$$.$$$* 的暫存檔案。 您有 toouse HDFS`ls`指令 toosee 此檔案; 您無法看到在 Cloud Explorer 中的 hello 檔案。 toodelete 這個檔案，使用 hello HDFS 命令`hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`。  

執行這些命令之後，HMaster 應立即啟動。 

### <a name="error"></a>錯誤

區域 xxx 的 *hbase: meta* 中未列出任何伺服器位址。

### <a name="detailed-description"></a>詳細描述

您可能會看到一則訊息，指出該 hello Linux 叢集上*hbase： 中繼*資料表不在線上。 執行 `hbck` 可能會回報「在任何區域上找不到 hbase: meta 資料表 replicaId 0」。 hello 問題可能是 HMaster 無法初始化之後重新啟動 HBase。 Hello HMaster 記錄檔，您可能會看到 hello 訊息: 「 hbase 中列出的任何伺服器位址： 區域 hbase 的中繼： 備份\<地區名稱\>"。  

### <a name="resolution-steps"></a>解決步驟

1. 在 hello HBase 殼層中，輸入下列命令 （使用視需要變更實際值） 的 hello:  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. 刪除 hello *hbase： 命名空間*項目。 此項目可能 hello 相同的錯誤報告時 hello *hbase： 命名空間*資料表掃描。

3. toobring 向上 HBase hello Ambari UI 處於執行狀態，重新啟動 hello Active HMaster 服務。  

4. 在 hello HBase 殼層，toobring 所有離線的資料表，執行下列命令的 hello:

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>其他閱讀資料

[無法 tooprocess hello HBase 資料表](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>錯誤

與嚴重的例外狀況的類似 too"java.io.IOException HMaster 逾時： 等候指定的命名空間資料表 toobe Timedout 300000ms。 」

### <a name="detailed-description"></a>詳細描述

如果您有許多資料表和區域在重新啟動 HMaster 服務時尚未排清，則可能會遇到此問題。 重新啟動可能會失敗，而且您會看到上述錯誤訊息的 hello。  

### <a name="probable-cause"></a>可能的原因

這是 hello HMaster 服務的已知的問題。 一般叢集啟動工作可能需要很長的時間。 HMaster 關閉，因為尚未指派 hello 命名空間資料表。 這只會在存在大量未排清資料的情況下發生，因此五分鐘的逾時並不足夠。
  
### <a name="resolution-steps"></a>解決步驟

1. 在 hello Ambari UI，移過**HBase** > **Configs**。 在 hello 自訂 hbase-site.xml 檔案中，新增 hello 下列設定： 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. 重新啟動所需的 hello 服務 （HMaster，以及可能還有其他 HBase 服務）。  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>什麼情況導致區域伺服器上的重新啟動失敗

### <a name="issue"></a>問題

區域伺服器上的重新啟動失敗可透過遵循最佳做法來加以防止。 我們建議您在規劃 toorestart HBase 區域伺服器時，暫停工作負載過重的活動。 Shutdown 正在進行中時，應用程式就會繼續 tooconnect 與區域的伺服器，如果 hello 區域伺服器重新啟動作業就會變慢幾分鐘的時間。 此外，它是個不錯的主意 toofirst 排清所有 hello 資料表。 如需如何參考 tooflush 資料表，請參閱[HDInsight HBase： 如何 tooimprove hello HBase 叢集重新啟動的時間清除資料表](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/)。

如果起始於 hello Ambari UI HBase 區域伺服器上的 hello 重新啟動作業時，立即看到 hello 區域伺服器已關閉，但是它們立即不要重新啟動。 

以下是發生什麼事幕後 hello: 

1. hello Ambari 代理程式傳送停止要求 toohello 區域伺服器。
2. hello Ambari 代理程式會等候 30 秒的向下 hello 區域伺服器 tooshut 依正常程序。 
3. 如果您的應用程式會繼續與 hello 區域伺服器 tooconnect，hello 伺服器將不會立即關閉。 hello 30 秒逾時過期之前的關機。 
4. 30 秒之後，hello Ambari 代理程式會將強制終止 (`kill -9`) 命令 toohello 區域伺服器。 您可以看到此 hello ambari 代理程式記錄檔 （hello /var/記錄檔目錄中的 hello 個別的背景工作節點） 中：

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
Hello 突然關機，hello 與 hello 程序相關聯的連接埠可能不會釋放，即使 hello 區域伺服器處理序已停止。 這種情況時可能會導致 tooan AddressBindException hello 區域伺服器啟動時，hello 下列記錄檔中所示。 您可以確認這在 hello 區域-server.log hello 背景工作節點出 hello 區域伺服器無法 toostart hello /var/log/hbase 目錄中。 

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

### <a name="resolution-steps"></a>解決步驟

1. 請嘗試 tooreduce hello 負載 hello HBase 區域的伺服器上，才能起始重新啟動。 
2. 或者使用 hello 背景工作節點上的伺服器 hello 之後再試一次 toomanually 重新啟動區域 （如果步驟 1 不會說明），命令：

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

