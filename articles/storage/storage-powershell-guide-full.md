---
title: "將 Azure PowerShell 與 Azure 儲存體搭配使用 | Microsoft Docs"
description: "了解如何使用適用於 Azure 儲存體的 Azure PowerShell Cmdlet 建立和管理儲存體帳戶；使用 Blob、資料表、佇列和檔案；設定和查詢儲存體分析，並建立共用存取簽章。"
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 51e3e93ebedd31370857e61a00139294bcee9237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="484ab-103">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="484ab-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="484ab-104">Overview</span><span class="sxs-lookup"><span data-stu-id="484ab-104">Overview</span></span>
<span data-ttu-id="484ab-105">Azure PowerShell 是個模組，其提供了各種 Cmdlet 來透過 Windows PowerShell 管理 Azure。</span><span class="sxs-lookup"><span data-stu-id="484ab-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="484ab-106">它是以工作為基礎的命令列殼層和指令碼語言，特別為系統管理所設計。</span><span class="sxs-lookup"><span data-stu-id="484ab-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="484ab-107">使用 PowerShell，您可以輕鬆控制和自動執行 Azure 服務和應用程式的管理。</span><span class="sxs-lookup"><span data-stu-id="484ab-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="484ab-108">例如，您可透過 [Azure 入口網站](https://portal.azure.com)執行的工作，大多也可使用 Cmdlet 來執行。</span><span class="sxs-lookup"><span data-stu-id="484ab-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="484ab-109">在本指南中，我們將探討如何使用 [Azure 儲存體 Cmdlet (英文)](/powershell/module/azurerm.storage/#storage)，來使用 Azure 儲存體執行各種開發和管理工作。</span><span class="sxs-lookup"><span data-stu-id="484ab-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="484ab-110">本指南假設您過去有使用 [Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/)和 [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx) 的經驗。</span><span class="sxs-lookup"><span data-stu-id="484ab-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="484ab-111">本指南提供的一些指令碼示範如何搭配使用 PowerShell 與 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="484ab-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="484ab-112">您應該在執行每個指令碼之前，先根據您的組態更新指令碼變數。</span><span class="sxs-lookup"><span data-stu-id="484ab-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="484ab-113">本指南的第一節提供 Azure 儲存體和 PowerShell 的快速概覽。</span><span class="sxs-lookup"><span data-stu-id="484ab-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="484ab-114">如需詳細資訊和指示，請從 [搭配使用 Azure PowerShell 與 Azure 儲存體的先決條件](#prerequisites-for-using-azure-powershell-with-azure-storage)開始閱讀。</span><span class="sxs-lookup"><span data-stu-id="484ab-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="484ab-115">在 5 分鐘內開始使用 Azure 儲存體和 PowerShell</span><span class="sxs-lookup"><span data-stu-id="484ab-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="484ab-116">本節說明如何在 5 分鐘內透過 PowerShell 存取 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="484ab-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="484ab-117">**Azure 新手：** 取得 Microsoft Azure 訂用帳戶和與該訂用帳戶相關聯的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="484ab-118">如需 Azure 購買選項的資訊，請參閱[免費試用](https://azure.microsoft.com/pricing/free-trial/)、[購買選項](https://azure.microsoft.com/pricing/purchase-options/)和[會員優惠](https://azure.microsoft.com/pricing/member-offers/) (適用於 MSDN、Microsoft 合作夥伴網路、BizSpark 和其他 Microsoft 方案的成員)。</span><span class="sxs-lookup"><span data-stu-id="484ab-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="484ab-119">如需 Azure 訂用帳戶的詳細資訊，請參閱 [在 Azure Active Directory (Azure AD) 中指派系統管理員角色](https://msdn.microsoft.com/library/azure/hh531793.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="484ab-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="484ab-120">**建立 Microsoft Azure 訂用帳戶和帳戶之後：**</span><span class="sxs-lookup"><span data-stu-id="484ab-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="484ab-121">下載並安裝最新的 [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest)。</span><span class="sxs-lookup"><span data-stu-id="484ab-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="484ab-122">啟動 Windows PowerShell 整合式指令碼環境 (ISE)：在本機電腦中移至 [開始]功能表。</span><span class="sxs-lookup"><span data-stu-id="484ab-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="484ab-123">鍵入**系統管理工具**，然後按一下以執行。</span><span class="sxs-lookup"><span data-stu-id="484ab-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="484ab-124">在 [系統管理工具] 視窗中，以滑鼠右鍵按一下 [Windows PowerShell ISE]，按一下 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="484ab-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="484ab-125">在 [Windows PowerShell ISE] 中，按一下 [檔案]  >  [新增]，建立新的指令碼檔。</span><span class="sxs-lookup"><span data-stu-id="484ab-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="484ab-126">現在，我們將提供簡單的指令碼，顯示用以存取 Azure 儲存體的基本 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="484ab-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="484ab-127">此指令碼會先要求您的 Azure 帳戶認證，以將您的 Azure 帳戶新增到本機 PowerShell 環境。</span><span class="sxs-lookup"><span data-stu-id="484ab-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="484ab-128">然後，指令碼會設定預設 Azure 訂用帳戶，並在 Azure 中建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="484ab-129">接著，指令碼將在這個新的儲存體帳戶中建立新容器，並將現有的映像檔案 (Blob) 上傳至該容器。</span><span class="sxs-lookup"><span data-stu-id="484ab-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="484ab-130">指令碼列出該容器中的所有 Blob 之後，它會在本機電腦中建立新的目的地目錄並下載映像檔。</span><span class="sxs-lookup"><span data-stu-id="484ab-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="484ab-131">在下列程式碼區段中，選取 **#begin** 和 **#end** 備註之間的指令碼。</span><span class="sxs-lookup"><span data-stu-id="484ab-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="484ab-132">按 CTRL+C 將它複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="484ab-132">Press CTRL+C to copy it to the clipboard.</span></span>

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="484ab-133">在 [Windows PowerShell ISE] 中，按 CTRL+V 以複製指令碼。</span><span class="sxs-lookup"><span data-stu-id="484ab-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="484ab-134">按一下 檔案 > 儲存。</span><span class="sxs-lookup"><span data-stu-id="484ab-134">Click **File** > **Save**.</span></span> <span data-ttu-id="484ab-135">在 [另存新檔] 對話方塊視窗中，輸入指令碼檔的名稱，例如 "mystoragescript"。</span><span class="sxs-lookup"><span data-stu-id="484ab-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="484ab-136">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="484ab-136">Click **Save**.</span></span>
7. <span data-ttu-id="484ab-137">現在，您需要根據您的組態設定更新指令碼變數。</span><span class="sxs-lookup"><span data-stu-id="484ab-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="484ab-138">您必須使用自己的訂用帳戶更新 **$SubscriptionName** 變數。</span><span class="sxs-lookup"><span data-stu-id="484ab-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="484ab-139">您可以保留指令碼中指定的其他變數或視需要予以更新。</span><span class="sxs-lookup"><span data-stu-id="484ab-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="484ab-140">**$SubscriptionName：** 您必須使用自己的訂用帳戶名稱更新此變數。</span><span class="sxs-lookup"><span data-stu-id="484ab-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="484ab-141">依照下列其中一個方式執行，即可找出您的訂用帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="484ab-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="484ab-142">a.</span><span class="sxs-lookup"><span data-stu-id="484ab-142">a.</span></span> <span data-ttu-id="484ab-143">在 [Windows PowerShell ISE] 中，按一下 [檔案]  >  [新增]，建立新的指令碼檔。</span><span class="sxs-lookup"><span data-stu-id="484ab-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="484ab-144">將下列指令碼複製到新的指令碼檔，然後按一下 [偵錯]  >  [執行]。</span><span class="sxs-lookup"><span data-stu-id="484ab-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="484ab-145">下列指令碼會先要求您的 Azure 帳戶認證，以將您的 Azure 帳戶新增到本機 PowerShell 環境，然後顯示連接到本機 PowerShell 工作階段的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="484ab-146">請記下遵循此教學課程時，您所要使用的訂用帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="484ab-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="484ab-147">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="484ab-147">b.</span></span> <span data-ttu-id="484ab-148">若要在 [Azure 入口網站](https://portal.azure.com)中尋找並複製您的訂用帳戶名稱，請按一下左側 [中樞] 功能表，再按一下 [訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="484ab-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="484ab-149">複製您想要在執行本指南中的指令碼時使用的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="484ab-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Azure 入口網站](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="484ab-151">c.</span><span class="sxs-lookup"><span data-stu-id="484ab-151">c.</span></span> <span data-ttu-id="484ab-152">若要在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中尋找並複製您的訂用帳戶名稱，請向下捲動並按一下入口網站左側的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="484ab-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="484ab-153">按一下 [訂用帳戶] 以查看您的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="484ab-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="484ab-154">複製您想要在執行本指南中提供的指令碼時使用的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="484ab-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![Azure 傳統入口網站](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="484ab-156">**$StorageAccountName：** 使用指令碼中的指定名稱，或是為儲存體帳戶輸入新名稱。</span><span class="sxs-lookup"><span data-stu-id="484ab-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="484ab-157">**重要事項：** 儲存體帳戶的名稱在 Azure 中必須是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="484ab-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="484ab-158">而且必須是小寫字母！</span><span class="sxs-lookup"><span data-stu-id="484ab-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="484ab-159">**$Location：** 使用指令碼中指定的「美國西部」，或選擇其他的 Azure 地點，例如美國東部、北歐等。</span><span class="sxs-lookup"><span data-stu-id="484ab-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="484ab-160">**$ContainerName：** 使用指令碼中的指定名稱，或是為容器輸入新名稱。</span><span class="sxs-lookup"><span data-stu-id="484ab-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="484ab-161">**$ImageToUpload：**輸入位於本機電腦上的圖片路徑，例如 "C:\Images\HelloWorld.png"。</span><span class="sxs-lookup"><span data-stu-id="484ab-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="484ab-162">**$DestinationFolder：**輸入本機目錄的路徑，以儲存從 Azure 儲存體下載的檔案，例如 "C:\DownloadImages"。</span><span class="sxs-lookup"><span data-stu-id="484ab-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="484ab-163">更新 "mystoragescript.ps1" 檔案中的指令碼變數之後，請按一下 [檔案]  >  [儲存]。</span><span class="sxs-lookup"><span data-stu-id="484ab-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="484ab-164">按一下 [偵錯]  > 執行或按 [F5]，以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="484ab-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="484ab-165">在指令碼執行之後，您應該有包含下載的映像檔案的本機目的資料夾。</span><span class="sxs-lookup"><span data-stu-id="484ab-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="484ab-166">以下螢幕擷取畫面顯示範例輸出︰</span><span class="sxs-lookup"><span data-stu-id="484ab-166">The following screenshot shows an example output:</span></span>

![下載 Blob](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="484ab-168">「在 5 分鐘內開始使用 Azure 儲存體和 PowerShell」一節提供有關如何搭配使用 Azure PowerShell 與 Azure 儲存體的快速簡介。</span><span class="sxs-lookup"><span data-stu-id="484ab-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="484ab-169">如需詳細資訊和指示，我們鼓勵您閱讀下列各節。</span><span class="sxs-lookup"><span data-stu-id="484ab-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="484ab-170">搭配使用 Azure PowerShell 與 Azure 儲存體的先決條件</span><span class="sxs-lookup"><span data-stu-id="484ab-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="484ab-171">您需要有 Azure 訂用帳戶和帳戶，才能如上面說明的方法執行本指南提供的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="484ab-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="484ab-172">Azure PowerShell 是個模組，其提供了各種 Cmdlet 來透過 Windows PowerShell 管理 Azure。</span><span class="sxs-lookup"><span data-stu-id="484ab-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="484ab-173">如需安裝和設定 Azure PowerShell 的資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="484ab-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="484ab-174">建議您在使用本指南之前，先下載並安裝或升級至最新的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="484ab-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="484ab-175">您可以在標準 Windows PowerShell 主控台，或是 Windows PowerShell 整合式指令碼環境 (ISE) 中執行 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="484ab-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="484ab-176">若要開啟 [Windows PowerShell ISE] ，請移至 [開始] 功能表、輸入「系統管理工具」，然後按一下加以執行。</span><span class="sxs-lookup"><span data-stu-id="484ab-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="484ab-177">在 [系統管理工具] 視窗中，以滑鼠右鍵按一下 [Windows PowerShell ISE]，按一下 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="484ab-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="484ab-178">如何在 Azure 中管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="484ab-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="484ab-179">讓我們看看如何使用 PowerShell 在 Azure 中管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="484ab-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="484ab-180">如何設定預設 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="484ab-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="484ab-181">若要使用 Azure PowerShell 管理 Azure 儲存體，您需要透過 Azure Active Directory 驗證或憑證型驗證向 Azure 驗證用戶端環境。</span><span class="sxs-lookup"><span data-stu-id="484ab-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="484ab-182">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="484ab-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="484ab-183">本指南使用 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="484ab-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="484ab-184">在 Windows PowerShell ISE 中，輸入下列命令，將您的 Azure 帳戶新增到本機的 PowerShell 環境：</span><span class="sxs-lookup"><span data-stu-id="484ab-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="484ab-185">在 [登入 Microsoft Azure] 視窗中，輸入與您的帳戶相關聯的電子郵件地址及密碼。</span><span class="sxs-lookup"><span data-stu-id="484ab-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="484ab-186">Azure 會驗證並儲存認證資訊，然後關閉視窗。</span><span class="sxs-lookup"><span data-stu-id="484ab-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="484ab-187">接著，執行下列命令以檢視本機 PowerShell 環境的 Azure 帳戶，並確認您的帳戶已列出：</span><span class="sxs-lookup"><span data-stu-id="484ab-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="484ab-188">然後，執行下列 Cmdlet 可檢視已連接到本機 PowerShell 工作階段的所有訂用帳戶，並確認您的訂用帳戶已列出：</span><span class="sxs-lookup"><span data-stu-id="484ab-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="484ab-189">若要設定預設 Azure 訂用帳戶，請執行 Select-azuresubscription Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="484ab-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="484ab-190">執行 Get-azuresubscription Cmdlet 來確認預設訂用帳戶的名稱：</span><span class="sxs-lookup"><span data-stu-id="484ab-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="484ab-191">若要查看 Azure 儲存體的所有可用 PowerShell Cmdlet，請執行：</span><span class="sxs-lookup"><span data-stu-id="484ab-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="484ab-192">如何建立新的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="484ab-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="484ab-193">若要使用 Azure 儲存體，您將需要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="484ab-194">設定電腦以連接至您的訂用帳戶之後，您可以建立新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="484ab-195">執行 Get-azurelocation Cmdlet 來尋找所有可用的資料中心位置：</span><span class="sxs-lookup"><span data-stu-id="484ab-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="484ab-196">接著，執行 New-AzureStorageAccount Cmdlet 來建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="484ab-197">下列範例會在「美國西部」資料中心建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="484ab-198">儲存體帳戶的名稱在 Azure 中必須是獨一無二的且必須小寫。</span><span class="sxs-lookup"><span data-stu-id="484ab-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="484ab-199">如需命名慣例與限制，請參閱[關於 Azure 儲存體帳戶](storage-create-storage-account.md)和[命名和參考容器、Blob 及中繼資料](http://msdn.microsoft.com/library/azure/dd135715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="484ab-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="484ab-200">如何設定預設 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="484ab-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="484ab-201">您可以在訂用帳戶中有多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="484ab-202">您可以選擇其中一個儲存體帳戶，並將它設為相同 PowerShell 工作階段中所有儲存體命令的預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="484ab-203">這可讓您執行 Azure PowerShell 儲存體命令，而不需明確指定儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="484ab-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="484ab-204">若要設定您的訂用帳戶的預設儲存體帳戶，您可以執行 Set-azuresubscription Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="484ab-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="484ab-205">接著，執行 Get-azuresubscription Cmdlet 來確認儲存體帳戶與預設訂用帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="484ab-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="484ab-206">這個命令會傳回目前訂用帳戶的訂用帳戶屬性，包括其目前的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="484ab-207">如何列出訂用帳戶中的所有 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="484ab-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="484ab-208">每個 Azure 訂用帳戶可以擁有高達 100 個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="484ab-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="484ab-209">如需最新的限制資訊，請參閱 [Azure 訂用帳戶和服務限制、配額及條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="484ab-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="484ab-210">執行下列 Cmdlet 來找出目前訂用帳戶中儲存體帳戶的名稱和狀態：</span><span class="sxs-lookup"><span data-stu-id="484ab-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="484ab-211">如何建立 Azure 儲存體內容</span><span class="sxs-lookup"><span data-stu-id="484ab-211">How to create an Azure storage context</span></span>
<span data-ttu-id="484ab-212">Azure 儲存體內容是 PowerShell 中用以封裝儲存體認證的物件。</span><span class="sxs-lookup"><span data-stu-id="484ab-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="484ab-213">在執行任何後續 Cmdlet 時使用儲存體內容，可讓您驗證您的要求，而不需明確指定儲存體帳戶和其存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="484ab-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="484ab-214">您可以用很多方式建立儲存體內容，例如使用儲存體帳戶名稱和存取金鑰、共用存取簽章 (SAS) 權杖、連接字串或匿名。</span><span class="sxs-lookup"><span data-stu-id="484ab-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="484ab-215">如需詳細資訊，請參閱 [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext)。</span><span class="sxs-lookup"><span data-stu-id="484ab-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="484ab-216">使用下列三種方式之一來建立儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="484ab-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="484ab-217">執行 [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) Cmdlet 可找出 Azure 儲存體帳戶的主要儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="484ab-217">Run the [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="484ab-218">接著，呼叫 [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) Cmdlet，以建立儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="484ab-218">Next, call the [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="484ab-219">產生 Azure 儲存體容器的共用存取簽章權杖，並用來它建立儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="484ab-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="484ab-220">如需詳細資訊，請參閱 [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) 和[使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="484ab-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="484ab-221">在某些情況下，您可能想要在建立新的儲存體內容時指定服務端點。</span><span class="sxs-lookup"><span data-stu-id="484ab-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="484ab-222">當您向 Blob 服務註冊儲存體帳戶的自訂網域名稱，或想要使用共用存取簽章存取儲存體資源時，這可能是必要作業。</span><span class="sxs-lookup"><span data-stu-id="484ab-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="484ab-223">在連接字串中設定服務端點，並用來建立新的儲存體內容，如下所示：</span><span class="sxs-lookup"><span data-stu-id="484ab-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="484ab-224">如需如何設定儲存體連接字串的詳細資訊，請參閱 [設定連接字串](storage-configure-connection-string.md)。</span><span class="sxs-lookup"><span data-stu-id="484ab-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="484ab-225">您現已設定您的電腦並學會如何使用 Azure PowerShell 管理訂用帳戶和儲存體帳戶，請移至下一節，以了解如何管理 Azure Blob 和 Blob 快照集。</span><span class="sxs-lookup"><span data-stu-id="484ab-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="484ab-226">如何擷取和重新產生 Azure 儲存體金鑰</span><span class="sxs-lookup"><span data-stu-id="484ab-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="484ab-227">Azure 儲存體帳戶會隨附兩個帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="484ab-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="484ab-228">您可以使用下列 Cmdlet 來擷取您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="484ab-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="484ab-229">使用下列 Cmdlet 來擷取特定的金鑰。</span><span class="sxs-lookup"><span data-stu-id="484ab-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="484ab-230">有效值為 Primary 和 Secondary。</span><span class="sxs-lookup"><span data-stu-id="484ab-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="484ab-231">如果您想要重新產生金鑰，請使用下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="484ab-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="484ab-232">-KeyType 的有效值為 "Primary" 和 "Secondary"</span><span class="sxs-lookup"><span data-stu-id="484ab-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="484ab-233">如何管理 Azure blob</span><span class="sxs-lookup"><span data-stu-id="484ab-233">How to manage Azure blobs</span></span>
<span data-ttu-id="484ab-234">Azure Blob 儲存體是一項儲存大量非結構化資料的服務 (例如文字或二進位資料)，全球任何地方都可透過 HTTP 或 HTTPS 來存取這些資料。</span><span class="sxs-lookup"><span data-stu-id="484ab-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="484ab-235">本節假設您已熟悉 Azure Blob 儲存體服務概念。</span><span class="sxs-lookup"><span data-stu-id="484ab-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="484ab-236">如需詳細資訊，請參閱[以 .NET 開始使用 Blob 儲存體](storage-dotnet-how-to-use-blobs.md)和 [Blob 服務概念](http://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="484ab-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="484ab-237">如何建立容器</span><span class="sxs-lookup"><span data-stu-id="484ab-237">How to create a container</span></span>
<span data-ttu-id="484ab-238">Azure 儲存體中的每個 Blob 必須位於一個容器中。</span><span class="sxs-lookup"><span data-stu-id="484ab-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="484ab-239">您可以使用 New-AzureStorageContainer Cmdlet 建立私用容器：</span><span class="sxs-lookup"><span data-stu-id="484ab-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="484ab-240">匿名讀取權限有三個層級：**Off**、**Blob** 和 **Container**。</span><span class="sxs-lookup"><span data-stu-id="484ab-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="484ab-241">若要防止匿名存取 Blob，請將 Permission 參數設定為 **Off**。</span><span class="sxs-lookup"><span data-stu-id="484ab-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="484ab-242">新容器預設為私人，且只能由帳戶擁有者存取。</span><span class="sxs-lookup"><span data-stu-id="484ab-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="484ab-243">若要允許 Blob 資源的匿名公開讀取權限，但不允許容器中繼資料或容器中 Blob 清單的匿名公開讀取權限，請將 Permission 參數設定為 **Blob**。</span><span class="sxs-lookup"><span data-stu-id="484ab-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="484ab-244">若要允許 Blob 資源、容器中繼資料或容器中 Blob 清單的完整公開讀取權限，請將 Permission 參數設定為 **Container**。</span><span class="sxs-lookup"><span data-stu-id="484ab-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="484ab-245">如需詳細資訊，請參閱 [管理對容器與 Blob 的匿名讀取權限](storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="484ab-245">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="484ab-246">如何將 Blob 上傳到容器中</span><span class="sxs-lookup"><span data-stu-id="484ab-246">How to upload a blob into a container</span></span>
<span data-ttu-id="484ab-247">Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="484ab-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="484ab-248">如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。</span><span class="sxs-lookup"><span data-stu-id="484ab-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="484ab-249">若要將 Blob 上傳至容器，您可以使用 [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="484ab-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="484ab-250">根據預設，此命令會將本機檔案上傳至區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="484ab-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="484ab-251">若要指定 Blob 的類型，您可以使用 -BlobType 參數。</span><span class="sxs-lookup"><span data-stu-id="484ab-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="484ab-252">下列範例會執行 [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) Cmdlet 以取得指定資料夾中的所有檔案，然後使用管線運算子將這些檔案傳遞至下一個 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="484ab-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="484ab-253">[Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) Cmdlet 會將本機檔案上傳至您的容器：</span><span class="sxs-lookup"><span data-stu-id="484ab-253">The [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="484ab-254">如何從容器下載 Blob</span><span class="sxs-lookup"><span data-stu-id="484ab-254">How to download blobs from a container</span></span>
<span data-ttu-id="484ab-255">下列範例示範如何從容器下載 Blob。</span><span class="sxs-lookup"><span data-stu-id="484ab-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="484ab-256">此範例會先使用儲存體帳戶內容建立 Azure 儲存體的連線，其中包含儲存體帳戶名稱及其主要存取金鑰 。</span><span class="sxs-lookup"><span data-stu-id="484ab-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="484ab-257">然後使用 [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Cmdlet 擷取 Blob 參照。</span><span class="sxs-lookup"><span data-stu-id="484ab-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="484ab-258">接著再使用 [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) Cmdlet 將 Blob 下載到本機目的地資料夾中。</span><span class="sxs-lookup"><span data-stu-id="484ab-258">Next, the example uses the [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet to download blobs into the local destination folder.</span></span>

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="484ab-259">如何在儲存體容器之間複製 Blob</span><span class="sxs-lookup"><span data-stu-id="484ab-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="484ab-260">您可以跨儲存體帳戶和區域以非同步方式複製 Blob。</span><span class="sxs-lookup"><span data-stu-id="484ab-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="484ab-261">下列範例示範如何在兩個不同的儲存體帳戶中將 Blob 從一個儲存體容器複製到另一個儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="484ab-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="484ab-262">此範例會先設定來源和目的地儲存體帳戶的變數，然後建立每個帳戶的儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="484ab-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="484ab-263">接著再使用 [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) Cmdlet 將 Blob 從來源容器複製到目的地容器。</span><span class="sxs-lookup"><span data-stu-id="484ab-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="484ab-264">此範例假設來源和目的地儲存體帳戶和容器已經存在。</span><span class="sxs-lookup"><span data-stu-id="484ab-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="484ab-265">請注意，此範例會執行非同步複製。</span><span class="sxs-lookup"><span data-stu-id="484ab-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="484ab-266">您可以透過執行 [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) Cmdlet，監視每個副本的狀態。</span><span class="sxs-lookup"><span data-stu-id="484ab-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="484ab-267">如何從次要位置複製 Blob</span><span class="sxs-lookup"><span data-stu-id="484ab-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="484ab-268">您可以從支援 RA-GRS 之帳戶的次要位置複製 Blob。</span><span class="sxs-lookup"><span data-stu-id="484ab-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="484ab-269">如何刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="484ab-269">How to delete a blob</span></span>
<span data-ttu-id="484ab-270">若要刪除 Blob，請先取得 Blob 參考，然後在該參考上呼叫 Remove-AzureStorageBlob Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="484ab-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="484ab-271">下列範例會刪除指定的容器中的所有 Blob。</span><span class="sxs-lookup"><span data-stu-id="484ab-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="484ab-272">此範例會先設定儲存體帳戶的變數，然後建立儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="484ab-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="484ab-273">接著再使用 [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Cmdlet 擷取 Blob 參照，並執行 [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) Cmdlet，以從 Azure 儲存體中的容器移除 Blob。</span><span class="sxs-lookup"><span data-stu-id="484ab-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet to remove blobs from a container in Azure storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="484ab-274">如何管理 Azure Blob 快照集</span><span class="sxs-lookup"><span data-stu-id="484ab-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="484ab-275">Azure 可讓您建立 Blob 的快照集。</span><span class="sxs-lookup"><span data-stu-id="484ab-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="484ab-276">快照集是在某個點時間取得的唯讀 Blob 版本。</span><span class="sxs-lookup"><span data-stu-id="484ab-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="484ab-277">一旦建立快照集後，即可加以讀取、複製或刪除，但不能修改。</span><span class="sxs-lookup"><span data-stu-id="484ab-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="484ab-278">快照集提供在某個時間點備份 Blob 的方法。</span><span class="sxs-lookup"><span data-stu-id="484ab-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="484ab-279">如需詳細資訊，請參閱 [建立 Blob 的快照集](http://msdn.microsoft.com/library/azure/hh488361.aspx)。</span><span class="sxs-lookup"><span data-stu-id="484ab-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="484ab-280">如何建立 Blob 快照集</span><span class="sxs-lookup"><span data-stu-id="484ab-280">How to create a blob snapshot</span></span>
<span data-ttu-id="484ab-281">若要建立 Blob 的快照，請先取得 Blob 參照，然後在該參考上呼叫 `ICloudBlob.CreateSnapshot` 方法。</span><span class="sxs-lookup"><span data-stu-id="484ab-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="484ab-282">下列範例會先設定儲存體帳戶的變數，然後建立儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="484ab-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="484ab-283">接著再使用 [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Cmdlet 擷取 Blob 參考，並執行 [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) 方法建立快照。</span><span class="sxs-lookup"><span data-stu-id="484ab-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="484ab-284">如何列出 Blob 的快照</span><span class="sxs-lookup"><span data-stu-id="484ab-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="484ab-285">您可以對 Blob 建立您所需數量的快照集。</span><span class="sxs-lookup"><span data-stu-id="484ab-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="484ab-286">您可以列出與 Blob 相關聯的快照集，以追蹤目前的快照集。</span><span class="sxs-lookup"><span data-stu-id="484ab-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="484ab-287">下列範例會使用預先定義的 Blob，並呼叫 [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Cmdlet 以列出該 Blob 的快照。</span><span class="sxs-lookup"><span data-stu-id="484ab-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="484ab-288">如何複製 Blob 的快照集</span><span class="sxs-lookup"><span data-stu-id="484ab-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="484ab-289">您可以複製 Blob 的快照集以還原該快照集。</span><span class="sxs-lookup"><span data-stu-id="484ab-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="484ab-290">如需詳細的資訊及限制，請參閱 [建立 Blob 的快照集](http://msdn.microsoft.com/library/azure/hh488361.aspx)。</span><span class="sxs-lookup"><span data-stu-id="484ab-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="484ab-291">下列範例會先設定儲存體帳戶的變數，然後建立儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="484ab-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="484ab-292">接著，此範例會定義容器和 Blob 名稱變數。</span><span class="sxs-lookup"><span data-stu-id="484ab-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="484ab-293">然後使用 [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Cmdlet 擷取 Blob 參考，並執行 [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) 方法建立快照。</span><span class="sxs-lookup"><span data-stu-id="484ab-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="484ab-294">再執行 [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) Cmdlet，並使用來源 Blob 的 ICloudBlob 物件複製 Blob 的快照。</span><span class="sxs-lookup"><span data-stu-id="484ab-294">Then, the example runs the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="484ab-295">執行此範例前，請務必根據您的組態更新變更。</span><span class="sxs-lookup"><span data-stu-id="484ab-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="484ab-296">請注意，下列範例假設來源和目的地容器和來源 Blob 已經存在。</span><span class="sxs-lookup"><span data-stu-id="484ab-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="484ab-297">現在，您已學會如何使用 Azure PowerShell 管理 Azure Blob 和 Blob 快照集，請移至下一節，以了解如何管理資料表、佇列和檔案。</span><span class="sxs-lookup"><span data-stu-id="484ab-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="484ab-298">如何管理 Azure 資料表和資料表實體</span><span class="sxs-lookup"><span data-stu-id="484ab-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="484ab-299">Azure 資料表儲存體服務是 NoSQL 資料存放區，您可以用來儲存和查詢龐大的結構化、非關聯式資料集。</span><span class="sxs-lookup"><span data-stu-id="484ab-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="484ab-300">服務的主要元件是資料表、實體和屬性。</span><span class="sxs-lookup"><span data-stu-id="484ab-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="484ab-301">資料表是一組實體。</span><span class="sxs-lookup"><span data-stu-id="484ab-301">A table is a collection of entities.</span></span> <span data-ttu-id="484ab-302">實體是一組屬性。</span><span class="sxs-lookup"><span data-stu-id="484ab-302">An entity is a set of properties.</span></span> <span data-ttu-id="484ab-303">每個實體最多可有 252 個屬性，也就是所有的名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="484ab-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="484ab-304">本節假設您已熟悉 Azure 資料表儲存體服務概念。</span><span class="sxs-lookup"><span data-stu-id="484ab-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="484ab-305">如需詳細資訊，請參閱[了解表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)和[以 .NET 開始使用 Azure 資料表儲存體](storage-dotnet-how-to-use-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="484ab-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="484ab-306">在下列小節中，您將學習如何使用 Azure PowerShell 管理 Azure 資料表儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="484ab-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="484ab-307">涵蓋的狀況包括**建立**、**刪除**和**擷取****資料表**，以及**新增**、**查詢**和**刪除資料表實體**。</span><span class="sxs-lookup"><span data-stu-id="484ab-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="484ab-308">如何建立資料表</span><span class="sxs-lookup"><span data-stu-id="484ab-308">How to create a table</span></span>
<span data-ttu-id="484ab-309">每個資料表必須位於 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="484ab-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="484ab-310">下列範例示範如何在 Azure 儲存體中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="484ab-311">此範例會先使用儲存體帳戶內容建立 Azure 儲存體的連線，其中包含儲存體帳戶名稱及其存取金鑰 。</span><span class="sxs-lookup"><span data-stu-id="484ab-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="484ab-312">接著再使用 [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) Cmdlet 在 Azure 儲存體中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-312">Next, it uses the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="484ab-313">如何擷取資料表</span><span class="sxs-lookup"><span data-stu-id="484ab-313">How to retrieve a table</span></span>
<span data-ttu-id="484ab-314">您可以查詢和擷取儲存體帳戶中的一個或所有資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="484ab-315">下列範例示範如何使用 [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) Cmdlet 擷取指定的資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="484ab-316">如果您未使用任何參數呼叫 Get-AzureStorageTable Cmdlet，它會取得儲存體帳戶的所有儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="484ab-317">如何刪除資料表</span><span class="sxs-lookup"><span data-stu-id="484ab-317">How to delete a table</span></span>
<span data-ttu-id="484ab-318">您可以使用 [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) Cmdlet 刪除儲存體帳戶中的資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="484ab-319">如何管理資料表實體</span><span class="sxs-lookup"><span data-stu-id="484ab-319">How to manage table entities</span></span>
<span data-ttu-id="484ab-320">目前，Azure PowerShell 不會提供 Cmdlet 來直接管理資料表實體。</span><span class="sxs-lookup"><span data-stu-id="484ab-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="484ab-321">若要在資料表實體上執行作業，您可以使用 [適用於 .NET 的 Azure 儲存體用戶端程式庫](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx)中提供的類別。</span><span class="sxs-lookup"><span data-stu-id="484ab-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="484ab-322">如何新增資料表實體</span><span class="sxs-lookup"><span data-stu-id="484ab-322">How to add table entities</span></span>
<span data-ttu-id="484ab-323">若要將實體新增至資料表，請先建立一個可定義實體屬性的物件。</span><span class="sxs-lookup"><span data-stu-id="484ab-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="484ab-324">實體最多可有 255 個屬性，包括 3 個系統屬性：**PartitionKey**、**RowKey** 和 **Timestamp**。</span><span class="sxs-lookup"><span data-stu-id="484ab-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="484ab-325">您需負責插入及更新 **PartitionKey** 和 **RowKey** 的值。</span><span class="sxs-lookup"><span data-stu-id="484ab-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="484ab-326">伺服器會管理 **Timestamp**的值，該值無法予以修改。</span><span class="sxs-lookup"><span data-stu-id="484ab-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="484ab-327">**PartitionKey** 和 **RowKey** 的組合可唯一識別資料表內的每個實體。</span><span class="sxs-lookup"><span data-stu-id="484ab-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="484ab-328">**PartitionKey**：決定儲存實體的資料分割。</span><span class="sxs-lookup"><span data-stu-id="484ab-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="484ab-329">**RowKey**：在資料分割內唯一地識別實體。</span><span class="sxs-lookup"><span data-stu-id="484ab-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="484ab-330">您可以為每個實體最多定義 252 個自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="484ab-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="484ab-331">如需詳細資訊，請參閱 [了解表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="484ab-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="484ab-332">下列範例示範如何將實體加入至資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="484ab-333">此範例示範如何擷取員工資料表並在其中加入數個項實體。</span><span class="sxs-lookup"><span data-stu-id="484ab-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="484ab-334">首先，它會先使用儲存體帳戶內容建立 Azure 儲存體的連線，其中包含儲存體帳戶名稱及其存取金鑰 。</span><span class="sxs-lookup"><span data-stu-id="484ab-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="484ab-335">接著，再使用 [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) Cmdlet 擷取指定的資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-335">Next, it retrieves the given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="484ab-336">如果資料表不存在，可使用 [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) Cmdlet 在 Azure 儲存體中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-336">If the table does not exist, the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="484ab-337">接下來，此範例會定義 Add-Entity 自訂函數，經由指定每個實體的分割區和資料列索引鍵，將實體加入至資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="484ab-338">Add-Entity 函數會在 [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) 類別上呼叫 [New-Object](http://technet.microsoft.com/library/hh849885.aspx) Cmdlet，以建立實體物件。</span><span class="sxs-lookup"><span data-stu-id="484ab-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="484ab-339">之後，此範例會在此實體物件上呼叫 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) 方法，以將它加入資料表中。</span><span class="sxs-lookup"><span data-stu-id="484ab-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity to a table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="484ab-340">如何查詢資料表實體</span><span class="sxs-lookup"><span data-stu-id="484ab-340">How to query table entities</span></span>
<span data-ttu-id="484ab-341">若要查詢資料表，請使用 [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) 類別。</span><span class="sxs-lookup"><span data-stu-id="484ab-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="484ab-342">下列範例假設您已執行本指南＜如何新增實體＞一節中所提供的指令碼。</span><span class="sxs-lookup"><span data-stu-id="484ab-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="484ab-343">此範例會先使用儲存體內容建立 Azure 儲存體的連線，其中包含儲存體帳戶名稱及其存取金鑰 。</span><span class="sxs-lookup"><span data-stu-id="484ab-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="484ab-344">接著，它會使用 [Get-AzureStorageTable (英文)](/powershell/module/azure.storage/get-azurestoragetable) Cmdlet 嘗試擷取先前建立的「員工」資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="484ab-345">在 Microsoft.WindowsAzure.Storage.Table.TableQuery 類別上呼叫 [New-Object](http://technet.microsoft.com/library/hh849885.aspx) Cmdlet，可建立新的查詢物件。</span><span class="sxs-lookup"><span data-stu-id="484ab-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="484ab-346">此範例會尋找 'ID' 資料行的值為 1 (如字串篩選條件中指定) 的實體。</span><span class="sxs-lookup"><span data-stu-id="484ab-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="484ab-347">如需詳細資訊，請參閱 [查詢資料表和實體](http://msdn.microsoft.com/library/azure/dd894031.aspx)。</span><span class="sxs-lookup"><span data-stu-id="484ab-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="484ab-348">當您執行此查詢時，它會傳回所有符合篩選準則的所有實體。</span><span class="sxs-lookup"><span data-stu-id="484ab-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="484ab-349">如何刪除資料表實體</span><span class="sxs-lookup"><span data-stu-id="484ab-349">How to delete table entities</span></span>
<span data-ttu-id="484ab-350">您可以使用實體的資料分割和資料列索引鍵來刪除實體。</span><span class="sxs-lookup"><span data-stu-id="484ab-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="484ab-351">下列範例假設您已執行本指南＜如何新增實體＞一節中所提供的指令碼。</span><span class="sxs-lookup"><span data-stu-id="484ab-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="484ab-352">此範例會先使用儲存體內容建立 Azure 儲存體的連線，其中包含儲存體帳戶名稱及其存取金鑰 。</span><span class="sxs-lookup"><span data-stu-id="484ab-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="484ab-353">接著，它會使用 [Get-AzureStorageTable (英文)](/powershell/module/azure.storage/get-azurestoragetable) Cmdlet 嘗試擷取先前建立的「員工」資料表。</span><span class="sxs-lookup"><span data-stu-id="484ab-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="484ab-354">如果資料表已存在，則會呼叫 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) 方法，根據資料分割及資料列索引鍵的值擷取實體。</span><span class="sxs-lookup"><span data-stu-id="484ab-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="484ab-355">然後，將實體傳遞至 [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) 方法加以刪除。</span><span class="sxs-lookup"><span data-stu-id="484ab-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="484ab-356">如何管理 Azure 佇列和佇列訊息</span><span class="sxs-lookup"><span data-stu-id="484ab-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="484ab-357">Azure 佇列儲存體是一項儲存大量訊息的服務，全球任何地方都可利用 HTTP 或 HTTPS 並透過驗證的呼叫來存取這些訊息。</span><span class="sxs-lookup"><span data-stu-id="484ab-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="484ab-358">本節假設您已熟悉 Azure 佇列儲存體服務概念。</span><span class="sxs-lookup"><span data-stu-id="484ab-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="484ab-359">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="484ab-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="484ab-360">本節將示範如何使用 Azure PowerShell 來管理 Azure 佇列儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="484ab-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="484ab-361">涵蓋的狀況包括**插入**和**刪除**佇列訊息，以及**建立**、**刪除**和**擷取**佇列。</span><span class="sxs-lookup"><span data-stu-id="484ab-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="484ab-362">如何建立佇列</span><span class="sxs-lookup"><span data-stu-id="484ab-362">How to create a queue</span></span>
<span data-ttu-id="484ab-363">下列範例會先使用儲存體帳戶內容建立 Azure 儲存體的連線，其中包含儲存體帳戶名稱及其存取金鑰 。</span><span class="sxs-lookup"><span data-stu-id="484ab-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="484ab-364">接著，它會呼叫 [New-AzureStorageQueue (英文)](/powershell/module/azure.storage/new-azurestoragequeue) Cmdlet 以建立名為 'queuename' 的佇列。</span><span class="sxs-lookup"><span data-stu-id="484ab-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="484ab-365">如需 Azure 佇列服務命名慣例的資訊，請參閱 [為佇列和中繼資料命名](http://msdn.microsoft.com/library/azure/dd179349.aspx)。</span><span class="sxs-lookup"><span data-stu-id="484ab-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="484ab-366">如何擷取佇列</span><span class="sxs-lookup"><span data-stu-id="484ab-366">How to retrieve a queue</span></span>
<span data-ttu-id="484ab-367">您可以查詢與擷取儲存體帳戶中的特定佇列或所有佇列清單。</span><span class="sxs-lookup"><span data-stu-id="484ab-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="484ab-368">下列範例示範如何使用 [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) Cmdlet 擷取指定的佇列。</span><span class="sxs-lookup"><span data-stu-id="484ab-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="484ab-369">如果您未使用任何參數，直接呼叫 [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) Cmdlet，會取得所有佇列的清單。</span><span class="sxs-lookup"><span data-stu-id="484ab-369">If you call the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="484ab-370">如何刪除佇列</span><span class="sxs-lookup"><span data-stu-id="484ab-370">How to delete a queue</span></span>
<span data-ttu-id="484ab-371">若要刪除佇列及其內含的所有訊息，請呼叫 Remove-AzureStorageQueue Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="484ab-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="484ab-372">下列範例示範如何使用 Remove-AzureStorageQueue Cmdlet 刪除指定的佇列。</span><span class="sxs-lookup"><span data-stu-id="484ab-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="484ab-373">如何將訊息插入佇列中</span><span class="sxs-lookup"><span data-stu-id="484ab-373">How to insert a message into a queue</span></span>
<span data-ttu-id="484ab-374">若要將訊息插入現有佇列中，請先建立 [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) 類別的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="484ab-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="484ab-375">接著，呼叫 [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) 方法。</span><span class="sxs-lookup"><span data-stu-id="484ab-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="484ab-376">您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 CloudQueueMessage。</span><span class="sxs-lookup"><span data-stu-id="484ab-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="484ab-377">下列範例示範如何將訊息加入佇列中。</span><span class="sxs-lookup"><span data-stu-id="484ab-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="484ab-378">此範例會先使用儲存體帳戶內容建立 Azure 儲存體的連線，其中包含儲存體帳戶名稱及其存取金鑰 。</span><span class="sxs-lookup"><span data-stu-id="484ab-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="484ab-379">接著，再使用 [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) Cmdlet 擷取指定的佇列。</span><span class="sxs-lookup"><span data-stu-id="484ab-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="484ab-380">如果佇列存在，可使用 [New-Object](http://technet.microsoft.com/library/hh849885.aspx) Cmdlet 建立 [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="484ab-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="484ab-381">之後，此範例會在此訊息物件上呼叫 [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) 方法，以將其加入佇列。</span><span class="sxs-lookup"><span data-stu-id="484ab-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="484ab-382">以下是可擷取佇列及插入訊息「MessageInfo」的程式碼：</span><span class="sxs-lookup"><span data-stu-id="484ab-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="484ab-383">如何在下一個訊息中清除佇列</span><span class="sxs-lookup"><span data-stu-id="484ab-383">How to de-queue at the next message</span></span>
<span data-ttu-id="484ab-384">您的程式碼可以使用兩個步驟將訊息自佇列中清除佇列。</span><span class="sxs-lookup"><span data-stu-id="484ab-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="484ab-385">當您呼叫 [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) 方法，會取得佇列中的下一個訊息。</span><span class="sxs-lookup"><span data-stu-id="484ab-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="484ab-386">從 **GetMessage** 傳回的訊息，對於從此佇列讀取訊息的任何其他程式碼而言將會是不可見的。</span><span class="sxs-lookup"><span data-stu-id="484ab-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="484ab-387">若要完成從佇列移除訊息的動作，您還必須呼叫 [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) 方法。</span><span class="sxs-lookup"><span data-stu-id="484ab-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="484ab-388">這個移除訊息的兩步驟程序可確保您的程式碼因為硬體或軟體故障而無法處理訊息時，另一個程式碼的執行個體可以取得相同訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="484ab-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="484ab-389">您的程式碼會在處理完訊息之後立即呼叫 **DeleteMessage** 。</span><span class="sxs-lookup"><span data-stu-id="484ab-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="484ab-390">如何管理 Azure 檔案共用和檔案</span><span class="sxs-lookup"><span data-stu-id="484ab-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="484ab-391">Azure 檔案儲存體為使用標準 SMB 通訊協定的應用程式提供共用儲存體。</span><span class="sxs-lookup"><span data-stu-id="484ab-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="484ab-392">Microsoft Azure 虛擬機器和雲端服務可以透過掛接的共用，在應用程式元件之間共用檔案資料，而內部部署應用程式可以透過檔案儲存體 API 或 Azure PowerShell，存取共用中的檔案資料。</span><span class="sxs-lookup"><span data-stu-id="484ab-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="484ab-393">如需 Azure 檔案儲存體的詳細資訊，請參閱[在 Windows 上開始使用 Azure 檔案儲存體](storage-dotnet-how-to-use-files.md)和[檔案服務 REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx)。</span><span class="sxs-lookup"><span data-stu-id="484ab-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="484ab-394">如何設定及查詢儲存體分析</span><span class="sxs-lookup"><span data-stu-id="484ab-394">How to set and query storage analytics</span></span>
<span data-ttu-id="484ab-395">您可以使用 [Azure 儲存體分析](storage-analytics.md) 收集 Azure 儲存體帳戶的計量，以及傳送至儲存體帳戶之要求的相關記錄資料。</span><span class="sxs-lookup"><span data-stu-id="484ab-395">You can use [Azure Storage Analytics](storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="484ab-396">也可以使用儲存體計量監視儲存體帳戶的健康狀態，並使用儲存體記錄診斷和疑難排解儲存體帳戶的問題。</span><span class="sxs-lookup"><span data-stu-id="484ab-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="484ab-397">若要設定監視，可以使用 Azure 入口網站或 Windows PowerShell，或使用儲存體用戶端程式庫以程式設計方式進行。</span><span class="sxs-lookup"><span data-stu-id="484ab-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="484ab-398">系統會在伺服器端執行儲存體記錄，這可讓您在儲存體帳戶中記錄成功和失敗要求的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="484ab-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="484ab-399">這些記錄檔可讓您查看資料表、佇列和 Blob 的讀取、寫入和刪除作業詳細資料，以及失敗要求的原因。</span><span class="sxs-lookup"><span data-stu-id="484ab-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="484ab-400">若要了解如何使用 PowerShell 啟用和檢視儲存體計量的資料，請參閱 [如何使用 PowerShell 啟用儲存體度量](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell)。</span><span class="sxs-lookup"><span data-stu-id="484ab-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="484ab-401">若要了解如何使用 PowerShell 啟用和擷取儲存體記錄的資料，請參閱[如何使用 PowerShell 啟用儲存體記錄](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell)和[尋找儲存體記錄的記錄資料](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata)。</span><span class="sxs-lookup"><span data-stu-id="484ab-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="484ab-402">如需使用儲存體計量和儲存體記錄疑難排解儲存體問題的詳細資訊，請參閱 [監控、診斷和疑難排解 Microsoft Azure 儲存體](storage-monitoring-diagnosing-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="484ab-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="484ab-403">如何管理共用存取簽章 (SAS) 和預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="484ab-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="484ab-404">對於任何使用 Azure 儲存體的應用程式而言，共用存取簽章是安全性模型不可或缺的一部分。</span><span class="sxs-lookup"><span data-stu-id="484ab-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="484ab-405">若要提供您儲存體帳戶的有限權限給沒有帳戶金鑰的用戶端，它們是非常有用的方式。</span><span class="sxs-lookup"><span data-stu-id="484ab-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="484ab-406">根據預設，只有儲存體帳戶的擁有者可以存取該帳戶內的 Blob、資料表和佇列。</span><span class="sxs-lookup"><span data-stu-id="484ab-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="484ab-407">如果您的服務或應用程式需要將這些資源提供給其他用戶端使用，而不共用存取金鑰，您會有下列三個選項：</span><span class="sxs-lookup"><span data-stu-id="484ab-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="484ab-408">設定容器的權限，以允許對容器及其 Blob 進行匿名的讀取存取。</span><span class="sxs-lookup"><span data-stu-id="484ab-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="484ab-409">這不適用於資料表或佇列。</span><span class="sxs-lookup"><span data-stu-id="484ab-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="484ab-410">使用共用存取簽章，可針對特定的時間間隔，授與容器、Blob、佇列和資料表有限的存取權限。</span><span class="sxs-lookup"><span data-stu-id="484ab-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="484ab-411">使用預存的存取原則，針對容器或其 Blob、佇列或資料表的共用存取簽章取得一層額外控制。</span><span class="sxs-lookup"><span data-stu-id="484ab-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="484ab-412">預存的存取原則讓您能夠變更開始時間、到期時間或簽章的權限，或者在發出之後將它撤銷。</span><span class="sxs-lookup"><span data-stu-id="484ab-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="484ab-413">共用存取簽章可以是下列其中一種格式：</span><span class="sxs-lookup"><span data-stu-id="484ab-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="484ab-414">**臨機操作 SAS**：當您建立臨機操作的 SAS 時，SAS 的開始時間、到期時間和權限全都標示在 SAS URI 上。</span><span class="sxs-lookup"><span data-stu-id="484ab-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="484ab-415">您可以在容器、Blob、資料表或佇列上建立此類型的 SAS，而且無法撤銷它。</span><span class="sxs-lookup"><span data-stu-id="484ab-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="484ab-416">**具有預存存取原則的 SAS**：預存存取原則是在資源容器、Blob 容器、資料表或佇列中定義，且可用來管理一或多個共用存取簽章的條件約束。</span><span class="sxs-lookup"><span data-stu-id="484ab-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="484ab-417">當您將 SAS 與預存存取原則建立關聯時，SAS 會繼承為該預存存取原則所定義的限制 (開始時間、過期時間和權限)。</span><span class="sxs-lookup"><span data-stu-id="484ab-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="484ab-418">這種類型的 SAS 是可撤銷的。</span><span class="sxs-lookup"><span data-stu-id="484ab-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="484ab-419">如需詳細資訊，請參閱[使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 和[管理對容器與 Blob 的匿名讀取權限](storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="484ab-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="484ab-420">在下一節中，您將了解如何為 Azure 資料表建立共用存取簽章權杖和預存的存取原則。</span><span class="sxs-lookup"><span data-stu-id="484ab-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="484ab-421">Azure PowerShell 也會為容器、Blob 和佇列提供類似的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="484ab-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="484ab-422">若要執行本節中的指令碼，請下載 [Azure PowerShell 0.8.14 版](http://go.microsoft.com/?linkid=9811175&clcid=0x409) 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="484ab-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="484ab-423">如何建立原則式共用存取簽章權杖</span><span class="sxs-lookup"><span data-stu-id="484ab-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="484ab-424">使用 New-AzureStorageTableStoredAccessPolicy Cmdlet 來建立新的預存存取原則。</span><span class="sxs-lookup"><span data-stu-id="484ab-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="484ab-425">然後呼叫 [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) Cmdlet，為 Azure 儲存體資料表建立新的原則式共用存取簽章權杖。</span><span class="sxs-lookup"><span data-stu-id="484ab-425">Then, call the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="484ab-426">如何建立臨機操作 (無法撤銷) 的共用存取簽章權杖</span><span class="sxs-lookup"><span data-stu-id="484ab-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="484ab-427">[New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) Cmdlet 可為 Azure 儲存體資料表建立新的臨機操作 (無法撤銷) 的共用存取簽章權杖：</span><span class="sxs-lookup"><span data-stu-id="484ab-427">Use the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="484ab-428">如何建立預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="484ab-428">How to create a stored access policy</span></span>
<span data-ttu-id="484ab-429">使用 New-AzureStorageTableStoredAccessPolicy Cmdlet，為 Azure 儲存體資料表建立新的預存存取原則：</span><span class="sxs-lookup"><span data-stu-id="484ab-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="484ab-430">如何更新預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="484ab-430">How to update a stored access policy</span></span>
<span data-ttu-id="484ab-431">使用 Set-AzureStorageTableStoredAccessPolicy Cmdlet，為 Azure 儲存體資料表更新現有的預存存取原則：</span><span class="sxs-lookup"><span data-stu-id="484ab-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="484ab-432">如何刪除預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="484ab-432">How to delete a stored access policy</span></span>
<span data-ttu-id="484ab-433">使用 Remove-AzureStorageTableStoredAccessPolicy Cmdlet，在 Azure 儲存體資料表上刪除預存的存取原則：</span><span class="sxs-lookup"><span data-stu-id="484ab-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="484ab-434">如何使用適用於美國政府和 Azure China 的 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="484ab-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="484ab-435">Azure 環境是 Microsoft Azure 的獨立部署，例如[適用於美國政府的 Azure Government](https://azure.microsoft.com/features/gov/)、[適用於全球 Azure 的 AzureCloud](https://portal.azure.com) 和[由中國世紀互聯運作的 AzureChinaCloud for Azure](http://www.windowsazure.cn/)。</span><span class="sxs-lookup"><span data-stu-id="484ab-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="484ab-436">您可以針對美國政府與 Azure 中國部署新的 Azure 環境。</span><span class="sxs-lookup"><span data-stu-id="484ab-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="484ab-437">若要搭配使用 Azure 儲存體與 AzureChinaCloud，您需要建立與 AzureChinaCloud 相關聯的儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="484ab-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="484ab-438">遵循下列步驟，以便開始使用產品：</span><span class="sxs-lookup"><span data-stu-id="484ab-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="484ab-439">執行 [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) Cmdlet，查看可用的 Azure 環境：</span><span class="sxs-lookup"><span data-stu-id="484ab-439">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="484ab-440">將 Azure China 帳戶新增至 Windows PowerShell：</span><span class="sxs-lookup"><span data-stu-id="484ab-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="484ab-441">建立 AzureChinaCloud 帳戶的儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="484ab-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="484ab-442">若要將 Azure 儲存體與[適用於美國政府的 Azure Government ](https://azure.microsoft.com/features/gov/) 搭配使用，請定義一個新環境，然後在此環境中建立新的儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="484ab-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="484ab-443">執行 [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) Cmdlet，查看可用的 Azure 環境：</span><span class="sxs-lookup"><span data-stu-id="484ab-443">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="484ab-444">將 Azure 美國政府帳戶新增至 Windows PowerShell：</span><span class="sxs-lookup"><span data-stu-id="484ab-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="484ab-445">建立 AzureUSGovernment 帳戶的儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="484ab-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="484ab-446">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="484ab-446">For more information, see:</span></span>

* <span data-ttu-id="484ab-447">[Microsoft Azure Government 開發人員指南](../azure-government-developer-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="484ab-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="484ab-448">在 China 服務上建立應用程式時差異的概觀</span><span class="sxs-lookup"><span data-stu-id="484ab-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="484ab-449">後續步驟</span><span class="sxs-lookup"><span data-stu-id="484ab-449">Next Steps</span></span>
<span data-ttu-id="484ab-450">在本指南，您已了解如何使用 Azure PowerShell 管理 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="484ab-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="484ab-451">以下是有助於您深入了解的一些相關文章和資源。</span><span class="sxs-lookup"><span data-stu-id="484ab-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="484ab-452">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="484ab-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="484ab-453">Azure 儲存體 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="484ab-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="484ab-454">Windows PowerShell 參考</span><span class="sxs-lookup"><span data-stu-id="484ab-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
