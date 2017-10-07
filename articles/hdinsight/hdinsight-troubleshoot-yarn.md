---
title: "使用 Azure HDInsight aaaTroubleshoot YARN |Microsoft 文件"
description: "取得解答 toocommon 疑問 Apache Hadoop YARN 與 Azure HDInsight 工作。"
keywords: "Azure HDInsight, YARN, 常見問題集, 疑難排解指南, 常見問題"
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>使用 Azure HDInsight 進行 YARN 的疑難排解

了解 hello 最常發生的問題和其解析度使用 Apache Hadoop YARN 裝載 Apache Ambari 中時。

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>如何在叢集上建立新的 YARN 佇列


### <a name="resolution-steps"></a>解決步驟 

使用 hello 以下步驟 Ambari toocreate 新 YARN 佇列，並接著平衡所有 hello 佇列之間的 hello 容量配置。 

在此範例中，兩個現有的佇列 (**預設**和**thriftsvr**) 都從 50%容量 too25%容量，讓新佇列 (的 spark) 50%容量 hello 變更。
| 佇列 | 容量 | 最大容量 |
| --- | --- | --- | --- |
| 預設值 | 25% | 50% |
| thrftsvr | 25% | 50% |
| spark | 50% | 50% |

1. 選取 hello **Ambari 檢視**圖示，並選取 hello 方格模式。 接著，選取 [YARN 佇列管理員]。

    ![選取 hello Ambari 檢視圖示](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. 選取 hello**預設**佇列。

    ![選取 hello 預設佇列](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Hello**預設**排入佇列，變更 hello**容量**從 50%too25%。 Hello **thriftsvr**排入佇列，變更 hello**容量**too25%。

    ![變更 hello 容量 too25 %hello 預設和 thriftsvr 佇列](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. toocreate 新佇列中，選取**加入佇列**。

    ![選取 [新增佇列]](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. Hello 新佇列名稱。

    ![名稱 hello 佇列 Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. 保留 hello**容量**值 50%，然後選取 hello**動作** 按鈕。

    ![選取 hello 動作按鈕](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. 選取 [Save and Refresh Queues] \(儲存並重新整理佇列)。

    ![選取 [Save and Refresh Queues] \(儲存並重新整理佇列)。](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

這些變更會立即在 hello YARN 排程器 UI 上顯示項目。

### <a name="additional-reading"></a>其他閱讀資料

- [YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>如何下載叢集的 YARN 記錄


### <a name="resolution-steps"></a>解決步驟 

1. 使用安全殼層 (SSH) 用戶端連接 toohello HDInsight 叢集。 如需詳細資訊，請參閱[其他閱讀資料](#additional-reading-2)。

2. toolist 所有 hello 應用程式識別碼 hello YARN 應用程式目前正在執行，執行下列命令的 hello:

    ```apache
    yarn top
    ```
    hello 識別碼會列在 hello **APPLICATIONID**資料行。 您可以下載記錄檔從 hello **APPLICATIONID**資料行。

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. toodownload YARN 容器記錄檔中的所有應用程式主機，請使用下列命令的 hello:
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    此命令會建立名為 amlogs.txt 的記錄檔。 

4. toodownload YARN 容器記錄檔中的唯一的 hello 最新的應用程式主機，使用下列命令的 hello:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    此命令會建立名為 latestamlogs.txt 的記錄檔。 

4. toodownload YARN 容器記錄檔中的第一個兩個應用程式主機 hello，請使用下列命令的 hello:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    此命令會建立名為 first2amlogs.txt 的記錄檔。 

5. 所有的 YARN 容器記錄檔，會使用 toodownload hello 下列命令：

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    此命令會建立名為 logs.txt 的記錄檔。 

6. toodownload hello YARN 容器記錄檔以取得特定的容器，使用 hello 下列命令：

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    此命令會建立名為 containerlogs.txt 的記錄檔。

### <a name="additional-reading-2"></a>其他閱讀資料

- [透過 SSH 連線 tooHDInsight (Hadoop)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [Apache Hadoop YARN 概念與應用程式](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







