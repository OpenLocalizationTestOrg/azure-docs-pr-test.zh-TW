---
title: "使用 Azure 範本建立 HDInsight 與 Data Lake Store | Microsoft Docs"
description: "使用 Azure Resource Manager 範本來建立和使用搭配 Azure Data Lake Store 的 HDInsight 叢集"
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
ms.openlocfilehash: 6f43423096f0e74f41afea275e4ec9801dc2cea5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="212c3-103">使用 Azure Resource Manager 範本來建立搭配 Data Lake Store 的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="212c3-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="212c3-104">使用入口網站</span><span class="sxs-lookup"><span data-stu-id="212c3-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="212c3-105">使用 PowerShell (針對預設儲存體)</span><span class="sxs-lookup"><span data-stu-id="212c3-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="212c3-106">使用 PowerShell (針對額外儲存體)</span><span class="sxs-lookup"><span data-stu-id="212c3-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="212c3-107">使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="212c3-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="212c3-108">了解如何使用 Azure PowerShell 將搭配 Azure Data Lake Store 的 HDInsight 叢集設定為「額外儲存體」。</span><span class="sxs-lookup"><span data-stu-id="212c3-108">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="212c3-109">Data Lake Store 對於支援的叢集類型，是做為預設儲存體或額外儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="212c3-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="212c3-110">當 Data Lake Store 做為額外儲存體時，叢集的預設儲存體帳戶仍然是 Azure 儲存體 Blob (WASB)，叢集相關的檔案 (例如記錄檔等) 仍然會寫入預設儲存體，而您想要處理的資料會儲存於 Data Lake Store 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="212c3-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="212c3-111">使用 Data Lake Store 做為其他儲存體帳戶，不會影響效能或從叢集讀取/寫入至儲存體的能力。</span><span class="sxs-lookup"><span data-stu-id="212c3-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="212c3-112">針對 HDInsight 叢集儲存體使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="212c3-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="212c3-113">以下是使用 HDInsight 搭配 Data Lake Store 的一些重要考量：</span><span class="sxs-lookup"><span data-stu-id="212c3-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="212c3-114">HDInsight 3.5 和 3.6 版提供建立可存取 Data Lake Store 作為預設儲存體之 HDInsight 叢集的選項。</span><span class="sxs-lookup"><span data-stu-id="212c3-114">Option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="212c3-115">HDInsight 3.2、3.4、3.5 和 3.6 版提供建立可存取 Data Lake Store 作為額外儲存體之 HDInsight 叢集的選項。</span><span class="sxs-lookup"><span data-stu-id="212c3-115">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="212c3-116">在本文中，我們佈建 Hadoop 叢集與 Data Lake Store 做為額外的儲存體。</span><span class="sxs-lookup"><span data-stu-id="212c3-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="212c3-117">如需有關如何建立以 Data Lake Store 做為預設儲存體之 Hadoop 叢集的指示，請參閱[使用 Azure 入口網站建立搭配 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="212c3-117">For instructions on how to create a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="212c3-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="212c3-118">Prerequisites</span></span>
<span data-ttu-id="212c3-119">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="212c3-119">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="212c3-120">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="212c3-120">**An Azure subscription**.</span></span> <span data-ttu-id="212c3-121">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="212c3-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="212c3-122">**Azure PowerShell 1.0 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="212c3-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="212c3-123">請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="212c3-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="212c3-124">**Azure Active Directory 服務主體**。</span><span class="sxs-lookup"><span data-stu-id="212c3-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="212c3-125">本教學課程中的步驟提供有關如何在 Azure AD 中建立服務主體的指示。</span><span class="sxs-lookup"><span data-stu-id="212c3-125">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="212c3-126">不過，您必須是 Azure AD 系統管理員，才能建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="212c3-126">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="212c3-127">如果您是 Azure AD 系統管理員，您就可以略過這項先決條件並繼續進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="212c3-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="212c3-128">**如果您不是 Azure AD 系統管理員**，您將無法執行建立服務主體所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="212c3-128">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="212c3-129">在這樣的情況下，您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="212c3-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="212c3-130">此外，必須使用憑證來建立服務主體，如[使用憑證來建立服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)所述。</span><span class="sxs-lookup"><span data-stu-id="212c3-130">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="212c3-131">建立搭配 Azure Data Lake Store 的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="212c3-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="212c3-132">GitHub 的[使用新的 Data Lake Store 來部署 HDInsight Linux 叢集](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage)提供了 Resource Manager 範本，以及使用該範本的先決條件。</span><span class="sxs-lookup"><span data-stu-id="212c3-132">The Resource Manager template, and the prerequisites for using the template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="212c3-133">請依照此連結所提供的指示來建立以 Azure Data Lake Store 作為額外儲存體的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="212c3-133">Follow the instructions provided at this link to create an HDInsight cluster with Azure Data Lake Store as the additional storage.</span></span>

<span data-ttu-id="212c3-134">上述連結所提供的指示需要使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="212c3-134">The instructions at the link mentioned above require PowerShell.</span></span> <span data-ttu-id="212c3-135">從這些指示開始著手之前，請確定您已登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="212c3-135">Before you start with those instructions, make sure you log in to your Azure account.</span></span> <span data-ttu-id="212c3-136">從您的桌面開啟新的 Azure PowerShell 視窗，然後輸入下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="212c3-136">From your desktop, open a new Azure PowerShell window, and enter the following snippets.</span></span> <span data-ttu-id="212c3-137">系統提示您登入時，請確定您會使用其中一個訂用帳戶管理員/擁有者身分登入：</span><span class="sxs-lookup"><span data-stu-id="212c3-137">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

```
# Log in to your Azure account
Login-AzureRmAccount

# List all the subscriptions associated to your account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-to-the-azure-data-lake-store"></a><span data-ttu-id="212c3-138">將範例資料上傳到 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="212c3-138">Upload sample data to the Azure Data Lake Store</span></span>
<span data-ttu-id="212c3-139">Resource Manager 範本會建立一個新的 Data Lake Store 帳戶並將它與 HDInsight 叢集建立關聯。</span><span class="sxs-lookup"><span data-stu-id="212c3-139">The Resource Manager template creates a new Data Lake Store account and associates it with the HDInsight cluster.</span></span> <span data-ttu-id="212c3-140">您現在必須將一些範例資料上傳到 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="212c3-140">You must now upload some sample data to the Data Lake Store.</span></span> <span data-ttu-id="212c3-141">稍後在教學課程中，您將需要這項資料，以從會存取 Data Lake Store 中資料的 HDInsight 叢集中執行作業。</span><span class="sxs-lookup"><span data-stu-id="212c3-141">You'll need this data later in the tutorial to run jobs from an HDInsight cluster that access data in the Data Lake Store.</span></span> <span data-ttu-id="212c3-142">如需有關如何上傳資料的指示，請參閱[將檔案上傳至 Data Lake Store](data-lake-store-get-started-portal.md#uploaddata)。</span><span class="sxs-lookup"><span data-stu-id="212c3-142">For instructions on how to upload data, see [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="212c3-143">如果您正在尋找一些可上傳的範例資料，可以從 **Azure Data Lake Git 存放庫** 取得 [Ambulance Data](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData)資料夾。</span><span class="sxs-lookup"><span data-stu-id="212c3-143">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-the-sample-data"></a><span data-ttu-id="212c3-144">在範例資料上設定相關的 ACL</span><span class="sxs-lookup"><span data-stu-id="212c3-144">Set relevant ACLs on the sample data</span></span>
<span data-ttu-id="212c3-145">為了確定可從 HDInsight 叢集存取您上傳的範例資料，您必須確保用來在 HDInsight 叢集與 Data Lake Store 之間建立身分識別的 Azure AD 應用程式能夠存取您嘗試存取的檔案/資料夾。</span><span class="sxs-lookup"><span data-stu-id="212c3-145">To make sure the sample data you upload is accessible from the HDInsight cluster, you must ensure that the Azure AD application that is used to establish identity between the HDInsight cluster and Data Lake Store has access to the file/folder you are trying to access.</span></span> <span data-ttu-id="212c3-146">若要這樣做，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="212c3-146">To do this, perform the following steps.</span></span>

1. <span data-ttu-id="212c3-147">找出與 HDInsight 叢集和 Data Lake Store 關聯的 Azure AD 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="212c3-147">Find the name of the Azure AD application that is associated with HDInsight cluster and the Data Lake Store.</span></span> <span data-ttu-id="212c3-148">其中一個尋找名稱的方法是開啟您使用 Resource Manager 範本來建立的 HDInsight 叢集刀鋒視窗、按一下 [叢集 AAD 識別] 索引標籤，然後尋找 [服務主體顯示名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="212c3-148">One way to look for the name is to open the HDInsight cluster blade that you created using the Resource Manager template, click the **Cluster AAD Identity** tab, and look for the value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="212c3-149">現在，將您想要從 HDInsight 叢集存取之檔案/資料夾的存取權提供給此 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="212c3-149">Now, provide access to this Azure AD application on the file/folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="212c3-150">若要在 Data Lake Store 中的檔案/資料夾上設定正確的 ACL，請參閱[保護 Data Lake Store 中的資料](data-lake-store-secure-data.md#filepermissions)。</span><span class="sxs-lookup"><span data-stu-id="212c3-150">To set the right ACLs on the file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="212c3-151">在 HDInsight 叢集上執行測試工作以使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="212c3-151">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="212c3-152">設定 HDInsight 叢集之後，您可以在叢集上執行測試工作，以測試 HDInsight 叢集是否可以存取 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="212c3-152">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="212c3-153">為了完成這個操作，我們將會執行範例 Hive 工作，該工作會使用您稍早上傳至 Data Lake Store 的範例資料建立資料表。</span><span class="sxs-lookup"><span data-stu-id="212c3-153">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="212c3-154">在這一節中，您會透過 SSH 連線到 HDInsight Linux 叢集並執行範例 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="212c3-154">In this section you will SSH into an HDInsight Linux cluster and run the a sample Hive query.</span></span> <span data-ttu-id="212c3-155">如果您是使用 Windows 用戶端，建議使用 **PuTTY**，您可以從下列位置下載： [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。</span><span class="sxs-lookup"><span data-stu-id="212c3-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="212c3-156">如需使用 PuTTY 的詳細資訊，請參閱 [從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="212c3-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="212c3-157">連線之後，使用下列命令來啟動 Hive CLI：</span><span class="sxs-lookup"><span data-stu-id="212c3-157">Once connected, start the Hive CLI by using the following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="212c3-158">使用 CLI，輸入下列陳述式，以使用 Data Lake Store 中的範例資料來建立名為 **vehicles** 的新資料表：</span><span class="sxs-lookup"><span data-stu-id="212c3-158">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="212c3-159">您應該會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="212c3-159">You should see an output similar to the following:</span></span>

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


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="212c3-160">使用 HDFS 命令存取 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="212c3-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="212c3-161">一旦您已設定 HDInsight 叢集使用 Data Lake Store，您可以使用 HDFS 殼層命令來存取存放區。</span><span class="sxs-lookup"><span data-stu-id="212c3-161">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="212c3-162">在本節中，您會透過 SSH 連線到 HDInsight Linux 叢集並執行 HDFS 命令。</span><span class="sxs-lookup"><span data-stu-id="212c3-162">In this section you will SSH into an HDInsight Linux cluster and run the HDFS commands.</span></span> <span data-ttu-id="212c3-163">如果您是使用 Windows 用戶端，建議使用 **PuTTY**，您可以從下列位置下載： [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)。</span><span class="sxs-lookup"><span data-stu-id="212c3-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="212c3-164">如需使用 PuTTY 的詳細資訊，請參閱 [從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="212c3-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="212c3-165">連線之後，使用下列 HDFS 檔案系統命令列出 Data Lake Store 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="212c3-165">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="212c3-166">這樣應該會列出您稍早上傳至 Data Lake Store 的檔案。</span><span class="sxs-lookup"><span data-stu-id="212c3-166">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="212c3-167">您也可以使用 `hdfs dfs -put` 命令來將一些檔案上傳至 Data Lake Store，然後使用 `hdfs dfs -ls` 以確認是否成功上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="212c3-167">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="212c3-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="212c3-168">Next steps</span></span>
* [<span data-ttu-id="212c3-169">將資料從 Azure 儲存體 Blob 複製到 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="212c3-169">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
