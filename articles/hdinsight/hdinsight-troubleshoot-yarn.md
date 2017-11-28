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
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a><span data-ttu-id="13b80-104">使用 Azure HDInsight 進行 YARN 的疑難排解</span><span class="sxs-lookup"><span data-stu-id="13b80-104">Troubleshoot YARN by using Azure HDInsight</span></span>

<span data-ttu-id="13b80-105">了解 hello 最常發生的問題和其解析度使用 Apache Hadoop YARN 裝載 Apache Ambari 中時。</span><span class="sxs-lookup"><span data-stu-id="13b80-105">Learn about hello top issues and their resolutions when working with Apache Hadoop YARN payloads in Apache Ambari.</span></span>

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a><span data-ttu-id="13b80-106">如何在叢集上建立新的 YARN 佇列</span><span class="sxs-lookup"><span data-stu-id="13b80-106">How do I create a new YARN queue on a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="13b80-107">解決步驟</span><span class="sxs-lookup"><span data-stu-id="13b80-107">Resolution steps</span></span> 

<span data-ttu-id="13b80-108">使用 hello 以下步驟 Ambari toocreate 新 YARN 佇列，並接著平衡所有 hello 佇列之間的 hello 容量配置。</span><span class="sxs-lookup"><span data-stu-id="13b80-108">Use hello following steps in Ambari toocreate a new YARN queue, and then balance hello capacity allocation among all hello queues.</span></span> 

<span data-ttu-id="13b80-109">在此範例中，兩個現有的佇列 (**預設**和**thriftsvr**) 都從 50%容量 too25%容量，讓新佇列 (的 spark) 50%容量 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="13b80-109">In this example, two existing queues (**default** and **thriftsvr**) both are changed from 50% capacity too25% capacity, which gives hello new queue (spark) 50% capacity.</span></span>
| <span data-ttu-id="13b80-110">佇列</span><span class="sxs-lookup"><span data-stu-id="13b80-110">Queue</span></span> | <span data-ttu-id="13b80-111">容量</span><span class="sxs-lookup"><span data-stu-id="13b80-111">Capacity</span></span> | <span data-ttu-id="13b80-112">最大容量</span><span class="sxs-lookup"><span data-stu-id="13b80-112">Maximum capacity</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="13b80-113">預設值</span><span class="sxs-lookup"><span data-stu-id="13b80-113">default</span></span> | <span data-ttu-id="13b80-114">25%</span><span class="sxs-lookup"><span data-stu-id="13b80-114">25%</span></span> | <span data-ttu-id="13b80-115">50%</span><span class="sxs-lookup"><span data-stu-id="13b80-115">50%</span></span> |
| <span data-ttu-id="13b80-116">thrftsvr</span><span class="sxs-lookup"><span data-stu-id="13b80-116">thrftsvr</span></span> | <span data-ttu-id="13b80-117">25%</span><span class="sxs-lookup"><span data-stu-id="13b80-117">25%</span></span> | <span data-ttu-id="13b80-118">50%</span><span class="sxs-lookup"><span data-stu-id="13b80-118">50%</span></span> |
| <span data-ttu-id="13b80-119">spark</span><span class="sxs-lookup"><span data-stu-id="13b80-119">spark</span></span> | <span data-ttu-id="13b80-120">50%</span><span class="sxs-lookup"><span data-stu-id="13b80-120">50%</span></span> | <span data-ttu-id="13b80-121">50%</span><span class="sxs-lookup"><span data-stu-id="13b80-121">50%</span></span> |

1. <span data-ttu-id="13b80-122">選取 hello **Ambari 檢視**圖示，並選取 hello 方格模式。</span><span class="sxs-lookup"><span data-stu-id="13b80-122">Select hello **Ambari Views** icon, and then select hello grid pattern.</span></span> <span data-ttu-id="13b80-123">接著，選取 [YARN 佇列管理員]。</span><span class="sxs-lookup"><span data-stu-id="13b80-123">Next, select **YARN Queue Manager**.</span></span>

    ![選取 hello Ambari 檢視圖示](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. <span data-ttu-id="13b80-125">選取 hello**預設**佇列。</span><span class="sxs-lookup"><span data-stu-id="13b80-125">Select hello **default** queue.</span></span>

    ![選取 hello 預設佇列](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. <span data-ttu-id="13b80-127">Hello**預設**排入佇列，變更 hello**容量**從 50%too25%。</span><span class="sxs-lookup"><span data-stu-id="13b80-127">For hello **default** queue, change hello **capacity** from 50% too25%.</span></span> <span data-ttu-id="13b80-128">Hello **thriftsvr**排入佇列，變更 hello**容量**too25%。</span><span class="sxs-lookup"><span data-stu-id="13b80-128">For hello **thriftsvr** queue, change hello **capacity** too25%.</span></span>

    ![變更 hello 容量 too25 %hello 預設和 thriftsvr 佇列](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. <span data-ttu-id="13b80-130">toocreate 新佇列中，選取**加入佇列**。</span><span class="sxs-lookup"><span data-stu-id="13b80-130">toocreate a new queue, select **Add Queue**.</span></span>

    ![選取 [新增佇列]](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. <span data-ttu-id="13b80-132">Hello 新佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="13b80-132">Name hello new queue.</span></span>

    ![名稱 hello 佇列 Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. <span data-ttu-id="13b80-134">保留 hello**容量**值 50%，然後選取 hello**動作** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13b80-134">Leave hello **capacity** values at 50%, and then select hello **Actions** button.</span></span>

    ![選取 hello 動作按鈕](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. <span data-ttu-id="13b80-136">選取 [Save and Refresh Queues] \(儲存並重新整理佇列)。</span><span class="sxs-lookup"><span data-stu-id="13b80-136">Select **Save and Refresh Queues**.</span></span>

    ![選取 [Save and Refresh Queues] \(儲存並重新整理佇列)。](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

<span data-ttu-id="13b80-138">這些變更會立即在 hello YARN 排程器 UI 上顯示項目。</span><span class="sxs-lookup"><span data-stu-id="13b80-138">These changes are visible immediately on hello YARN Scheduler UI.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="13b80-139">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="13b80-139">Additional reading</span></span>

- [<span data-ttu-id="13b80-140">YARN CapacityScheduler</span><span class="sxs-lookup"><span data-stu-id="13b80-140">YARN CapacityScheduler</span></span>](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a><span data-ttu-id="13b80-141">如何下載叢集的 YARN 記錄</span><span class="sxs-lookup"><span data-stu-id="13b80-141">How do I download YARN logs from a cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="13b80-142">解決步驟</span><span class="sxs-lookup"><span data-stu-id="13b80-142">Resolution steps</span></span> 

1. <span data-ttu-id="13b80-143">使用安全殼層 (SSH) 用戶端連接 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="13b80-143">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="13b80-144">如需詳細資訊，請參閱[其他閱讀資料](#additional-reading-2)。</span><span class="sxs-lookup"><span data-stu-id="13b80-144">For more information, see [Additional reading](#additional-reading-2).</span></span>

2. <span data-ttu-id="13b80-145">toolist 所有 hello 應用程式識別碼 hello YARN 應用程式目前正在執行，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="13b80-145">toolist all hello application IDs of hello YARN applications that are currently running, run hello following command:</span></span>

    ```apache
    yarn top
    ```
    <span data-ttu-id="13b80-146">hello 識別碼會列在 hello **APPLICATIONID**資料行。</span><span class="sxs-lookup"><span data-stu-id="13b80-146">hello IDs are listed in hello **APPLICATIONID** column.</span></span> <span data-ttu-id="13b80-147">您可以下載記錄檔從 hello **APPLICATIONID**資料行。</span><span class="sxs-lookup"><span data-stu-id="13b80-147">You can download logs from hello **APPLICATIONID** column.</span></span>

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

3. <span data-ttu-id="13b80-148">toodownload YARN 容器記錄檔中的所有應用程式主機，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="13b80-148">toodownload YARN container logs for all application masters, use hello following command:</span></span>
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    <span data-ttu-id="13b80-149">此命令會建立名為 amlogs.txt 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="13b80-149">This command creates a log file named amlogs.txt.</span></span> 

4. <span data-ttu-id="13b80-150">toodownload YARN 容器記錄檔中的唯一的 hello 最新的應用程式主機，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="13b80-150">toodownload YARN container logs for only hello latest application master, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    <span data-ttu-id="13b80-151">此命令會建立名為 latestamlogs.txt 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="13b80-151">This command creates a log file named latestamlogs.txt.</span></span> 

4. <span data-ttu-id="13b80-152">toodownload YARN 容器記錄檔中的第一個兩個應用程式主機 hello，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="13b80-152">toodownload YARN container logs for hello first two application masters, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    <span data-ttu-id="13b80-153">此命令會建立名為 first2amlogs.txt 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="13b80-153">This command creates a log file named first2amlogs.txt.</span></span> 

5. <span data-ttu-id="13b80-154">所有的 YARN 容器記錄檔，會使用 toodownload hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="13b80-154">toodownload all YARN container logs, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    <span data-ttu-id="13b80-155">此命令會建立名為 logs.txt 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="13b80-155">This command creates a log file named logs.txt.</span></span> 

6. <span data-ttu-id="13b80-156">toodownload hello YARN 容器記錄檔以取得特定的容器，使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="13b80-156">toodownload hello YARN container log for a specific container, use hello following command:</span></span>

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    <span data-ttu-id="13b80-157">此命令會建立名為 containerlogs.txt 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="13b80-157">This command creates a log file named containerlogs.txt.</span></span>

### <span data-ttu-id="13b80-158"><a name="additional-reading-2"></a>其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="13b80-158"><a name="additional-reading-2"></a>Additional reading</span></span>

- [<span data-ttu-id="13b80-159">透過 SSH 連線 tooHDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="13b80-159">Connect tooHDInsight (Hadoop) by using SSH</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [<span data-ttu-id="13b80-160">Apache Hadoop YARN 概念與應用程式</span><span class="sxs-lookup"><span data-stu-id="13b80-160">Apache Hadoop YARN concepts and applications</span></span>](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







