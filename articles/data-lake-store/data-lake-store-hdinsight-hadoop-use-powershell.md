---
title: "PowerShell：Azure HDInsight 叢集搭配 Data Lake Store 做為附加儲存體 | Microsoft Docs"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/08/2017
ms.author: nitinme
ms.openlocfilehash: 7a7069adab5742a9dae2833c13a1db57337a41a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="b4675-102">使用 Azure PowerShell 建立 HDInsight 叢集搭配 Data Lake Store (做為附加儲存體)</span><span class="sxs-lookup"><span data-stu-id="b4675-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4675-103">使用入口網站</span><span class="sxs-lookup"><span data-stu-id="b4675-103">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="b4675-104">使用 PowerShell (針對預設儲存體)</span><span class="sxs-lookup"><span data-stu-id="b4675-104">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="b4675-105">使用 PowerShell (針對額外儲存體)</span><span class="sxs-lookup"><span data-stu-id="b4675-105">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="b4675-106">使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b4675-106">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="b4675-107">了解如何使用 Azure PowerShell 將搭配 Azure Data Lake Store 的 HDInsight 叢集設定為**額外儲存體**。</span><span class="sxs-lookup"><span data-stu-id="b4675-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="b4675-108">如需有關如何建立具 Azure Data Lake Store 的 HDInsight 叢集做為預設儲存體的指示，請參閱[建立具有 Data Lake Store 的 HDInsight 叢集做為預設儲存體](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="b4675-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b4675-109">如果您即將使用 Azure Data Lake Store 作為 HDInsight 叢集的額外儲存體，強烈建議您如本文所述建立叢集時執行此作業。</span><span class="sxs-lookup"><span data-stu-id="b4675-109">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="b4675-110">將 Azure Data Lake Store 新增為現有 HDInsight 叢集的額外儲存體是很複雜的程序，很容易出錯。</span><span class="sxs-lookup"><span data-stu-id="b4675-110">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

<span data-ttu-id="b4675-111">Data Lake Store 對於支援的叢集類型，是做為預設儲存體或額外儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4675-111">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="b4675-112">當 Data Lake Store 做為額外儲存體時，叢集的預設儲存體帳戶仍然是 Azure 儲存體 Blob (WASB)，叢集相關的檔案 (例如記錄檔等) 仍然會寫入預設儲存體，而您想要處理的資料會儲存於 Data Lake Store 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="b4675-112">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="b4675-113">使用 Data Lake Store 做為其他儲存體帳戶，不會影響效能或從叢集讀取/寫入至儲存體的能力。</span><span class="sxs-lookup"><span data-stu-id="b4675-113">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="b4675-114">針對 HDInsight 叢集儲存體使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b4675-114">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="b4675-115">以下是使用 HDInsight 搭配 Data Lake Store 的一些重要考量：</span><span class="sxs-lookup"><span data-stu-id="b4675-115">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="b4675-116">HDInsight 3.2、3.4、3.5 和 3.6 版提供建立可存取 Data Lake Store 作為額外儲存體之 HDInsight 叢集的選項。</span><span class="sxs-lookup"><span data-stu-id="b4675-116">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="b4675-117">使用 PowerShell 以設定 HDInsight 來搭配 Data Lake Store 使用，包含下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b4675-117">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span></span>

* <span data-ttu-id="b4675-118">建立 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b4675-118">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="b4675-119">設定 Data Lake Store 以角色為基礎的存取的驗證</span><span class="sxs-lookup"><span data-stu-id="b4675-119">Set up authentication for role-based access to Data Lake Store</span></span>
* <span data-ttu-id="b4675-120">建立具有 Data Lake Store 驗證的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="b4675-120">Create HDInsight cluster with authentication to Data Lake Store</span></span>
* <span data-ttu-id="b4675-121">在叢集上執行測試工作</span><span class="sxs-lookup"><span data-stu-id="b4675-121">Run a test job on the cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4675-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="b4675-122">Prerequisites</span></span>
<span data-ttu-id="b4675-123">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="b4675-123">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="b4675-124">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="b4675-124">**An Azure subscription**.</span></span> <span data-ttu-id="b4675-125">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b4675-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b4675-126">**Azure PowerShell 1.0 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="b4675-126">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="b4675-127">請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b4675-127">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b4675-128">**Windows SDK**。</span><span class="sxs-lookup"><span data-stu-id="b4675-128">**Windows SDK**.</span></span> <span data-ttu-id="b4675-129">您可以從[這裡](https://dev.windows.com/en-us/downloads)安裝它。</span><span class="sxs-lookup"><span data-stu-id="b4675-129">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="b4675-130">您使用它來建立安全性憑證。</span><span class="sxs-lookup"><span data-stu-id="b4675-130">You use this to create a security certificate.</span></span>
* <span data-ttu-id="b4675-131">**Azure Active Directory 服務主體**。</span><span class="sxs-lookup"><span data-stu-id="b4675-131">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="b4675-132">本教學課程中的步驟提供有關如何在 Azure AD 中建立服務主體的指示。</span><span class="sxs-lookup"><span data-stu-id="b4675-132">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="b4675-133">不過，您必須是 Azure AD 系統管理員，才能建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="b4675-133">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="b4675-134">如果您是 Azure AD 系統管理員，您就可以略過這項先決條件並繼續進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="b4675-134">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="b4675-135">**如果您不是 Azure AD 系統管理員**，您將無法執行建立服務主體所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="b4675-135">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="b4675-136">在這樣的情況下，您的 Azure AD 系統管理員必須先建立服務主體，您才能建立搭配 Data Lake Store 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b4675-136">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="b4675-137">此外，必須使用憑證來建立服務主體，如[使用憑證來建立服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)所述。</span><span class="sxs-lookup"><span data-stu-id="b4675-137">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="b4675-138">建立 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b4675-138">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="b4675-139">依照這些步驟建立 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="b4675-139">Follow these steps to create a Data Lake Store.</span></span>

1. <span data-ttu-id="b4675-140">從您的桌面開啟新的 Azure PowerShell 視窗，並輸入下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="b4675-140">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span></span> <span data-ttu-id="b4675-141">系統提示您登入時，請確定您使用其中一個訂用帳戶管理員/擁有者身分登入：</span><span class="sxs-lookup"><span data-stu-id="b4675-141">When prompted to log in, make sure you log in as one of the subscription administrator/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="b4675-142">如果您在註冊 Data Lake Store 的資源提供者時收到類似 `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` 的錯誤，可能表示您的訂用帳戶不在 Azure Data Lake Store 的允許清單中。</span><span class="sxs-lookup"><span data-stu-id="b4675-142">If you receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` when registering the Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="b4675-143">請遵循這些 [指示](data-lake-store-get-started-portal.md)，確保您會啟用 Azure 訂用帳戶來使用 Data Lake Store 公開預覽版。</span><span class="sxs-lookup"><span data-stu-id="b4675-143">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="b4675-144">Azure Data Lake Store 帳戶與 Azure 資源群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="b4675-144">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="b4675-145">從建立 Azure 資源群組開始。</span><span class="sxs-lookup"><span data-stu-id="b4675-145">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="b4675-146">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="b4675-146">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="b4675-147">建立 Azure Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4675-147">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="b4675-148">您指定的帳戶名稱必須只包含小寫字母和數字。</span><span class="sxs-lookup"><span data-stu-id="b4675-148">The account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="b4675-149">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="b4675-149">You should see an output like the following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. <span data-ttu-id="b4675-150">將一些範例資料上傳至 Azure Data Lake。</span><span class="sxs-lookup"><span data-stu-id="b4675-150">Upload some sample data to Azure Data Lake.</span></span> <span data-ttu-id="b4675-151">我們將在本文稍後使用這個項目來確認資料可以從 HDInsight 叢集存取。</span><span class="sxs-lookup"><span data-stu-id="b4675-151">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="b4675-152">如果您正在尋找一些可上傳的範例資料，您可以從 **Azure Data Lake Git 存放庫** 取得 [Ambulance Data](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData)資料夾。</span><span class="sxs-lookup"><span data-stu-id="b4675-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="b4675-153">設定 Data Lake Store 以角色為基礎的存取的驗證</span><span class="sxs-lookup"><span data-stu-id="b4675-153">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="b4675-154">每一個 Azure 訂用帳戶都與 Azure Active Directory 相關聯。</span><span class="sxs-lookup"><span data-stu-id="b4675-154">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="b4675-155">透過 Azure 傳統入口網站或 Azure Resource Manager API 來存取訂用帳戶資源的使用者與服務，都必須先向 Azure Active Directory 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="b4675-155">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="b4675-156">您可以在 Azure 資源上為 Azure 訂用帳戶和服務指派適當的角色，以授與其存取權限。</span><span class="sxs-lookup"><span data-stu-id="b4675-156">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span>  <span data-ttu-id="b4675-157">對於服務，服務主體會識別 Azure Active Directory (AAD) 中的服務。</span><span class="sxs-lookup"><span data-stu-id="b4675-157">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="b4675-158">本章節將說明如何將 Azure 資源 (您稍早建立的 Azure Data Lake Store 帳戶) 的存取權授與像是 HDInsight 的應用程式服務，方法是建立應用程式的服務主體，並透過 Azure PowerShell 將角色指派給它。</span><span class="sxs-lookup"><span data-stu-id="b4675-158">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span></span>

<span data-ttu-id="b4675-159">若要設定 Azure Data Lake 的 Active Directory 驗證，您必須執行下列工作。</span><span class="sxs-lookup"><span data-stu-id="b4675-159">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span></span>

* <span data-ttu-id="b4675-160">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="b4675-160">Create a self-signed certificate</span></span>
* <span data-ttu-id="b4675-161">在 Azure Active Directory 和服務主體中建立應用程式</span><span class="sxs-lookup"><span data-stu-id="b4675-161">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="b4675-162">建立自我簽署憑證</span><span class="sxs-lookup"><span data-stu-id="b4675-162">Create a self-signed certificate</span></span>
<span data-ttu-id="b4675-163">進行本節中的步驟之前，請確定您已安裝 [Windows SDK](https://dev.windows.com/en-us/downloads)。</span><span class="sxs-lookup"><span data-stu-id="b4675-163">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="b4675-164">您也必須建立一個目錄 (例如 **C:\mycertdir**)，以在其中建立憑證。</span><span class="sxs-lookup"><span data-stu-id="b4675-164">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span></span>

1. <span data-ttu-id="b4675-165">在 PowerShell 視窗中，瀏覽至您安裝 Windows SDK 的位置 (通常是 `C:\Program Files (x86)\Windows Kits\10\bin\x86`)，並使用 [MakeCert][makecert] 公用程式來建立自我簽署的憑證和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="b4675-165">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="b4675-166">使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="b4675-166">Use the following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="b4675-167">系統會提示您輸入私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="b4675-167">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="b4675-168">命令成功執行之後，您應該會在您指定的憑證目錄中看到 **CertFile.cer** 和 **mykey.pvk**。</span><span class="sxs-lookup"><span data-stu-id="b4675-168">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span></span>
2. <span data-ttu-id="b4675-169">使用 [Pvk2Pfx][pvk2pfx] 公用程式將 MakeCert 建立的 .pvk 和 .cer 檔案轉換成 .pfx 檔案。</span><span class="sxs-lookup"><span data-stu-id="b4675-169">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="b4675-170">執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="b4675-170">Run the following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="b4675-171">系統提示時，輸入您稍早指定的私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="b4675-171">When prompted enter the private key password you specified earlier.</span></span> <span data-ttu-id="b4675-172">您針對 **-po** 參數指定的值是與 .pfx 檔案相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="b4675-172">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span></span> <span data-ttu-id="b4675-173">命令成功完成之後，您應該也會在您指定的憑證目錄中看到 CertFile.pfx。</span><span class="sxs-lookup"><span data-stu-id="b4675-173">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="b4675-174">建立 Azure Active Directory 和服務主體</span><span class="sxs-lookup"><span data-stu-id="b4675-174">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="b4675-175">在這一節中，您將執行相關步驟來建立 Azure Active Directory 應用程式的服務主體、指派角色給服務主體，並藉由提供憑證驗證為服務主體。</span><span class="sxs-lookup"><span data-stu-id="b4675-175">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="b4675-176">執行下列命令以在 Azure Active Directory 中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4675-176">Run the following commands to create an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="b4675-177">在 PowerShell 主控台視窗中貼上下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b4675-177">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="b4675-178">請確定您針對 **-DisplayName** 屬性指定的值是唯一的。</span><span class="sxs-lookup"><span data-stu-id="b4675-178">Make sure the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="b4675-179">此外，**-HomePage** 和 **-IdentiferUris** 的值是預留位置值而不會受到驗證。</span><span class="sxs-lookup"><span data-stu-id="b4675-179">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="b4675-180">使用應用程式識別碼建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="b4675-180">Create a service principal using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="b4675-181">將您要從 HDInsight 叢集存取之 Data Lake Store 資料夾和檔案的存取權授與服務主體。</span><span class="sxs-lookup"><span data-stu-id="b4675-181">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span></span> <span data-ttu-id="b4675-182">下列程式碼片段可讓您存取 Data Lake Store 帳戶的根目錄 (您從中複製範例資料檔的位置) 和檔案本身。</span><span class="sxs-lookup"><span data-stu-id="b4675-182">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="b4675-183">建立 HDInsight Linux 叢集搭配 Data Lake Store 做為額外儲存體</span><span class="sxs-lookup"><span data-stu-id="b4675-183">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="b4675-184">在本節中，我們會建立一個 HDInsight Hadoop Linux 叢集搭配 Data Lake Store 做為額外儲存體。</span><span class="sxs-lookup"><span data-stu-id="b4675-184">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="b4675-185">對於此版本，HDInsight 叢集和 Data Lake Store 必須位於相同位置。</span><span class="sxs-lookup"><span data-stu-id="b4675-185">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="b4675-186">開始擷取訂用帳戶租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="b4675-186">Start with retrieving the subscription tenant ID.</span></span> <span data-ttu-id="b4675-187">稍後您將會需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="b4675-187">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="b4675-188">在此版本中，對於 Hadoop 叢集，Data Lake Store 只能做為叢集的額外儲存體。</span><span class="sxs-lookup"><span data-stu-id="b4675-188">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span></span> <span data-ttu-id="b4675-189">預設儲存體仍是 Azure 儲存體 Blob (WASB)。</span><span class="sxs-lookup"><span data-stu-id="b4675-189">The default storage will still be the Azure storage blobs (WASB).</span></span> <span data-ttu-id="b4675-190">所以，我們要先建立叢集所需的儲存體帳戶和儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="b4675-190">So, we'll first create the storage account and storage containers required for the cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="b4675-191">建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b4675-191">Create the HDInsight cluster.</span></span> <span data-ttu-id="b4675-192">使用下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b4675-192">Use the following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="b4675-193">Cmdlet 成功完成後，您應該會看到列出叢集詳細資料的輸出。</span><span class="sxs-lookup"><span data-stu-id="b4675-193">After the cmdlet successfully completes, you should see an output listing the cluster details.</span></span>


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="b4675-194">在 HDInsight 叢集上執行測試工作以使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b4675-194">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="b4675-195">設定 HDInsight 叢集之後，您可以在叢集上執行測試工作，以測試 HDInsight 叢集是否可以存取 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="b4675-195">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="b4675-196">為了完成這個操作，我們將會執行範例 Hive 工作，該工作會使用您稍早上傳至 Data Lake Store 的範例資料建立資料表。</span><span class="sxs-lookup"><span data-stu-id="b4675-196">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="b4675-197">在這一節中，您將透過 SSH 連線到您所建立的 HDInsight Linux 叢集並執行範例 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="b4675-197">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span></span>

* <span data-ttu-id="b4675-198">如果您使用 Windows 用戶端來透過 SSH 連線到叢集，請參閱[從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="b4675-198">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="b4675-199">如果您使用 Linux 用戶端來透過 SSH 連線到叢集，請參閱[從 Linux 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="b4675-199">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="b4675-200">連線之後，使用下列命令來啟動 Hive CLI：</span><span class="sxs-lookup"><span data-stu-id="b4675-200">Once connected, start the Hive CLI by using the following command:</span></span>

        hive
2. <span data-ttu-id="b4675-201">使用 CLI，輸入下列陳述式，以使用 Data Lake Store 中的範例資料來建立名為 **vehicles** 的新資料表：</span><span class="sxs-lookup"><span data-stu-id="b4675-201">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="b4675-202">您應該會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="b4675-202">You should see an output similar to the following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="b4675-203">使用 HDFS 命令存取 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b4675-203">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="b4675-204">一旦您已設定 HDInsight 叢集使用 Data Lake Store，您可以使用 HDFS 殼層命令來存取存放區。</span><span class="sxs-lookup"><span data-stu-id="b4675-204">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="b4675-205">在這一節中，您將透過 SSH 連線到您所建立的 HDInsight Linux 叢集並執行 HDFS 命令。</span><span class="sxs-lookup"><span data-stu-id="b4675-205">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span></span>

* <span data-ttu-id="b4675-206">如果您使用 Windows 用戶端來透過 SSH 連線到叢集，請參閱[從 Windows 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md)。</span><span class="sxs-lookup"><span data-stu-id="b4675-206">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="b4675-207">如果您使用 Linux 用戶端來透過 SSH 連線到叢集，請參閱[從 Linux 在 HDInsight 上搭配使用 SSH 與以 Linux 為基礎的 Hadoop](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="b4675-207">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="b4675-208">連接之後，使用下列 HDFS 檔案系統命令列出 Data Lake Store 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="b4675-208">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="b4675-209">這樣應該會列出您稍早上傳至 Data Lake Store 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b4675-209">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="b4675-210">您也可以使用 `hdfs dfs -put` 命令來將一些檔案上傳至 Data Lake Store，然後使用 `hdfs dfs -ls` 以確認是否成功上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="b4675-210">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="b4675-211">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b4675-211">See Also</span></span>
* [<span data-ttu-id="b4675-212">入口網站：建立 HDInsight 叢集以使用 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b4675-212">Portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
