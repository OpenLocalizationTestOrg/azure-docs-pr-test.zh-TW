---
title: "自訂適用於 Team Data Science Process 的 Hadoop 叢集 | Microsoft Docs"
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
ms.openlocfilehash: 53ff04ee66b08ae36f3550536c659a547c658fd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-the-team-data-science-process"></a><span data-ttu-id="f5597-103">自訂適用於 Team Data Science Process 的 Azure HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="f5597-103">Customize Azure HDInsight Hadoop clusters for the Team Data Science Process</span></span>
<span data-ttu-id="f5597-104">本文將說明若將 HDInsight Hadoop 叢集佈建為 HDInsight 服務，如何藉由在每個節點上安裝 64 位元的 Anaconda (Python 2.7) 來自訂該叢集。</span><span class="sxs-lookup"><span data-stu-id="f5597-104">This article describes how to customize an HDInsight Hadoop cluster by installing 64-bit Anaconda (Python 2.7) on each node when the cluster is provisioned as an HDInsight service.</span></span> <span data-ttu-id="f5597-105">它也會示範如何存取前端節點，以將自訂工作提交至叢集。</span><span class="sxs-lookup"><span data-stu-id="f5597-105">It also shows how to access the headnode to submit custom jobs to the cluster.</span></span> <span data-ttu-id="f5597-106">這項自訂讓許多熱門的 Python 模組 (隨附於 Anaconda) 非常方便地在使用者定義函式 (UDF) 中使用，這類函式是設計來處理叢集中的 Hive 記錄。</span><span class="sxs-lookup"><span data-stu-id="f5597-106">This customization makes many popular Python modules, that are included in Anaconda, conveniently available for use in user defined functions (UDFs) that are designed to process Hive records in the cluster.</span></span> <span data-ttu-id="f5597-107">如需此案例中使用的程序的相關指示，請參閱 [如何提交 Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)。</span><span class="sxs-lookup"><span data-stu-id="f5597-107">For instructions on the procedures used in this scenario, see [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

<span data-ttu-id="f5597-108">以下功能表所連結的主題會說明如何設定 [Team Data Science Process (TDSP)](data-science-process-overview.md)所用的各種資料科學環境。</span><span class="sxs-lookup"><span data-stu-id="f5597-108">The following menu links to topics that describe how to set up the various data science environments used by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span>

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <span data-ttu-id="f5597-109"><a name="customize"></a>自訂 Azure HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="f5597-109"><a name="customize"></a>Customize Azure HDInsight Hadoop Cluster</span></span>
<span data-ttu-id="f5597-110">若要建立自訂的 HDInsight Hadoop 叢集，請先登入 [**Azure 傳統入口網站**](https://manage.windowsazure.com/)，按一下左下角的 [新增]，然後選取 [資料服務] -> [HDINSIGHT] -> [自訂建立]，以顯示 [叢集詳細資料] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f5597-110">To create a customized HDInsight Hadoop cluster, start by logging on to [**Azure classic portal**](https://manage.windowsazure.com/), click **New** at the left bottom corner, and then select DATA SERVICES -> HDINSIGHT -> **CUSTOM CREATE** to bring up the **Cluster Details** window.</span></span> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="f5597-112">在設定頁面 1 上輸入要建立的叢集名稱，並接受其他欄位的預設值。</span><span class="sxs-lookup"><span data-stu-id="f5597-112">Input the name of the cluster to be created on configuration page 1, and accept default values for the other fields.</span></span> <span data-ttu-id="f5597-113">按一下箭號，以前往下一個設定頁面。</span><span class="sxs-lookup"><span data-stu-id="f5597-113">Click the arrow to go to the next configuration page.</span></span> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

<span data-ttu-id="f5597-115">在組態頁面 2 上，輸入 [資料節點] 的數目，選取 [區域/虛擬網路]，然後選取 [前端節點] 和 [資料節點] 的大小。</span><span class="sxs-lookup"><span data-stu-id="f5597-115">On configuration page 2, input the number of **DATA NODES**, select the **REGION/VIRTUAL NETWORK**, and select the sizes of the **HEAD NODE** and the **DATA NODE**.</span></span> <span data-ttu-id="f5597-116">按一下箭號，以前往下一個設定頁面。</span><span class="sxs-lookup"><span data-stu-id="f5597-116">Click the arrow to go to the next configuration page.</span></span>

> [!NOTE]
> <span data-ttu-id="f5597-117">[區域/虛擬網路] 必須與即將用於 HDInsight Hadoop 叢集的儲存體帳戶區域相同。</span><span class="sxs-lookup"><span data-stu-id="f5597-117">The **REGION/VIRTUAL NETWORK** has to be the same as the region of the storage account that is going to be used for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="f5597-118">否則，在第四個組態頁面中，儲存體帳戶將不會出現在 [帳戶名稱] 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="f5597-118">Otherwise, in the fourth configuration page, the storage account will not appear on the dropdown list of **ACCOUNT NAME**.</span></span>
> 
> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

<span data-ttu-id="f5597-120">在設定頁面 3 上，提供適用於 HDInsight Hadoop 叢集的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f5597-120">On configuration page 3, provide a user name and password for the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="f5597-121">**請勿**選取 [進入 Hive/Oozie 中繼存放區]。</span><span class="sxs-lookup"><span data-stu-id="f5597-121">**Do not** select the *Enter the Hive/Oozie Metastore*.</span></span> <span data-ttu-id="f5597-122">然後按一下箭號，前往下一個設定頁面。</span><span class="sxs-lookup"><span data-stu-id="f5597-122">Then, click the arrow to go to the next configuration page.</span></span> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

<span data-ttu-id="f5597-124">在設定頁面 4 上，指定儲存體帳戶名稱，以及 HDInsight Hadoop 叢集的預設容器。</span><span class="sxs-lookup"><span data-stu-id="f5597-124">On configuration page 4, specify the storage account name, the default container of the HDInsight Hadoop cluster.</span></span> <span data-ttu-id="f5597-125">如果您在 [預設容器] 下拉式清單中選取 [建立預設容器]，就會建立名稱與叢集相同的容器。</span><span class="sxs-lookup"><span data-stu-id="f5597-125">If you select *Create default container* in the **DEFAULT CONTAINER** dropdown list, a container with the same name as the cluster will be created.</span></span> <span data-ttu-id="f5597-126">按一下箭號，前往最後一個設定頁面。</span><span class="sxs-lookup"><span data-stu-id="f5597-126">Click the arrow to go to the last configuration page.</span></span>

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

<span data-ttu-id="f5597-128">在最後的 [指令碼動作] 設定頁面中，按一下 [新增指令碼動作] 按鈕，然後使用下列值填入文字欄位。</span><span class="sxs-lookup"><span data-stu-id="f5597-128">On the final **Script Actions** configuration page, click **add script action** button, and fill the text fields with the following values.</span></span>

* <span data-ttu-id="f5597-129">**名稱** - 可做為這個指令碼動作名稱的任何字串</span><span class="sxs-lookup"><span data-stu-id="f5597-129">**NAME** - any string as the name of this script action</span></span>
* <span data-ttu-id="f5597-130">**節點類型** - 選取 [所有節點]</span><span class="sxs-lookup"><span data-stu-id="f5597-130">**NODE TYPE** - select **All nodes**</span></span>
* <span data-ttu-id="f5597-131">**指令碼 URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span><span class="sxs-lookup"><span data-stu-id="f5597-131">**SCRIPT URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1*</span></span> 
  * <span data-ttu-id="f5597-132">publicscripts 是儲存體帳戶中的公用容器</span><span class="sxs-lookup"><span data-stu-id="f5597-132">*publicscripts* is a public container in the storage account</span></span> 
  * <span data-ttu-id="f5597-133">getgoing 可用來共用 PowerShell 指令碼檔案，以協助使用者在 Azure 中工作</span><span class="sxs-lookup"><span data-stu-id="f5597-133">*getgoing* we use to share PowerShell script files to facilitate users' work in Azure</span></span>
* <span data-ttu-id="f5597-134">**PARAMETERS** - (保留空白)</span><span class="sxs-lookup"><span data-stu-id="f5597-134">**PARAMETERS** - (leave blank)</span></span>

<span data-ttu-id="f5597-135">最後，按一下勾號，開始建立自訂的 HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="f5597-135">Finally, click the check mark to start the creation of the customized HDInsight Hadoop cluster.</span></span> 

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <span data-ttu-id="f5597-137"><a name="headnode"></a> 存取 Hadoop 叢集的前端節點</span><span class="sxs-lookup"><span data-stu-id="f5597-137"><a name="headnode"></a> Access the Head Node of Hadoop Cluster</span></span>
<span data-ttu-id="f5597-138">您必須先在 Azure 中啟用 Hadoop 叢集的遠端存取，才能透過 RDP 存取 Hadoop 叢集的前端節點。</span><span class="sxs-lookup"><span data-stu-id="f5597-138">You must enable remote access to the Hadoop cluster in Azure before you can access the head node of the Hadoop cluster through RDP.</span></span> 

1. <span data-ttu-id="f5597-139">登入 [**Azure 傳統入口網站**](https://manage.windowsazure.com/)，選取左側的 [HDInsight]，從叢集清單中選取您的 Hadoop 叢集，按一下 [設定] 索引標籤，然後按一下頁面底部的 [啟用遠端] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f5597-139">Log in to the [**Azure classic portal**](https://manage.windowsazure.com/), select **HDInsight** on the left, select your Hadoop cluster from the list of clusters, click the **CONFIGURATION** tab, and then click the **ENABLE REMOTE** icon at the bottom of the page.</span></span>
   
    ![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. <span data-ttu-id="f5597-141">在 [設定遠端桌面]  視窗中，輸入 [使用者名稱] 和 [密碼] 欄位，然後選取遠端存取的到期日。</span><span class="sxs-lookup"><span data-stu-id="f5597-141">In the **Configure Remote Desktop** window, enter the USER NAME and PASSWORD fields, and select the expiration date for remote access.</span></span> <span data-ttu-id="f5597-142">接著，按一下勾號，啟用對 Hadoop 叢集前端節點的遠端存取。</span><span class="sxs-lookup"><span data-stu-id="f5597-142">Then click the check mark to enable the remote access to the head node of the Hadoop cluster.</span></span>
   
    ![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> <span data-ttu-id="f5597-144">適用於遠端存取的使用者名稱和密碼並非您在建立 Hadoop 叢集時所使用的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f5597-144">The user name and password for the remote access are not the user name and password that you use when you created the Hadoop cluster.</span></span> <span data-ttu-id="f5597-145">這是另一組個別的認證。</span><span class="sxs-lookup"><span data-stu-id="f5597-145">This is a separate set of credentials.</span></span> <span data-ttu-id="f5597-146">此外，遠端存取的到期日必須在從目前日期起算的 7 天內。</span><span class="sxs-lookup"><span data-stu-id="f5597-146">Also, the expiration date of the remote access has to be within 7 days from the current date.</span></span>
> 
> 

<span data-ttu-id="f5597-147">啟用遠端存取之後，按一下頁面底部的 [連接]  ，遠端連至前端節點。</span><span class="sxs-lookup"><span data-stu-id="f5597-147">After remote access is enabled, click **CONNECT** at the bottom of the page to remote into the head node.</span></span> <span data-ttu-id="f5597-148">您登入 Hadoop 叢集前端節點的方式是針對稍早指定的遠端存取使用者輸入認證。</span><span class="sxs-lookup"><span data-stu-id="f5597-148">You log on to the head node of the Hadoop cluster by entering the credentials for the remote access user that you specified earlier.</span></span>

![建立工作區](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

<span data-ttu-id="f5597-150">[Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 中說明了進階分析程序的後續步驟，其中可能包含將資料移至 HDInsight 並在其中處理資料與取樣，做為透過 Azure Machine Learning 從資料學習的準備。</span><span class="sxs-lookup"><span data-stu-id="f5597-150">The next steps in the advanced analytics process are mapped in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) and may include steps that move data into HDInsight, then process and sample it there in preparation for learning from the data with Azure Machine Learning.</span></span>

<span data-ttu-id="f5597-151">請參閱[如何提交 Hive 查詢](machine-learning-data-science-move-hive-tables.md#submit)中的相關指示，以了解如何在用來處理儲存於叢集的 Hive 記錄的使用者定義函式 (UDF) 中，從叢集的前端節點存取隨附於 Anaconda 的 Python 模組。</span><span class="sxs-lookup"><span data-stu-id="f5597-151">See [How to submit Hive queries](machine-learning-data-science-move-hive-tables.md#submit) for instructions on how to access the Python modules that are included in Anaconda from the head node of the cluster in user-defined functions (UDFs) that are used to process Hive records stored in the cluster.</span></span>

