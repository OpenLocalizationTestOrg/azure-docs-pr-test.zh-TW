---
title: "aaaCustomize Hadoop 叢集以提供 hello 資料科學的小組流程 |Microsoft 文件"
description: "自訂 Azure HDInsight Hadoop 叢集中提供熱門 Python 模組。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a><span data-ttu-id="e135b-103">自訂 hello 小組資料科學程序的 Azure HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="e135b-103">Customize Azure HDInsight Hadoop clusters for hello Team Data Science Process</span></span>
<span data-ttu-id="e135b-104">本文說明如何安裝 64 位元 Anaconda (Python 2.7) toocustomize HDInsight Hadoop 叢集每個節點上 hello 叢集佈建為 HDInsight 服務時。</span><span class="sxs-lookup"><span data-stu-id="e135b-104">This article describes how toocustomize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when hello cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="e135b-105">它也會示範如何 tooaccess hello toosubmit 自訂工作 toohello 叢集中前端節點。</span><span class="sxs-lookup"><span data-stu-id="e135b-105">It also shows how tooaccess hello headnode toosubmit custom jobs toohello cluster.</span></span> <span data-ttu-id="e135b-106">這項自訂許多熱門 Python 模組，隨附於 Anaconda，方便用於使用者定義的函數 (Udf) 是設計 tooprocess hello 叢集中的 Hive 記錄。</span><span class="sxs-lookup"><span data-stu-id="e135b-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed tooprocess Hive records in hello cluster.</span></span> <span data-ttu-id="e135b-107">在此案例中使用的 hello 程序的指示，請參閱[如何 toosubmit Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)。</span><span class="sxs-lookup"><span data-stu-id="e135b-107">For instructions on hello procedures used in this scenario, see [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="e135b-108">hello 下列功能表連結，說明如何設定 hello tooset 各種資料科學環境使用 hello tootopics[小組資料科學程序 (TDSP)](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e135b-108">hello following menu links tootopics that describe how tooset up hello various data science environments used by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="e135b-109"><a name="customize"></a>自訂 Azure HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="e135b-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="e135b-110">toocreate 自訂 HDInsight Hadoop 叢集中，啟動登入太[**Azure 傳統入口網站**](https://manage.windowsazure.com/)，按一下 **新增**hello 留在底端的角，，，然後選取 [資料服務-> [HDINSIGHT]-> [**自訂建立**向上 hello toobring**叢集詳細資料**視窗。</span><span class="sxs-lookup"><span data-stu-id="e135b-110">toocreate a customized HDInsight Hadoop cluster, start by logging on too[**Azure classic portal**](https://manage.windowsazure.com/), click **New** at hello left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** toobring up hello **Cluster Details** window.</span></span> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="e135b-112">輸入 hello hello 叢集 toobe 組態頁面 1，建立名稱，並接受預設值為 hello 其他欄位。</span><span class="sxs-lookup"><span data-stu-id="e135b-112">Input hello name of hello cluster toobe created on configuration page 1, and accept default values for hello other fields.</span></span> <span data-ttu-id="e135b-113">按一下 hello 箭號 toogo toohello 下一個組態頁面。</span><span class="sxs-lookup"><span data-stu-id="e135b-113">Click hello arrow toogo toohello next configuration page.</span></span> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="e135b-115">在組態 頁面 2 輸入 hello 數目**資料節點**，選取 hello**地區/虛擬網路**，選取 hello 大小的 hello**前端節點**和 hello **資料節點**。</span><span class="sxs-lookup"><span data-stu-id="e135b-115">On configuration page 2, input hello number of **DATA NODES**, select hello **REGION/VIRTUAL NETWORK**, and select hello sizes of hello **HEAD NODE** and hello **DATA NODE**.</span></span> <span data-ttu-id="e135b-116">按一下 hello 箭號 toogo toohello 下一個組態頁面。</span><span class="sxs-lookup"><span data-stu-id="e135b-116">Click hello arrow toogo toohello next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="e135b-117">hello**地區/虛擬網路**具有 toobe hello 相同為 hello hello 即將 toobe hello HDInsight Hadoop 叢集中使用的儲存體帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="e135b-117">hello **REGION/VIRTUAL NETWORK** has toobe hello same as hello region of hello storage account that is going toobe used for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e135b-118">否則，在 hello 第四個組態頁面中，hello 儲存體帳戶不會出現在下拉式清單中的 hello**帳戶名稱**。</span><span class="sxs-lookup"><span data-stu-id="e135b-118">Otherwise, in hello fourth configuration page, hello storage account will not appear on hello dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="e135b-120">在設定第 3 頁，提供使用者名稱和密碼 hello HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="e135b-120">On configuration page 3, provide a user name and password for hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e135b-121">**不這麼做**選取 hello *Enter hello Hive/Oozie 中繼存放區*。</span><span class="sxs-lookup"><span data-stu-id="e135b-121">**Do not** select hello *Enter hello Hive/Oozie Metastore*.</span></span> <span data-ttu-id="e135b-122">然後，按一下 hello 箭號 toogo toohello 下一個組態頁面。</span><span class="sxs-lookup"><span data-stu-id="e135b-122">Then, click hello arrow toogo toohello next configuration page.</span></span> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="e135b-124">設定第 4 頁，指定 hello 儲存體帳戶名稱，hello HDInsight Hadoop 叢集中的 hello 預設容器。</span><span class="sxs-lookup"><span data-stu-id="e135b-124">On configuration page 4, specify hello storage account name, hello default container of hello HDInsight Hadoop cluster.</span></span> <span data-ttu-id="e135b-125">如果您選取*建立預設容器*在 hello**預設容器**下拉式清單中，以 hello 容器相同的名稱，將會建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="e135b-125">If you select *Create default container* in hello **DEFAULT CONTAINER** dropdown list, a container with hello same name as hello cluster will be created.</span></span> <span data-ttu-id="e135b-126">按一下 hello 箭號 toogo toohello 最後一個組態頁面。</span><span class="sxs-lookup"><span data-stu-id="e135b-126">Click hello arrow toogo toohello last configuration page.</span></span>

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="e135b-128">在最終的 hello**指令碼動作**組態] 頁面上，按一下 [**加入指令碼動作**按鈕，然後填入下列值的 hello 的 hello 文字欄位。</span><span class="sxs-lookup"><span data-stu-id="e135b-128">On hello final **Script Actions** configuration page, click **add script action** button, and fill hello text fields with hello following values.</span></span>

* <span data-ttu-id="e135b-129">**名稱**-hello 名稱，此指令碼動作的任何字串</span><span class="sxs-lookup"><span data-stu-id="e135b-129">**NAME** - any string as hello name of this script action</span></span>
* <span data-ttu-id="e135b-130">**節點類型** - 選取 [所有節點]</span><span class="sxs-lookup"><span data-stu-id="e135b-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="e135b-131">**指令碼 URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="e135b-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="e135b-132">*publicscripts*是 hello 儲存體帳戶中的公用容器</span><span class="sxs-lookup"><span data-stu-id="e135b-132">*publicscripts* is a public container in hello storage account</span></span> 
  * <span data-ttu-id="e135b-133">*getgoing*我們在 Azure 中使用 tooshare PowerShell 指令碼檔案 toofacilitate 使用者的工作</span><span class="sxs-lookup"><span data-stu-id="e135b-133">*getgoing* we use tooshare PowerShell script files toofacilitate users' work in Azure</span></span>
* <span data-ttu-id="e135b-134">**PARAMETERS** - (保留空白)</span><span class="sxs-lookup"><span data-stu-id="e135b-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="e135b-135">最後，按一下 hello 核取記號 toostart hello 建立自訂的 hello HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="e135b-135">Finally, click hello check mark toostart hello creation of hello customized HDInsight Hadoop cluster.</span></span> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="e135b-137"><a name="headnode"></a>存取 hello 的 Hadoop 叢集前端節點</span><span class="sxs-lookup"><span data-stu-id="e135b-137"><a name="headnode"></a> Access hello Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="e135b-138">您可以透過 RDP 存取 hello hello Hadoop 叢集前端節點之前，您必須啟用 Azure 中的遠端存取 toohello Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="e135b-138">You must enable remote access toohello Hadoop cluster in Azure before you can access hello head node of hello Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="e135b-139">登入 toohello [ **Azure 傳統入口網站**](https://manage.windowsazure.com/)，選取**HDInsight** hello 左側從 hello 群集清單選取 Hadoop 叢集，請按一下 hello **組態**索引標籤，然後再按一下 [hello**啟用遠端**在 hello hello 頁面底部的圖示。</span><span class="sxs-lookup"><span data-stu-id="e135b-139">Log in toohello [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on hello left, select your Hadoop cluster from hello list of clusters, click hello **CONFIGURATION** tab, and then click hello **ENABLE REMOTE** icon at hello bottom of hello page.</span></span>
   
    ![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="e135b-141">在 hello**設定遠端桌面**視窗中，輸入 hello 使用者名稱和密碼欄位，並選取 遠端存取的 hello 到期日。</span><span class="sxs-lookup"><span data-stu-id="e135b-141">In hello **Configure Remote Desktop** window, enter hello USER NAME and PASSWORD fields, and select hello expiration date for remote access.</span></span> <span data-ttu-id="e135b-142">然後按一下 hello 核取記號 tooenable hello 遠端存取 toohello 前端節點的 hello Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="e135b-142">Then click hello check mark tooenable hello remote access toohello head node of hello Hadoop cluster.</span></span>
   
    ![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="e135b-144">hello 使用者名稱和密碼 hello 遠端存取的不 hello 使用者名稱和密碼，讓您用於建立 hello Hadoop 叢集時。</span><span class="sxs-lookup"><span data-stu-id="e135b-144">hello user name and password for hello remote access are not hello user name and password that you use when you created hello Hadoop cluster.</span></span> <span data-ttu-id="e135b-145">這是另一組個別的認證。</span><span class="sxs-lookup"><span data-stu-id="e135b-145">This is a separate set of credentials.</span></span> <span data-ttu-id="e135b-146">同時，hello 的 hello 遠端存取的到期日必須 toobe 7 天內從 hello 目前的日期。</span><span class="sxs-lookup"><span data-stu-id="e135b-146">Also, hello expiration date of hello remote access has toobe within 7 days from hello current date.</span></span>
> 
> 

<span data-ttu-id="e135b-147">啟用遠端存取之後，請按一下**連接**底部 hello hello 頁面 tooremote hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="e135b-147">After remote access is enabled, click **CONNECT** at hello bottom of hello page tooremote into hello head node.</span></span> <span data-ttu-id="e135b-148">您輸入您稍早指定的 hello 遠端存取使用者的 hello 認證登入 toohello hello Hadoop 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="e135b-148">You log on toohello head node of hello Hadoop cluster by entering hello credentials for hello remote access user that you specified earlier.</span></span>

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="e135b-150">hello hello 進階分析程序中的下一個步驟中的對應 hello[小組資料科學程序 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) ，而且可能包括將資料移入 HDInsight，然後處理以及它那里範例中學習 hello 資料的準備步驟使用 Azure Machine Learning 中。</span><span class="sxs-lookup"><span data-stu-id="e135b-150">hello next steps in hello advanced analytics process are mapped in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from hello data with Azure Machine Learning.</span></span>

<span data-ttu-id="e135b-151">請參閱[如何 toosubmit Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)如需有關如何 tooaccess hello Anaconda 中包含從 hello 中使用者定義函數 (Udf 所使用的 tooprocess) 的 hello 叢集前端節點的 Python 模組指示 hive 控制檔儲存的記錄hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="e135b-151">See [How toosubmit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how tooaccess hello Python modules that are included in Anaconda from hello head node of hello cluster in user-defined functions (UDFs) that are used tooprocess Hive records stored in hello cluster.</span></span>

