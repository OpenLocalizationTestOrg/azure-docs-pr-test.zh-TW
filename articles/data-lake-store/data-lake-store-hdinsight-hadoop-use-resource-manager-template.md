---
title: "aaaUse Azure 範本 toocreate HDInsight 及資料湖存放區 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本 toocreate 和使用 Azure Data Lake Store 的 HDInsight 叢集"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="a759d-103">使用 Azure Resource Manager 範本來建立搭配 Data Lake Store 的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="a759d-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a759d-104">使用入口網站</span><span class="sxs-lookup"><span data-stu-id="a759d-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="a759d-105">使用 PowerShell (針對預設儲存體)</span><span class="sxs-lookup"><span data-stu-id="a759d-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="a759d-106">使用 PowerShell (針對額外儲存體)</span><span class="sxs-lookup"><span data-stu-id="a759d-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="a759d-107">使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a759d-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="a759d-108">了解如何 toouse Azure PowerShell tooconfigure 在 HDInsight 叢集與 Azure 資料湖存放區**做為額外的儲存體**。</span><span class="sxs-lookup"><span data-stu-id="a759d-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="a759d-109">Data Lake Store 對於支援的叢集類型，是做為預設儲存體或額外儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a759d-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="a759d-110">資料湖存放區是作為額外的存放裝置，hello hello 叢集的預設儲存體帳戶仍會 Azure 儲存體 Blob (WASB) 和受 hello 叢集相關的檔案 （例如記錄檔等） 仍會寫入 toohello 預設儲存體，hello 資料時，您想 tooprocess 可以儲存在 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a759d-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="a759d-111">使用資料湖存放區做為額外的儲存體帳戶不會影響效能或 hello 能力 tooread/寫入 toohello 叢集中存放裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="a759d-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="a759d-112">針對 HDInsight 叢集儲存體使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a759d-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="a759d-113">以下是使用 HDInsight 搭配 Data Lake Store 的一些重要考量：</span><span class="sxs-lookup"><span data-stu-id="a759d-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="a759d-114">選項 toocreate HDInsight 叢集，以存取做為預設儲存體 tooData Lake Store 適用於 HDInsight 版本 3.5 和 3.6。</span><span class="sxs-lookup"><span data-stu-id="a759d-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="a759d-115">選項 toocreate HDInsight 叢集的存取是適用於 HDInsight 版本 3.2、 3.4、 3.5 和 3.6 tooData 湖存放區做為額外的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="a759d-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="a759d-116">在本文中，我們佈建 Hadoop 叢集與 Data Lake Store 做為額外的儲存體。</span><span class="sxs-lookup"><span data-stu-id="a759d-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="a759d-117">如需有關如何 toocreate Hadoop 叢集做為預設儲存體的資料湖存放區的指示，請參閱[建立與使用 Azure 入口網站的 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a759d-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a759d-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="a759d-118">Prerequisites</span></span>
<span data-ttu-id="a759d-119">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="a759d-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="a759d-120">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a759d-120">**An Azure subscription**.</span></span> <span data-ttu-id="a759d-121">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a759d-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a759d-122">**Azure PowerShell 1.0 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="a759d-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="a759d-123">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a759d-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="a759d-124">**Azure Active Directory 服務主體**。</span><span class="sxs-lookup"><span data-stu-id="a759d-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="a759d-125">本教學課程步驟提供如何指示 toocreate Azure AD 中的服務主體。</span><span class="sxs-lookup"><span data-stu-id="a759d-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="a759d-126">不過，您必須是 Azure AD 管理員 toobe 無法 toocreate 服務主體。</span><span class="sxs-lookup"><span data-stu-id="a759d-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="a759d-127">如果您是 Azure AD 管理員，則可以略過這項必要條件，並繼續進行 hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="a759d-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="a759d-128">**如果您不是 Azure AD 管理員**，就能 tooperform hello 步驟需要的 toocreate 服務主體。</span><span class="sxs-lookup"><span data-stu-id="a759d-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="a759d-129">在這樣的情況下，您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a759d-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="a759d-130">此外，hello 服務主體必須建立使用的認證，依照[建立服務主體與憑證](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)。</span><span class="sxs-lookup"><span data-stu-id="a759d-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="a759d-131">建立搭配 Azure Data Lake Store 的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="a759d-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="a759d-132">hello Resource Manager 範本，並使用 hello 範本 hello 必要條件可用在 GitHub 上[部署新的 Data Lake Store 的 HDInsight Linux 叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage)。</span><span class="sxs-lookup"><span data-stu-id="a759d-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="a759d-133">請遵循隨附於此連結 toocreate 的 HDInsight 叢集為 hello 額外的儲存體的 Azure Data Lake Store 的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="a759d-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="a759d-134">在上述的 hello 連結 hello 指示需要 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a759d-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="a759d-135">您開始使用這些指示之前，請確定您登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a759d-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="a759d-136">從您的桌面，開啟新的 Azure PowerShell 視窗，並輸入下列程式碼片段的 hello。</span><span class="sxs-lookup"><span data-stu-id="a759d-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="a759d-137">當提示的 toolog 中，請確定您登入做為其中一個 hello 訂用帳戶 admininistrators/擁有者：</span><span class="sxs-lookup"><span data-stu-id="a759d-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="a759d-138">上傳範例資料 toohello Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a759d-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="a759d-139">hello Resource Manager 範本建立新的 Data Lake Store 帳戶，並將其與 hello HDInsight 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="a759d-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="a759d-140">現在，您必須上傳某些範例資料 toohello 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="a759d-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="a759d-141">您將需要這項資料稍後從 HDInsight 叢集 hello 教學課程 toorun 作業，存取 hello 資料湖存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="a759d-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="a759d-142">如需有關指示 tooupload 資料，請參閱 <<c0> [ 上傳檔案 tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata)。</span><span class="sxs-lookup"><span data-stu-id="a759d-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="a759d-143">如果您要尋找的一些範例資料 tooupload，您可以取得 hello**政策救護車資料**資料夾從 hello [Azure 資料湖 Git 儲存機制](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData)。</span><span class="sxs-lookup"><span data-stu-id="a759d-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="a759d-144">Hello 範例資料設定相關的 Acl</span><span class="sxs-lookup"><span data-stu-id="a759d-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="a759d-145">toomake 確認可從 hello HDInsight 叢集存取您上傳的 hello 範例資料，您必須確定是使用的 tooestablish hello HDInsight 叢集與資料湖存放區之間的身分識別的 hello Azure AD 應用程式具有存取 toohello 檔案/資料夾嘗試 tooaccess。</span><span class="sxs-lookup"><span data-stu-id="a759d-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="a759d-146">toodo，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="a759d-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="a759d-147">尋找 hello 的 hello 與 HDInsight 叢集相關聯的 Azure AD 應用程式和 hello 資料湖存放區的名稱。</span><span class="sxs-lookup"><span data-stu-id="a759d-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="a759d-148">其中一種方式 toolook hello 名稱是 tooopen hello HDInsight 叢集刀鋒視窗使用 hello Resource Manager 範本所建立，請按一下 hello**叢集 AAD 身分識別**索引標籤，然後尋找 hello 值**服務主體顯示名稱**。</span><span class="sxs-lookup"><span data-stu-id="a759d-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="a759d-149">現在，提供存取 toothis Azure AD 應用程式上 hello 檔案/資料夾的 tooaccess 從 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a759d-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="a759d-150">tooset hello 右邊 Acl hello 檔案/資料夾資料湖存放區中，請參閱[保護資料湖存放區中的資料](data-lake-store-secure-data.md#filepermissions)。</span><span class="sxs-lookup"><span data-stu-id="a759d-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="a759d-151">Hello HDInsight 叢集 toouse hello 資料湖存放區上執行測試工作</span><span class="sxs-lookup"><span data-stu-id="a759d-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="a759d-152">您已設定的 HDInsight 叢集之後，您可以測試工作上執行 hello 叢集 tootest 該 hello HDInsight 叢集可以存取資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="a759d-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="a759d-153">toodo 因此，我們會執行使用您上傳先前 tooyour Data Lake Store 的 hello 範例資料建立資料表的範例 Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="a759d-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="a759d-154">本節中您將 SSH 成 HDInsight Linux 叢集和執行的 hello 範例 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="a759d-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="a759d-155">如果您是使用 Windows 用戶端，建議使用 **PuTTY**，您可以從下列位置下載： [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。</span><span class="sxs-lookup"><span data-stu-id="a759d-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="a759d-156">如需使用 PuTTY 的詳細資訊，請參閱 [從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="a759d-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="a759d-157">一旦連接之後，請使用下列命令的 hello 啟動 hello Hive CLI:</span><span class="sxs-lookup"><span data-stu-id="a759d-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="a759d-158">使用 hello CLI 中，輸入下列陳述式 toocreate 名為的新資料表的 hello**車輛**利用 hello 資料湖存放區中的 hello 範例資料：</span><span class="sxs-lookup"><span data-stu-id="a759d-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="a759d-159">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="a759d-159">You should see an output similar toohello following:</span></span>

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="a759d-160">使用 HDFS 命令存取 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a759d-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="a759d-161">一旦您已設定 hello HDInsight 叢集 toouse 資料湖存放區，您可以使用 hello HDFS 殼層命令 tooaccess hello 存放區。</span><span class="sxs-lookup"><span data-stu-id="a759d-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="a759d-162">本節中您將 SSH 成 HDInsight Linux 叢集和執行的 hello HDFS 命令。</span><span class="sxs-lookup"><span data-stu-id="a759d-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="a759d-163">如果您是使用 Windows 用戶端，建議使用 **PuTTY**，您可以從下列位置下載： [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。</span><span class="sxs-lookup"><span data-stu-id="a759d-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="a759d-164">如需使用 PuTTY 的詳細資訊，請參閱 [從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="a759d-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="a759d-165">一旦連接之後，請使用下列 HDFS 檔案系統命令 toolist hello 檔案 hello 資料湖存放區中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a759d-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="a759d-166">這應該會列出您上傳先前 toohello Data Lake Store 的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a759d-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="a759d-167">您也可以使用 hello`hdfs dfs -put`命令 tooupload 某些檔案 toohello 資料湖存放區，然後再使用`hdfs dfs -ls`tooverify 是否 hello 檔案已成功上傳。</span><span class="sxs-lookup"><span data-stu-id="a759d-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a759d-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a759d-168">Next steps</span></span>
* [<span data-ttu-id="a759d-169">從 Azure 儲存體 Blob tooData 湖存放區複製資料</span><span class="sxs-lookup"><span data-stu-id="a759d-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
