---
title: "在 Azure HDInsight 叢集化 Apache Spark aaaManage 資源 |Microsoft 文件"
description: "了解 toouse 管理 Azure HDInsight 上的 Spark 叢集，以提升效能的資源。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a><span data-ttu-id="66845-103">在 Azure HDInsight 上管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="66845-103">Manage resources for Apache Spark cluster on Azure HDInsight</span></span> 

<span data-ttu-id="66845-104">在本文中，您將學習 tooaccess hello 介面，例如 Ambari UI、 YARN UI 和 hello Spark 記錄伺服器與您的 Spark 叢集的相關聯。</span><span class="sxs-lookup"><span data-stu-id="66845-104">In this article you will learn how tooaccess hello interfaces like Ambari UI, YARN UI, and hello Spark History Server associated with your Spark cluster.</span></span> <span data-ttu-id="66845-105">您也將了解如何 tootune hello 叢集設定以獲得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="66845-105">You will also learn about how tootune hello cluster configuration for optimal performance.</span></span>

<span data-ttu-id="66845-106">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="66845-106">**Prerequisites:**</span></span>

<span data-ttu-id="66845-107">您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="66845-107">You must have hello following:</span></span>

* <span data-ttu-id="66845-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66845-108">An Azure subscription.</span></span> <span data-ttu-id="66845-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="66845-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="66845-110">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="66845-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="66845-111">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="66845-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="how-do-i-launch-hello-ambari-web-ui"></a><span data-ttu-id="66845-112">我要如何啟動 hello Ambari Web UI？</span><span class="sxs-lookup"><span data-stu-id="66845-112">How do I launch hello Ambari Web UI?</span></span>
1. <span data-ttu-id="66845-113">從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。</span><span class="sxs-lookup"><span data-stu-id="66845-113">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="66845-114">您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="66845-114">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>
2. <span data-ttu-id="66845-115">從 hello Spark 叢集刀鋒視窗中，按一下 **儀表板**。</span><span class="sxs-lookup"><span data-stu-id="66845-115">From hello Spark cluster blade, click **Dashboard**.</span></span> <span data-ttu-id="66845-116">出現提示時，輸入 hello Spark 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="66845-116">When prompted, enter hello admin credentials for hello Spark cluster.</span></span>

    <span data-ttu-id="66845-117">![啟動 Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "啟動 Resource Manager")</span><span class="sxs-lookup"><span data-stu-id="66845-117">![Launch Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Start Resource Manager")</span></span>
3. <span data-ttu-id="66845-118">這應該啟動 hello Ambari Web UI 中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="66845-118">This should launch hello Ambari Web UI, as shown below.</span></span>

    <span data-ttu-id="66845-119">![Ambari Web UI](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web UI")</span><span class="sxs-lookup"><span data-stu-id="66845-119">![Ambari Web UI](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web UI")</span></span>   

## <a name="how-do-i-launch-hello-spark-history-server"></a><span data-ttu-id="66845-120">我要如何啟動 hello Spark 記錄伺服器？</span><span class="sxs-lookup"><span data-stu-id="66845-120">How do I launch hello Spark History Server?</span></span>
1. <span data-ttu-id="66845-121">從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。</span><span class="sxs-lookup"><span data-stu-id="66845-121">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span>
2. <span data-ttu-id="66845-122">從 hello 叢集刀鋒視窗中，在**快速連結**，按一下 **叢集儀表板**。</span><span class="sxs-lookup"><span data-stu-id="66845-122">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**.</span></span> <span data-ttu-id="66845-123">在 hello**叢集儀表板**刀鋒視窗中，按一下  **Spark 記錄伺服器**。</span><span class="sxs-lookup"><span data-stu-id="66845-123">In hello **Cluster Dashboard** blade, click **Spark History Server**.</span></span>

    <span data-ttu-id="66845-124">![Spark 歷程記錄伺服器](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark 歷程記錄伺服器")</span><span class="sxs-lookup"><span data-stu-id="66845-124">![Spark History Server](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark History Server")</span></span>

    <span data-ttu-id="66845-125">出現提示時，輸入 hello Spark 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="66845-125">When prompted, enter hello admin credentials for hello Spark cluster.</span></span>

## <a name="how-do-i-launch-hello-yarn-ui"></a><span data-ttu-id="66845-126">我要如何啟動 hello Yarn UI？</span><span class="sxs-lookup"><span data-stu-id="66845-126">How do I launch hello Yarn UI?</span></span>
<span data-ttu-id="66845-127">您可以使用 hello YARN UI toomonitor 應用程式目前正在 hello Spark 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="66845-127">You can use hello YARN UI toomonitor applications that are currently running on hello Spark cluster.</span></span>

1. <span data-ttu-id="66845-128">從 hello 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **YARN**。</span><span class="sxs-lookup"><span data-stu-id="66845-128">From hello cluster blade, click **Cluster Dashboard**, and then click **YARN**.</span></span>

    ![啟動 YARN UI](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > <span data-ttu-id="66845-130">或者，您也可以啟動 hello YARN UI 從 hello Ambari UI。</span><span class="sxs-lookup"><span data-stu-id="66845-130">Alternatively, you can also launch hello YARN UI from hello Ambari UI.</span></span> <span data-ttu-id="66845-131">按一下 toolaunch hello Ambari UI hello 叢集刀鋒視窗中，從**叢集儀表板**，然後按一下 **HDInsight 叢集儀表板**。</span><span class="sxs-lookup"><span data-stu-id="66845-131">toolaunch hello Ambari UI, from hello cluster blade, click **Cluster Dashboard**, and then click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="66845-132">從 hello Ambari UI 中，按一下  **YARN**，按一下 **快速連結**hello 作用中的資源管理員，然後按**ResourceManager UI**。</span><span class="sxs-lookup"><span data-stu-id="66845-132">From hello Ambari UI, click **YARN**, click **Quick Links**, click hello active resource manager, and then click **ResourceManager UI**.</span></span>
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a><span data-ttu-id="66845-133">什麼是 hello 最佳群集組態 toorun Spark 應用程式？</span><span class="sxs-lookup"><span data-stu-id="66845-133">What is hello optimum cluster configuration toorun Spark applications?</span></span>
<span data-ttu-id="66845-134">用於根據應用程式需求的 Spark 組態 hello 三個參數都是`spark.executor.instances`， `spark.executor.cores`，和`spark.executor.memory`。</span><span class="sxs-lookup"><span data-stu-id="66845-134">hello three key parameters that can be used for Spark configuration depending on application requirements are `spark.executor.instances`, `spark.executor.cores`, and `spark.executor.memory`.</span></span> <span data-ttu-id="66845-135">執行程式是針對 Spark 應用程式啟動的程序。</span><span class="sxs-lookup"><span data-stu-id="66845-135">An Executor is a process launched for a Spark application.</span></span> <span data-ttu-id="66845-136">它在 hello 背景工作節點上執行，而且是負責 toocarry hello hello 應用程式的工作。</span><span class="sxs-lookup"><span data-stu-id="66845-136">It runs on hello worker node and is responsible toocarry out hello tasks for hello application.</span></span> <span data-ttu-id="66845-137">執行程式和每個叢集的 hello executor 大小的 hello 預設數目是根據 hello 數目背景工作節點和 hello 背景工作節點大小計算。</span><span class="sxs-lookup"><span data-stu-id="66845-137">hello default number of executors and hello executor sizes for each cluster is calculated based on hello number of worker nodes and hello worker node size.</span></span> <span data-ttu-id="66845-138">這些儲存在`spark-defaults.conf`hello 叢集前端節點上。</span><span class="sxs-lookup"><span data-stu-id="66845-138">These are stored in `spark-defaults.conf` on hello cluster head nodes.</span></span>

<span data-ttu-id="66845-139">hello 三個組態參數可以設定在 hello 叢集層級 （適用於 hello 叢集執行的所有應用程式），或每個個別應用程式也可以指定。</span><span class="sxs-lookup"><span data-stu-id="66845-139">hello three configuration parameters can be configured at hello cluster level (for all applications that run on hello cluster) or can be specified for each individual application as well.</span></span>

### <a name="change-hello-parameters-using-ambari-ui"></a><span data-ttu-id="66845-140">變更使用 Ambari UI hello 參數</span><span class="sxs-lookup"><span data-stu-id="66845-140">Change hello parameters using Ambari UI</span></span>
1. <span data-ttu-id="66845-141">從 hello Ambari UI 按一下**Spark**，按一下**Configs**，然後展開**自訂 spark 預設**。</span><span class="sxs-lookup"><span data-stu-id="66845-141">From hello Ambari UI click **Spark**, click **Configs**, and then expand **Custom spark-defaults**.</span></span>

    ![使用 Ambari UI 設定參數](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. <span data-ttu-id="66845-143">hello 預設值為 hello 叢集上同時執行的良好 toohave 4 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66845-143">hello default values are good toohave 4 Spark applications run concurrently on hello cluster.</span></span> <span data-ttu-id="66845-144">您可以變更這些值從 hello 使用者介面，如下所示。</span><span class="sxs-lookup"><span data-stu-id="66845-144">You can changes these values from hello user interface, as shown below.</span></span>

    ![使用 Ambari UI 設定參數](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. <span data-ttu-id="66845-146">按一下**儲存**toosave hello 組態變更。</span><span class="sxs-lookup"><span data-stu-id="66845-146">Click **Save** toosave hello configuration changes.</span></span> <span data-ttu-id="66845-147">在 hello hello 頁面頂端，系統會提示您所有 hello 的 toorestart 受影響的服務。</span><span class="sxs-lookup"><span data-stu-id="66845-147">At hello top of hello page, you will be prompted toorestart all hello affected services.</span></span> <span data-ttu-id="66845-148">按一下 [重新啟動] 。</span><span class="sxs-lookup"><span data-stu-id="66845-148">Click **Restart**.</span></span>

    ![重新啟動服務](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a><span data-ttu-id="66845-150">變更 hello 參數 Jupyter 筆記本中執行的應用程式</span><span class="sxs-lookup"><span data-stu-id="66845-150">Change hello parameters for an application running in Jupyter notebook</span></span>
<span data-ttu-id="66845-151">Hello Jupyter 筆記本中執行的應用程式，您可以使用 hello `%%configure` magic toomake hello 組態變更。</span><span class="sxs-lookup"><span data-stu-id="66845-151">For applications running in hello Jupyter notebook, you can use hello `%%configure` magic toomake hello configuration changes.</span></span> <span data-ttu-id="66845-152">在理想情況下，您必須進行這類變更在 hello 開頭 hello 應用程式，才能執行您的第一個程式碼儲存格。</span><span class="sxs-lookup"><span data-stu-id="66845-152">Ideally, you must make such changes at hello beginning of hello application, before you run your first code cell.</span></span> <span data-ttu-id="66845-153">這可確保該 hello 組態會套用的 toohello 晚總工作階段中，取得建立時。</span><span class="sxs-lookup"><span data-stu-id="66845-153">This ensures that hello configuration is applied toohello Livy session, when it gets created.</span></span> <span data-ttu-id="66845-154">如果您想在稍後階段 hello 應用程式中的 toochange hello 組態，您必須使用 hello`-f`參數。</span><span class="sxs-lookup"><span data-stu-id="66845-154">If you want toochange hello configuration at a later stage in hello application, you must use hello `-f` parameter.</span></span> <span data-ttu-id="66845-155">不過，這麼做會所有進度 hello 中應用程式將會遺失。</span><span class="sxs-lookup"><span data-stu-id="66845-155">However, by doing so all progress in hello application will be lost.</span></span>

<span data-ttu-id="66845-156">hello 以下程式碼片段顯示如何 toochange hello Jupyter 中執行的應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="66845-156">hello snippet below shows how toochange hello configuration for an application running in Jupyter.</span></span>

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

<span data-ttu-id="66845-157">組態參數必須為 JSON 字串中傳遞且必須在 hello 下一行之後 hello magic hello 範例資料行中所示。</span><span class="sxs-lookup"><span data-stu-id="66845-157">Configuration parameters must be passed in as a JSON string and must be on hello next line after hello magic, as shown in hello example column.</span></span>

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a><span data-ttu-id="66845-158">應用程式使用提交變更 hello 參數 spark-submit 對</span><span class="sxs-lookup"><span data-stu-id="66845-158">Change hello parameters for an application submitted using spark-submit</span></span>
<span data-ttu-id="66845-159">下列命令是如何 toochange hello 使用提交的批次應用程式的組態參數的範例`spark-submit`。</span><span class="sxs-lookup"><span data-stu-id="66845-159">Following command is an example of how toochange hello configuration parameters for a batch application that is submitted using `spark-submit`.</span></span>

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a><span data-ttu-id="66845-160">使用 cURL 提交應用程式的變更 hello 參數</span><span class="sxs-lookup"><span data-stu-id="66845-160">Change hello parameters for an application submitted using cURL</span></span>
<span data-ttu-id="66845-161">下列命令是如何 toochange hello 使用 cURL 提交的批次應用程式的組態參數的範例。</span><span class="sxs-lookup"><span data-stu-id="66845-161">Following command is an example of how toochange hello configuration parameters for a batch application that is submitted using using cURL.</span></span>

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a><span data-ttu-id="66845-162">如何在 Spark Thrift 伺服器變更這些參數？</span><span class="sxs-lookup"><span data-stu-id="66845-162">How do I change these parameters on a Spark Thrift Server?</span></span>
<span data-ttu-id="66845-163">Spark Thrift 伺服器提供 JDBC/ODBC 存取 tooa Spark 叢集，而且是使用的 tooservice Spark SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="66845-163">Spark Thrift Server provides JDBC/ODBC access tooa Spark cluster and is used tooservice Spark SQL queries.</span></span> <span data-ttu-id="66845-164">Power BI、Tableau 等工具</span><span class="sxs-lookup"><span data-stu-id="66845-164">Tools like Power BI, Tableau etc.</span></span> <span data-ttu-id="66845-165">ODBC 通訊協定 toocommunicate 搭配 Spark Thrift 伺服器 tooexecute Spark SQL 查詢使用做為 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66845-165">use ODBC protocol toocommunicate with Spark Thrift Server tooexecute Spark SQL queries as a Spark Application.</span></span> <span data-ttu-id="66845-166">Spark 叢集，以建立時，兩個 hello Spark Thrift 伺服器會啟動，每個前端節點上的其中一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="66845-166">When a Spark cluster is created, two instances of hello Spark Thrift Server are started, one on each head node.</span></span> <span data-ttu-id="66845-167">每個 Spark Thrift 伺服器會顯示以 hello YARN UI 中的 Spark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66845-167">Each Spark Thrift Server is visible as a Spark application in hello YARN UI.</span></span>

<span data-ttu-id="66845-168">Spark Thrift 伺服器使用二手動態執行程式配置，因此 hello`spark.executor.instances`未使用。</span><span class="sxs-lookup"><span data-stu-id="66845-168">Spark Thrift Server uses Spark dynamic executor allocation and hence hello `spark.executor.instances` is not used.</span></span> <span data-ttu-id="66845-169">相反地，Spark Thrift 伺服器會使用`spark.dynamicAllocation.minExecutors`和`spark.dynamicAllocation.maxExecutors`toospecify hello 執行程式計數。</span><span class="sxs-lookup"><span data-stu-id="66845-169">Instead, Spark Thrift Server uses `spark.dynamicAllocation.minExecutors` and `spark.dynamicAllocation.maxExecutors` toospecify hello executor count.</span></span> <span data-ttu-id="66845-170">hello 組態參數`spark.executor.cores`和`spark.executor.memory`是使用 toomodify hello 執行程式的大小。</span><span class="sxs-lookup"><span data-stu-id="66845-170">hello configuration parameters `spark.executor.cores` and `spark.executor.memory` is used toomodify hello executor size.</span></span> <span data-ttu-id="66845-171">您可以變更這些參數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="66845-171">You can change these parameters as shown below.</span></span>

* <span data-ttu-id="66845-172">展開 hello**進階 spark-thrift-sparkconf**類別 tooupdate hello 參數`spark.dynamicAllocation.minExecutors`， `spark.dynamicAllocation.maxExecutors`，和`spark.executor.memory`。</span><span class="sxs-lookup"><span data-stu-id="66845-172">Expand hello **Advanced spark-thrift-sparkconf** category tooupdate hello parameters `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, and `spark.executor.memory`.</span></span>

    ![設定 Spark Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* <span data-ttu-id="66845-174">展開 hello**自訂 spark thrift sparkconf**分類 tooupdate hello 參數`spark.executor.cores`。</span><span class="sxs-lookup"><span data-stu-id="66845-174">Expand hello **Custom spark-thrift-sparkconf** category tooupdate hello parameter `spark.executor.cores`.</span></span>

    ![設定 Spark Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a><span data-ttu-id="66845-176">如何變更 hello 驅動程式記憶體的 hello Spark Thrift 伺服器？</span><span class="sxs-lookup"><span data-stu-id="66845-176">How do I change hello driver memory of hello Spark Thrift Server?</span></span>
<span data-ttu-id="66845-177">Spark Thrift 伺服器驅動程式的記憶體是已設定的 too25 %hello 前端節點的 RAM 大小，提供 hello 前端節點的 hello 總 RAM 大小大於 14 GB。</span><span class="sxs-lookup"><span data-stu-id="66845-177">Spark Thrift Server driver memory is configured too25% of hello head node RAM size, provided hello total RAM size of hello head node is greater than 14GB.</span></span> <span data-ttu-id="66845-178">您可以使用 hello Ambari UI toochange hello 驅動程式的記憶體組態，如下所示。</span><span class="sxs-lookup"><span data-stu-id="66845-178">You can use hello Ambari UI toochange hello driver memory configuration, as shown below.</span></span>

* <span data-ttu-id="66845-179">從 hello Ambari UI 按一下**Spark**，按一下**Configs**，依序展開**進階 spark env**，然後提供 hello 值**spark_thrift_cmd_opts**.</span><span class="sxs-lookup"><span data-stu-id="66845-179">From hello Ambari UI click **Spark**, click **Configs**, expand **Advanced spark-env**, and then provide hello value for **spark_thrift_cmd_opts**.</span></span>

    ![設定 Spark Thrift 伺服器 RAM](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a><span data-ttu-id="66845-181">我沒有搭配使用 BI 和 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="66845-181">I do not use BI with Spark cluster.</span></span> <span data-ttu-id="66845-182">如何備份佔用 hello 資源？</span><span class="sxs-lookup"><span data-stu-id="66845-182">How do I take hello resources back?</span></span>
<span data-ttu-id="66845-183">因為我們使用 Spark 動態配置，hello thrift 伺服器所耗用的資源是 hello hello 兩個應用程式主機的資源。</span><span class="sxs-lookup"><span data-stu-id="66845-183">Since we use Spark dynamic allocation, hello only resources that are consumed by thrift server are hello resources for hello two application masters.</span></span> <span data-ttu-id="66845-184">tooreclaim 這些資源，您必須先停止 hello Thrift 伺服器 hello 叢集上執行的服務。</span><span class="sxs-lookup"><span data-stu-id="66845-184">tooreclaim these resources you must stop hello Thrift Server services running on hello cluster.</span></span>

1. <span data-ttu-id="66845-185">從 hello Ambari UI hello 左窗格中，按一下  **Spark**。</span><span class="sxs-lookup"><span data-stu-id="66845-185">From hello Ambari UI, from hello left pane, click **Spark**.</span></span>
2. <span data-ttu-id="66845-186">在 hello 下一步 頁面上，按一下**Spark Thrift 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="66845-186">In hello next page, click **Spark Thrift Servers**.</span></span>

    ![重新啟動 Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. <span data-ttu-id="66845-188">您應該會看到 hello 兩個 headnodes 哪些 hello Spark Thrift 伺服器正在執行。</span><span class="sxs-lookup"><span data-stu-id="66845-188">You should see hello two headnodes on which hello Spark Thrift Server is running.</span></span> <span data-ttu-id="66845-189">按一下其中一個 hello headnodes。</span><span class="sxs-lookup"><span data-stu-id="66845-189">Click one of hello headnodes.</span></span>

    ![重新啟動 Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. <span data-ttu-id="66845-191">hello 下一個頁面會列出在該叢集前端節點上執行的所有 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="66845-191">hello next page lists all hello services running on that headnode.</span></span> <span data-ttu-id="66845-192">從 hello 清單中，按一下 hello 下拉式按鈕下一步 tooSpark Thrift 伺服器，然後按一下**停止**。</span><span class="sxs-lookup"><span data-stu-id="66845-192">From hello list click hello drop-down button next tooSpark Thrift Server, and then click **Stop**.</span></span>

    ![重新啟動 Thrift 伺服器](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. <span data-ttu-id="66845-194">上重複這些步驟 hello 以及其他前端節點。</span><span class="sxs-lookup"><span data-stu-id="66845-194">Repeat these steps on hello other headnode as well.</span></span>

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a><span data-ttu-id="66845-195">我的 Jupyter Notebook 並未如預期般執行。</span><span class="sxs-lookup"><span data-stu-id="66845-195">My Jupyter notebooks are not running as expected.</span></span> <span data-ttu-id="66845-196">如何重新啟動 hello 服務？</span><span class="sxs-lookup"><span data-stu-id="66845-196">How can I restart hello service?</span></span>
<span data-ttu-id="66845-197">啟動 hello Ambari Web UI，如上所示。</span><span class="sxs-lookup"><span data-stu-id="66845-197">Launch hello Ambari Web UI as shown above.</span></span> <span data-ttu-id="66845-198">從 hello 左側瀏覽窗格中，按一下  **Jupyter**，按一下 **服務動作**，然後按一下**重新啟動所有**。</span><span class="sxs-lookup"><span data-stu-id="66845-198">From hello left navigation pane, click **Jupyter**, click **Service Actions**, and then click **Restart All**.</span></span> <span data-ttu-id="66845-199">這會啟動 hello Jupyter 服務上所有的 hello headnodes。</span><span class="sxs-lookup"><span data-stu-id="66845-199">This will start hello Jupyter service on all hello headnodes.</span></span>

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a><span data-ttu-id="66845-200">如何知道我是否用盡資源？</span><span class="sxs-lookup"><span data-stu-id="66845-200">How do I know if I am running out of resources?</span></span>
<span data-ttu-id="66845-201">啟動 hello Yarn UI，如上所示。</span><span class="sxs-lookup"><span data-stu-id="66845-201">Launch hello Yarn UI as shown above.</span></span> <span data-ttu-id="66845-202">在叢集度量資料表之上囉 」 畫面中，檢查值**記憶體使用**和**記憶體總計**資料行。</span><span class="sxs-lookup"><span data-stu-id="66845-202">In Cluster Metrics table on top of hello screen, check values of **Memory Used** and **Memory Total** columns.</span></span> <span data-ttu-id="66845-203">如果 hello 2 值非常接近，可能不會有足夠資源 toostart hello 下一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="66845-203">If hello 2 values are very close, there might not be enough resources toostart hello next application.</span></span> <span data-ttu-id="66845-204">hello 同樣適用 toohello **VCores 用**和**VCores 總計**資料行。</span><span class="sxs-lookup"><span data-stu-id="66845-204">hello same applies toohello **VCores Used** and **VCores Total** columns.</span></span> <span data-ttu-id="66845-205">此外，在 hello 主要檢視中，如果沒有應用程式仍會維持在**接受**狀態並不會轉換成**執行**也**失敗**狀態時，這也可能表示它沒有取得足夠的資源 toostart。</span><span class="sxs-lookup"><span data-stu-id="66845-205">Also, in hello main view, if there is an application stayed in **ACCEPTED** state and not transitioning into **RUNNING** nor **FAILED** state, this could also be an indication that it is not getting enough resources toostart.</span></span>

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a><span data-ttu-id="66845-206">如何終止執行的應用程式 toofree 資源？</span><span class="sxs-lookup"><span data-stu-id="66845-206">How do I kill a running application toofree up resource?</span></span>
1. <span data-ttu-id="66845-207">在 hello Yarn UI 從 hello 左面板中，按一下 **執行**。</span><span class="sxs-lookup"><span data-stu-id="66845-207">In hello Yarn UI, from hello left panel, click **Running**.</span></span> <span data-ttu-id="66845-208">從 hello 清單中執行的應用程式，判斷 hello 應用程式 toobe 遭到刪除，然後按一下 hello**識別碼**。</span><span class="sxs-lookup"><span data-stu-id="66845-208">From hello list of running applications, determine hello application toobe killed and click on hello **ID**.</span></span>

    <span data-ttu-id="66845-209">![終止 App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "終止 App1")</span><span class="sxs-lookup"><span data-stu-id="66845-209">![Kill App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Kill App1")</span></span>

2. <span data-ttu-id="66845-210">按一下**終止應用程式**hello 頂端的右上角，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="66845-210">Click **Kill Application** on hello top right corner, then click **OK**.</span></span>

    <span data-ttu-id="66845-211">![終止 App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "終止 App2")</span><span class="sxs-lookup"><span data-stu-id="66845-211">![Kill App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Kill App2")</span></span>

## <a name="see-also"></a><span data-ttu-id="66845-212">另請參閱</span><span class="sxs-lookup"><span data-stu-id="66845-212">See also</span></span>
* [<span data-ttu-id="66845-213">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="66845-213">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a><span data-ttu-id="66845-214">針對資料分析師</span><span class="sxs-lookup"><span data-stu-id="66845-214">For data analysts</span></span>

* [<span data-ttu-id="66845-215">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="66845-215">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="66845-216">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="66845-216">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="66845-217">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="66845-217">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [<span data-ttu-id="66845-218">HDInsight 中使用 Spark 的 Application Insight 遙測資料分析</span><span class="sxs-lookup"><span data-stu-id="66845-218">Application Insight telemetry data analysis using Spark in HDInsight</span></span>](hdinsight-spark-analyze-application-insight-logs.md)
* [<span data-ttu-id="66845-219">在 Azure HDInsight Spark 上使用 Caffe 進行分散式深入學習</span><span class="sxs-lookup"><span data-stu-id="66845-219">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a><span data-ttu-id="66845-220">針對 Spark 開發人員</span><span class="sxs-lookup"><span data-stu-id="66845-220">For Spark developers</span></span>

* [<span data-ttu-id="66845-221">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="66845-221">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="66845-222">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="66845-222">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="66845-223">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="66845-223">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="66845-224">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="66845-224">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="66845-225">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="66845-225">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="66845-226">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="66845-226">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="66845-227">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="66845-227">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="66845-228">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="66845-228">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="66845-229">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="66845-229">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)
