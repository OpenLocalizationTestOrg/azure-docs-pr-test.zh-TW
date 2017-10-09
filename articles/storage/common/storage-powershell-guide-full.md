---
title: "與 Azure 儲存體的 Azure PowerShell aaaUsing |Microsoft 文件"
description: "了解 toouse hello 適用於 Azure 儲存體 toocreate Azure PowerShell cmdlet，並管理儲存體帳戶。使用 blob、 資料表、 佇列和檔案。設定並查詢儲存體分析，並建立共用的存取簽章。"
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
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="934c5-103">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="934c5-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="934c5-104">概觀</span><span class="sxs-lookup"><span data-stu-id="934c5-104">Overview</span></span>
<span data-ttu-id="934c5-105">Azure PowerShell 是提供 cmdlet toomanage 透過 Windows PowerShell 的 Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="934c5-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="934c5-106">它是以工作為基礎的命令列殼層和指令碼語言，特別為系統管理所設計。</span><span class="sxs-lookup"><span data-stu-id="934c5-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="934c5-107">使用 PowerShell，您可以輕鬆地控制及自動化 hello 管理您的 Azure 服務和應用程式。</span><span class="sxs-lookup"><span data-stu-id="934c5-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="934c5-108">例如，您可以使用相同的工作，您可以執行透過 hello hello cmdlet tooperform hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="934c5-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="934c5-109">本指南中，我們將探討如何 toouse hello [Azure 儲存體 Cmdlet](/powershell/module/azurerm.storage/#storage) tooperform 各種開發和管理工作與 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="934c5-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="934c5-110">本指南假設您過去有使用 [Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/)和 [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx) 的經驗。</span><span class="sxs-lookup"><span data-stu-id="934c5-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="934c5-111">hello 指南提供的指令碼數目 toodemonstrate hello PowerShell 與 Azure 儲存體使用量。</span><span class="sxs-lookup"><span data-stu-id="934c5-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="934c5-112">您應該更新 hello 指令碼變數，根據您的設定，才能執行每個指令碼。</span><span class="sxs-lookup"><span data-stu-id="934c5-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="934c5-113">本指南中的 hello 第一節提供 Azure 儲存體和 PowerShell 快速概覽。</span><span class="sxs-lookup"><span data-stu-id="934c5-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="934c5-114">如需詳細的資訊和指示，請從 hello 啟動[與 Azure 儲存體使用 Azure PowerShell 的必要條件](#prerequisites-for-using-azure-powershell-with-azure-storage)。</span><span class="sxs-lookup"><span data-stu-id="934c5-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="934c5-115">在 5 分鐘內開始使用 Azure 儲存體和 PowerShell</span><span class="sxs-lookup"><span data-stu-id="934c5-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="934c5-116">本節說明如何在 5 分鐘內 tooaccess 透過 PowerShell 的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="934c5-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="934c5-117">**新 tooAzure:**取得 Microsoft Azure 訂用帳戶和該訂用帳戶相關聯的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="934c5-118">如需 Azure 購買選項的資訊，請參閱[免費試用](https://azure.microsoft.com/pricing/free-trial/)、[購買選項](https://azure.microsoft.com/pricing/purchase-options/)和[會員優惠](https://azure.microsoft.com/pricing/member-offers/) (適用於 MSDN、Microsoft 合作夥伴網路、BizSpark 和其他 Microsoft 方案的成員)。</span><span class="sxs-lookup"><span data-stu-id="934c5-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="934c5-119">如需 Azure 訂用帳戶的詳細資訊，請參閱 [在 Azure Active Directory (Azure AD) 中指派系統管理員角色](https://msdn.microsoft.com/library/azure/hh531793.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="934c5-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="934c5-120">**建立 Microsoft Azure 訂用帳戶和帳戶之後：**</span><span class="sxs-lookup"><span data-stu-id="934c5-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="934c5-121">下載並安裝最新的 hello [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest)。</span><span class="sxs-lookup"><span data-stu-id="934c5-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="934c5-122">啟動 Windows PowerShell 整合式指令碼環境 (ISE): 在本機電腦，到 toohello**啟動**功能表。</span><span class="sxs-lookup"><span data-stu-id="934c5-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="934c5-123">型別**系統管理工具**按一下 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="934c5-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="934c5-124">在 hello**系統管理工具**視窗中，以滑鼠右鍵按一下**Windows PowerShell ISE**，按一下 **系統管理員身分執行**。</span><span class="sxs-lookup"><span data-stu-id="934c5-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="934c5-125">在**Windows PowerShell ISE**，按一下 **檔案** > **新增**toocreate 新的指令碼檔。</span><span class="sxs-lookup"><span data-stu-id="934c5-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="934c5-126">現在，我們會提供簡單的指令碼會顯示基本的 PowerShell 命令 tooaccess Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="934c5-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="934c5-127">hello 指令碼會先問問您的 Azure 帳戶認證 tooadd Azure 帳戶 toohello 本機 PowerShell 環境。</span><span class="sxs-lookup"><span data-stu-id="934c5-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="934c5-128">然後，hello 指令碼會設定 hello 預設 Azure 訂用帳戶，並在 Azure 中建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="934c5-129">接下來，hello 指令碼會在這個新的儲存體帳戶中建立新的容器，並上傳現有的映像檔案 (blob) toothat 容器。</span><span class="sxs-lookup"><span data-stu-id="934c5-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="934c5-130">Hello 指令碼會列出該容器中的所有 blob 之後，它會在本機電腦中建立新的目的地目錄，並下載 hello 映像檔案。</span><span class="sxs-lookup"><span data-stu-id="934c5-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="934c5-131">在下列程式碼區段的 hello，選取 hello hello 註解之間的指令碼**#begin**和**#end**。</span><span class="sxs-lookup"><span data-stu-id="934c5-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="934c5-132">按下 CTRL + C toocopy 它 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="934c5-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
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
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="934c5-133">在**Windows PowerShell ISE**，按下 CTRL + V 鍵 toocopy hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="934c5-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="934c5-134">按一下 檔案 > 儲存。</span><span class="sxs-lookup"><span data-stu-id="934c5-134">Click **File** > **Save**.</span></span> <span data-ttu-id="934c5-135">在 hello**存**對話方塊視窗中，輸入 hello 名稱 hello 指令碼檔案，例如"mystoragescript。 」</span><span class="sxs-lookup"><span data-stu-id="934c5-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="934c5-136">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="934c5-136">Click **Save**.</span></span>
7. <span data-ttu-id="934c5-137">現在，您必須根據您的組態設定 tooupdate hello 指令碼變數。</span><span class="sxs-lookup"><span data-stu-id="934c5-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="934c5-138">您必須更新 hello **$SubscriptionName**變數與您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="934c5-139">您可以保留 hello hello 指令碼中所指定的其他變數或在您希望的位置加以更新。</span><span class="sxs-lookup"><span data-stu-id="934c5-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="934c5-140">**$SubscriptionName：** 您必須使用自己的訂用帳戶名稱更新此變數。</span><span class="sxs-lookup"><span data-stu-id="934c5-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="934c5-141">請遵循下列三種方式 toolocate hello 您訂用帳戶名稱的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="934c5-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="934c5-142">a.</span><span class="sxs-lookup"><span data-stu-id="934c5-142">a.</span></span> <span data-ttu-id="934c5-143">在**Windows PowerShell ISE**，按一下 **檔案** > **新增**toocreate 新的指令碼檔。</span><span class="sxs-lookup"><span data-stu-id="934c5-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="934c5-144">複製 hello 下列指令碼 toohello 新指令碼檔案，然後按一下**偵錯** > **執行**。</span><span class="sxs-lookup"><span data-stu-id="934c5-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="934c5-145">hello 下列指令碼會先詢問您的 Azure 帳戶認證 tooadd Azure 帳戶 toohello 本機 PowerShell 環境，然後顯示所有 hello 的訂用帳戶連線的 toohello 本機 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="934c5-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="934c5-146">記下 hello hello 訂用帳戶名稱的 toouse 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="934c5-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="934c5-147">b.</span><span class="sxs-lookup"><span data-stu-id="934c5-147">b.</span></span> <span data-ttu-id="934c5-148">toolocate 和複製您訂用帳戶名稱在 hello [Azure 入口網站](https://portal.azure.com)，在 hello hello 留在中樞功能表中按一下**訂閱**。</span><span class="sxs-lookup"><span data-stu-id="934c5-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="934c5-149">將複製 hello 的 toouse 執行本指南中的 hello 指令碼時的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="934c5-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Azure 入口網站](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="934c5-151">c.</span><span class="sxs-lookup"><span data-stu-id="934c5-151">c.</span></span> <span data-ttu-id="934c5-152">toolocate 和複製您訂用帳戶名稱在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)、 向下捲動並按一下**設定**上 hello hello 入口網站的左側。</span><span class="sxs-lookup"><span data-stu-id="934c5-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="934c5-153">按一下**訂閱**toosee 訂用帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="934c5-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="934c5-154">複製 hello 想 toouse 執行本指南中提供的 hello 指令碼時的訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="934c5-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![Azure 傳統入口網站](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="934c5-156">**$StorageAccountName:**使用給定名稱 hello 指令碼中的 hello 或輸入您的儲存體帳戶的新名稱。</span><span class="sxs-lookup"><span data-stu-id="934c5-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="934c5-157">**重要事項：** hello hello 儲存體帳戶名稱必須是唯一在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="934c5-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="934c5-158">而且必須是小寫字母！</span><span class="sxs-lookup"><span data-stu-id="934c5-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="934c5-159">**$Location:** hello 指令碼中使用給定 「 美國西部"hello，或選擇其他的 Azure 位置，例如，美國東部、 北歐、 等等。</span><span class="sxs-lookup"><span data-stu-id="934c5-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="934c5-160">**$ContainerName:**使用給定名稱 hello 指令碼中的 hello 或輸入您的容器的新名稱。</span><span class="sxs-lookup"><span data-stu-id="934c5-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="934c5-161">**$ImageToUpload:**您本機電腦上，輸入路徑 tooa 圖片，例如:"C:\Images\HelloWorld.png"。</span><span class="sxs-lookup"><span data-stu-id="934c5-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="934c5-162">**$DestinationFolder:** Enter 路徑 tooa 本機目錄 toostore 下載檔案，從 Azure 儲存體，例如:"C:\DownloadImages"。</span><span class="sxs-lookup"><span data-stu-id="934c5-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="934c5-163">在更新之後 hello hello"mystoragescript.ps1"檔案中的指令碼變數，按一下 **檔案** > **儲存**。</span><span class="sxs-lookup"><span data-stu-id="934c5-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="934c5-164">然後，按一下 **偵錯** > **執行**或按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="934c5-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="934c5-165">Hello 指令碼執行之後，您應該有包含 hello 下載映像檔的本機目的資料夾。</span><span class="sxs-lookup"><span data-stu-id="934c5-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="934c5-166">下列螢幕擷取畫面的 hello 顯示範例輸出：</span><span class="sxs-lookup"><span data-stu-id="934c5-166">hello following screenshot shows an example output:</span></span>

![下載 Blob](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="934c5-168">hello"Getting started 與 Azure 儲存體和 PowerShell 在 5 分鐘內"區段快速介紹如何 toouse 與 Azure 儲存體的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="934c5-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="934c5-169">如需詳細的資訊和指示，我們建議您 tooread hello 下列各節。</span><span class="sxs-lookup"><span data-stu-id="934c5-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="934c5-170">搭配使用 Azure PowerShell 與 Azure 儲存體的先決條件</span><span class="sxs-lookup"><span data-stu-id="934c5-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="934c5-171">您需要 Azure 訂用帳戶和帳戶 toorun hello PowerShell cmdlet 提供本指南中，如上面所述。</span><span class="sxs-lookup"><span data-stu-id="934c5-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="934c5-172">Azure PowerShell 是提供 cmdlet toomanage 透過 Windows PowerShell 的 Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="934c5-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="934c5-173">如需安裝及設定 Azure PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="934c5-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="934c5-174">我們建議您下載和安裝或使用本指南之前升級 toohello 最新的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="934c5-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="934c5-175">您可以在 hello 標準 Windows PowerShell 主控台或 hello Windows PowerShell 整合式指令碼環境 (ISE) 中執行 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="934c5-176">例如，tooopen **Windows PowerShell ISE**toohello [開始] 功能表中，輸入 [系統管理工具]，請按一下 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="934c5-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="934c5-177">在 hello 系統管理工具 視窗中，以滑鼠右鍵按一下 Windows PowerShell ISE 中，按一下 以系統管理員身分執行。</span><span class="sxs-lookup"><span data-stu-id="934c5-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="934c5-178">Toomanage 儲存體帳戶在 Azure 中的方式</span><span class="sxs-lookup"><span data-stu-id="934c5-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="934c5-179">讓我們看看如何使用 PowerShell 在 Azure 中管理儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="934c5-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="934c5-180">如何 tooset 預設的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="934c5-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="934c5-181">toomanage 使用 Azure PowerShell 的 Azure 儲存體，您需要 tooauthenticate 利用 Azure 將用戶端環境透過 Azure Active Directory 驗證或憑證式驗證。</span><span class="sxs-lookup"><span data-stu-id="934c5-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="934c5-182">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)教學課程。</span><span class="sxs-lookup"><span data-stu-id="934c5-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="934c5-183">本指南使用 hello Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="934c5-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="934c5-184">在 Windows PowerShell ISE 中，輸入下列命令 tooadd hello Azure 帳戶 toohello 本機 PowerShell 環境：</span><span class="sxs-lookup"><span data-stu-id="934c5-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="934c5-185">Hello 「 登入 tooMicrosoft Azure 」 在視窗中，輸入 hello 電子郵件地址與您的帳戶相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="934c5-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="934c5-186">Azure 驗證並儲存 hello 認證資訊，，然後關閉 [hello] 視窗。</span><span class="sxs-lookup"><span data-stu-id="934c5-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="934c5-187">接著，執行下列命令 tooview hello Azure 的 hello 帳戶在本機 PowerShell 環境中，並確認已列出您的帳戶：</span><span class="sxs-lookup"><span data-stu-id="934c5-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="934c5-188">然後，執行下列 cmdlet tooview hello 所有 hello 的訂用帳戶連線的 toohello 本機 PowerShell 工作階段，並確認已列出您的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="934c5-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="934c5-189">執行 hello Select-azuresubscription cmdlet tooset Azure 訂用帳戶中，預設值：</span><span class="sxs-lookup"><span data-stu-id="934c5-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="934c5-190">執行 hello Get-azuresubscription cmdlet 以驗證 hello hello 預設訂用帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="934c5-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="934c5-191">toosee 所有 hello 可用的 PowerShell cmdlet Azure 儲存體，都執行：</span><span class="sxs-lookup"><span data-stu-id="934c5-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="934c5-192">如何 toocreate 新的 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="934c5-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="934c5-193">toouse Azure 儲存體，您需要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="934c5-194">設定您的電腦 tooconnect tooyour 訂用帳戶之後，您可以建立新的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="934c5-195">執行 hello Get AzureLocation cmdlet toofind hello 的所有可用的資料中心位置：</span><span class="sxs-lookup"><span data-stu-id="934c5-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="934c5-196">接下來，執行 hello 新增 AzureStorageAccount cmdlet toocreate 新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="934c5-197">hello 下列範例會建立新的儲存體帳戶在 hello 「 美國西部 」 資料中心內。</span><span class="sxs-lookup"><span data-stu-id="934c5-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="934c5-198">hello 您的儲存體帳戶名稱必須是唯一在 Azure 中，而且必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="934c5-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="934c5-199">如需命名慣例與限制，請參閱[關於 Azure 儲存體帳戶](../storage-create-storage-account.md)和[命名和參考容器、Blob 及中繼資料](http://msdn.microsoft.com/library/azure/dd135715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-199">For naming conventions and restrictions, see [About Azure Storage Accounts](../storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="934c5-200">如何 tooset 預設 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="934c5-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="934c5-201">您可以在訂用帳戶中有多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="934c5-202">您可以選擇其中一個，並將它設定為 hello 預設儲存體帳戶的所有 hello 儲存體中的命令 hello 相同的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="934c5-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="934c5-203">這可讓您 toorun hello Azure PowerShell 儲存命令但未明確指定 hello 儲存內容。</span><span class="sxs-lookup"><span data-stu-id="934c5-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="934c5-204">tooset 訂用帳戶的預設儲存體帳戶，您可以執行 hello 組 AzureSubscription cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="934c5-205">接下來，執行 hello Get-azuresubscription cmdlet tooverify hello 儲存體帳戶是預設訂用帳戶的帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="934c5-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="934c5-206">此命令會傳回 hello 訂閱屬性，包括其目前的儲存體帳戶 hello 目前訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="934c5-207">如何 toolist 所有 Azure 儲存體帳戶的訂用帳戶中</span><span class="sxs-lookup"><span data-stu-id="934c5-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="934c5-208">每個 Azure 訂用帳戶可以有 too100 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="934c5-209">Hello 最新限制的資訊，請參閱[Azure 訂用帳戶和服務限制、 配額和條件約束](../../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="934c5-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="934c5-210">執行下列 cmdlet toofind 出 hello 名稱和狀態的 hello hello 目前訂用帳戶的儲存體帳戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="934c5-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="934c5-211">如何 toocreate Azure 儲存體內容</span><span class="sxs-lookup"><span data-stu-id="934c5-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="934c5-212">Azure 儲存體內容是 PowerShell tooencapsulate hello 儲存體認證中的物件。</span><span class="sxs-lookup"><span data-stu-id="934c5-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="934c5-213">執行任何後續的 cmdlet 時使用的儲存體內容可讓您 tooauthenticate 您的要求未明確指定 hello 儲存體帳戶和其存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="934c5-214">您可以用很多方式建立儲存體內容，例如使用儲存體帳戶名稱和存取金鑰、共用存取簽章 (SAS) 權杖、連接字串或匿名。</span><span class="sxs-lookup"><span data-stu-id="934c5-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="934c5-215">如需詳細資訊，請參閱 [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext)。</span><span class="sxs-lookup"><span data-stu-id="934c5-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="934c5-216">使用下列三種方式 toocreate hello 的其中一個儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="934c5-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="934c5-217">執行 hello [Get AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind 出 hello Azure 儲存體帳戶的主要儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="934c5-218">接下來，呼叫 hello[新增 AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate 儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="934c5-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="934c5-219">產生 Azure 儲存體容器的共用的存取簽章 token，並使用它 toocreate 儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="934c5-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="934c5-220">如需詳細資訊，請參閱 [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) 和[使用共用存取簽章 (SAS)](../storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="934c5-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="934c5-221">在某些情況下，您可能想 toospecify hello 服務端點，當您建立新的存放裝置內容。</span><span class="sxs-lookup"><span data-stu-id="934c5-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="934c5-222">當您儲存體帳戶的自訂網域名稱註冊與 hello Blob 服務或您想 toouse 共用的存取簽章存取儲存體資源，這可能是必要。</span><span class="sxs-lookup"><span data-stu-id="934c5-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="934c5-223">設定連接字串中的 hello 服務端點並使用新的儲存體內容 toocreate 如下所示：</span><span class="sxs-lookup"><span data-stu-id="934c5-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="934c5-224">如需有關如何 tooconfigure 儲存體連接字串，請參閱[設定連接字串](../storage-configure-connection-string.md)。</span><span class="sxs-lookup"><span data-stu-id="934c5-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](../storage-configure-connection-string.md).</span></span>

<span data-ttu-id="934c5-225">現在，您必須設定您的電腦，並學到如何 toomanage 訂閱和儲存體帳戶使用 Azure PowerShell toohello toomanage Azure blob 的方式下一個區段 toolearn 去 blob 快照集。</span><span class="sxs-lookup"><span data-stu-id="934c5-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="934c5-226">如何 tooretrieve 和重新產生 Azure 儲存體金鑰</span><span class="sxs-lookup"><span data-stu-id="934c5-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="934c5-227">Azure 儲存體帳戶會隨附兩個帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="934c5-228">您可以使用下列 cmdlet tooretrieve hello 您的金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="934c5-229">使用下列 cmdlet tooretrieve 特定索引鍵的 hello。</span><span class="sxs-lookup"><span data-stu-id="934c5-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="934c5-230">有效值為 Primary 和 Secondary。</span><span class="sxs-lookup"><span data-stu-id="934c5-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="934c5-231">如果您想要 tooregenerate 您的金鑰使用下列 cmdlet 的 hello。</span><span class="sxs-lookup"><span data-stu-id="934c5-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="934c5-232">-KeyType 的有效值為 "Primary" 和 "Secondary"</span><span class="sxs-lookup"><span data-stu-id="934c5-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="934c5-233">Toomanage Azure 的 blob</span><span class="sxs-lookup"><span data-stu-id="934c5-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="934c5-234">Azure Blob 儲存體是用於儲存大量非結構化資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="934c5-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="934c5-235">本節假設您已熟悉 hello Azure Blob 儲存體服務的概念。</span><span class="sxs-lookup"><span data-stu-id="934c5-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="934c5-236">如需詳細資訊，請參閱[以 .NET 開始使用 Blob 儲存體](../blobs/storage-dotnet-how-to-use-blobs.md)和 [Blob 服務概念](http://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-236">For detailed information, see [Get started with Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="934c5-237">如何 toocreate 容器</span><span class="sxs-lookup"><span data-stu-id="934c5-237">How toocreate a container</span></span>
<span data-ttu-id="934c5-238">Azure 儲存體中的每個 Blob 必須位於一個容器中。</span><span class="sxs-lookup"><span data-stu-id="934c5-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="934c5-239">您可以建立私用容器使用 hello New-azurestoragecontainer cmdlet:</span><span class="sxs-lookup"><span data-stu-id="934c5-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="934c5-240">匿名讀取權限有三個層級：**Off**、**Blob** 和 **Container**。</span><span class="sxs-lookup"><span data-stu-id="934c5-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="934c5-241">tooprevent 匿名存取 tooblobs，集 hello 權限的參數太**關閉**。</span><span class="sxs-lookup"><span data-stu-id="934c5-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="934c5-242">根據預設，hello 新容器是私人的而且只有 hello 帳戶擁有者可存取。</span><span class="sxs-lookup"><span data-stu-id="934c5-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="934c5-243">tooallow 匿名公用讀取存取 tooblob 資源，但不是 toocontainer 中繼資料或 toohello 清單 hello 容器中的 blob、 設定 hello 權限的參數太**Blob**。</span><span class="sxs-lookup"><span data-stu-id="934c5-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="934c5-244">tooallow 完整公用讀取存取 tooblob 資源、 容器中繼資料及 hello hello 容器中的 blob 清單中，設定 hello 權限的參數太**容器**。</span><span class="sxs-lookup"><span data-stu-id="934c5-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="934c5-245">如需詳細資訊，請參閱[管理匿名讀取權限 toocontainers 和 blob](../blobs/storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="934c5-245">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="934c5-246">如何 tooupload blob 容器</span><span class="sxs-lookup"><span data-stu-id="934c5-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="934c5-247">Azure Blob 儲存體支援區塊 Blob 和頁面 Blob。</span><span class="sxs-lookup"><span data-stu-id="934c5-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="934c5-248">如需詳細資訊，請參閱 [了解區塊 Blob、附加 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="934c5-249">tooupload tooa 容器中的 blob，您可以使用 hello [Set-azurestorageblobcontent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="934c5-250">根據預設，此命令會將 hello 本機檔案 tooa 區塊 blob 上傳。</span><span class="sxs-lookup"><span data-stu-id="934c5-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="934c5-251">toospecify hello hello blob 類型，您可以使用 hello-BlobType 參數。</span><span class="sxs-lookup"><span data-stu-id="934c5-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="934c5-252">hello 下列範例會執行 hello [Get-childitem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget 所有 hello hello 指定的資料夾中的檔案，然後將它們傳送 toohello 下一個指令程式使用 hello 管線運算子。</span><span class="sxs-lookup"><span data-stu-id="934c5-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="934c5-253">hello [Set-azurestorageblobcontent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet 上傳 hello 本機檔案 tooyour 容器：</span><span class="sxs-lookup"><span data-stu-id="934c5-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="934c5-254">Toodownload 從容器的 blob</span><span class="sxs-lookup"><span data-stu-id="934c5-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="934c5-255">下列範例中的 hello 示範 toodownload 從容器的 blob。</span><span class="sxs-lookup"><span data-stu-id="934c5-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="934c5-256">hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包含 hello 儲存體帳戶名稱以及其主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="934c5-257">然後，hello 範例會擷取使用 hello 的 blob 參考[Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="934c5-258">接下來，hello 範例會使用 hello [Get AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blob hello 本機目的資料夾。</span><span class="sxs-lookup"><span data-stu-id="934c5-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="934c5-259">Toocopy 從一個儲存體容器 tooanother 的 blob</span><span class="sxs-lookup"><span data-stu-id="934c5-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="934c5-260">您可以跨儲存體帳戶和區域以非同步方式複製 Blob。</span><span class="sxs-lookup"><span data-stu-id="934c5-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="934c5-261">hello 下列範例示範 toocopy 從一個儲存體容器 tooanother 兩個不同的儲存體帳戶中的 blob。</span><span class="sxs-lookup"><span data-stu-id="934c5-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="934c5-262">hello 範例先設定來源和目的地儲存體帳戶的變數，並接著會建立每個帳戶的儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="934c5-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="934c5-263">接下來，hello 範例會將 blob 複製從 hello 來源容器 toohello 目的地容器使用 hello[開始 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="934c5-264">hello 範例假設 hello 來源和目的地儲存體帳戶和容器已經存在。</span><span class="sxs-lookup"><span data-stu-id="934c5-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="934c5-265">請注意，此範例會執行非同步複製。</span><span class="sxs-lookup"><span data-stu-id="934c5-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="934c5-266">您可以監視的每個複本的 hello 狀態執行 hello [Get AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="934c5-267">Toocopy 從次要位置的 blob</span><span class="sxs-lookup"><span data-stu-id="934c5-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="934c5-268">您可以從 hello 次要位置的 RA GRS 啟用帳戶複製 blob。</span><span class="sxs-lookup"><span data-stu-id="934c5-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="934c5-269">如何 toodelete blob</span><span class="sxs-lookup"><span data-stu-id="934c5-269">How toodelete a blob</span></span>
<span data-ttu-id="934c5-270">toodelete blob，先取得 blob 的參考，然後在其上呼叫 hello 移除 AzureStorageBlob cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="934c5-271">hello 下列範例會刪除指定的容器中的所有 hello blob。</span><span class="sxs-lookup"><span data-stu-id="934c5-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="934c5-272">hello 範例第一次設定儲存體帳戶的變數，並接著會建立儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="934c5-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="934c5-273">接下來，hello 範例會擷取使用 hello 的 blob 參考[Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet，並執行 hello[移除 AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet 從 Azure 儲存體中容器的 tooremove blob。</span><span class="sxs-lookup"><span data-stu-id="934c5-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="934c5-274">如何 toomanage Azure blob 快照集</span><span class="sxs-lookup"><span data-stu-id="934c5-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="934c5-275">Azure 可讓您建立 Blob 的快照集。</span><span class="sxs-lookup"><span data-stu-id="934c5-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="934c5-276">快照集是在某個點時間取得的唯讀 Blob 版本。</span><span class="sxs-lookup"><span data-stu-id="934c5-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="934c5-277">一旦建立快照集後，即可加以讀取、複製或刪除，但不能修改。</span><span class="sxs-lookup"><span data-stu-id="934c5-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="934c5-278">快照集提供 blob 向上方式 tooback 出現在時間點。</span><span class="sxs-lookup"><span data-stu-id="934c5-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="934c5-279">如需詳細資訊，請參閱 [建立 Blob 的快照集](http://msdn.microsoft.com/library/azure/hh488361.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="934c5-280">如何 toocreate blob 快照集</span><span class="sxs-lookup"><span data-stu-id="934c5-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="934c5-281">blob 的 snaphot toocreate 先取得 blob 的參考，然後再呼叫 hello`ICloudBlob.CreateSnapshot`方法。</span><span class="sxs-lookup"><span data-stu-id="934c5-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="934c5-282">hello 下列範例先設定儲存體帳戶的變數，然後建立儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="934c5-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="934c5-283">接下來，hello 範例會擷取使用 hello 的 blob 參考[Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet，並執行 hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx)方法 toocreate 快照集。</span><span class="sxs-lookup"><span data-stu-id="934c5-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="934c5-284">如何 toolist blob 的快照集</span><span class="sxs-lookup"><span data-stu-id="934c5-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="934c5-285">您可以對 Blob 建立您所需數量的快照集。</span><span class="sxs-lookup"><span data-stu-id="934c5-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="934c5-286">您可以列出 blob tootrack 與相關聯的 hello 快照目前的快照集。</span><span class="sxs-lookup"><span data-stu-id="934c5-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="934c5-287">hello 下列範例會使用預先定義的 blob 和呼叫 hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob)該 blob 的 cmdlet toolist hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="934c5-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="934c5-288">如何 toocopy blob 的快照集</span><span class="sxs-lookup"><span data-stu-id="934c5-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="934c5-289">您可以複製 blob toorestore hello 快照集的快照集。</span><span class="sxs-lookup"><span data-stu-id="934c5-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="934c5-290">如需詳細的資訊及限制，請參閱 [建立 Blob 的快照集](http://msdn.microsoft.com/library/azure/hh488361.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="934c5-291">hello 下列範例先設定儲存體帳戶的變數，然後建立儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="934c5-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="934c5-292">接下來，hello 範例會定義 hello 容器和 blob 名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="934c5-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="934c5-293">hello 範例會擷取使用 hello 的 blob 參考[Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet，並執行 hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx)方法 toocreate 快照集。</span><span class="sxs-lookup"><span data-stu-id="934c5-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="934c5-294">然後，hello 範例會執行 hello[開始 AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello blob 快照集使用 hello ICloudBlob 物件 hello 來源 blob。</span><span class="sxs-lookup"><span data-stu-id="934c5-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="934c5-295">確定 tooupdate hello 變數根據您之前執行 hello 範例的組態。</span><span class="sxs-lookup"><span data-stu-id="934c5-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="934c5-296">請注意下列範例的 hello 假設 hello 來源和目的地容器和 hello 來源 blob 已經存在。</span><span class="sxs-lookup"><span data-stu-id="934c5-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="934c5-297">既然您已經學會如何 toomanage Azure blob，blob 快照集，使用 Azure PowerShell，請移 toohello 下一個區段 toolearn toomanage 資料表、 佇列與檔案的方式。</span><span class="sxs-lookup"><span data-stu-id="934c5-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="934c5-298">如何 toomanage Azure 資料表和資料表實體</span><span class="sxs-lookup"><span data-stu-id="934c5-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="934c5-299">Azure 資料表儲存體服務是 NoSQL 資料存放區，您可以使用 toostore 及查詢大型資料集的結構化、 非關聯式。</span><span class="sxs-lookup"><span data-stu-id="934c5-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="934c5-300">hello 的 hello 服務的主要元件是資料表、 實體和屬性。</span><span class="sxs-lookup"><span data-stu-id="934c5-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="934c5-301">資料表是一組實體。</span><span class="sxs-lookup"><span data-stu-id="934c5-301">A table is a collection of entities.</span></span> <span data-ttu-id="934c5-302">實體是一組屬性。</span><span class="sxs-lookup"><span data-stu-id="934c5-302">An entity is a set of properties.</span></span> <span data-ttu-id="934c5-303">每個實體可以有 too252 屬性，也就是所有的名稱 / 值組。</span><span class="sxs-lookup"><span data-stu-id="934c5-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="934c5-304">本節假設您已熟悉 hello Azure 資料表儲存體服務的概念。</span><span class="sxs-lookup"><span data-stu-id="934c5-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="934c5-305">如需詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)和[開始使用適用於.NET 的 Azure 資料表儲存體使用](../../cosmos-db/table-storage-how-to-use-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="934c5-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="934c5-306">在下列各小節 hello，您將學習如何 toomanage Azure 資料表儲存體服務使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="934c5-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="934c5-307">hello 涵蓋案例包括**建立**，**刪除**，和**擷取****資料表**，以及**加入**，**查詢**，和**刪除資料表實體**。</span><span class="sxs-lookup"><span data-stu-id="934c5-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="934c5-308">如何 toocreate 資料表</span><span class="sxs-lookup"><span data-stu-id="934c5-308">How toocreate a table</span></span>
<span data-ttu-id="934c5-309">每個資料表必須位於 Azure 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="934c5-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="934c5-310">hello 下列範例會示範如何 toocreate Azure 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="934c5-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="934c5-311">hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包括 hello 儲存體帳戶名稱和其存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="934c5-312">接下來，它會使用 hello[新增 AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate Azure 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="934c5-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="934c5-313">如何 tooretrieve 資料表</span><span class="sxs-lookup"><span data-stu-id="934c5-313">How tooretrieve a table</span></span>
<span data-ttu-id="934c5-314">您可以查詢和擷取儲存體帳戶中的一個或所有資料表。</span><span class="sxs-lookup"><span data-stu-id="934c5-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="934c5-315">hello 下列範例會示範如何指定的資料表使用 tooretrieve hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="934c5-316">如果您呼叫 hello Get AzureStorageTable cmdlet 不含任何參數，它會取得所有儲存體資料表儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="934c5-317">如何 toodelete 資料表</span><span class="sxs-lookup"><span data-stu-id="934c5-317">How toodelete a table</span></span>
<span data-ttu-id="934c5-318">您可以從儲存體帳戶刪除資料表，使用 hello[移除 AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="934c5-319">如何 toomanage 資料表實體</span><span class="sxs-lookup"><span data-stu-id="934c5-319">How toomanage table entities</span></span>
<span data-ttu-id="934c5-320">目前，Azure PowerShell 不會直接提供 cmdlet toomanage 資料表實體。</span><span class="sxs-lookup"><span data-stu-id="934c5-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="934c5-321">tooperform 作業在資料表實體上的，您可以使用在 hello hello 類別[適用於.NET 的 Azure 儲存體用戶端程式庫](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="934c5-322">如何 tooadd 資料表實體</span><span class="sxs-lookup"><span data-stu-id="934c5-322">How tooadd table entities</span></span>
<span data-ttu-id="934c5-323">tooadd 實體 tooa 資料表，第一次建立物件，定義實體屬性。</span><span class="sxs-lookup"><span data-stu-id="934c5-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="934c5-324">實體可以有 too255 屬性，包括 3 個系統屬性： **PartitionKey**， **RowKey**，和**時間戳記**。</span><span class="sxs-lookup"><span data-stu-id="934c5-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="934c5-325">您必須負責插入及更新的 hello 值**PartitionKey**和**RowKey**。</span><span class="sxs-lookup"><span data-stu-id="934c5-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="934c5-326">hello 伺服器負責管理 hello 值**時間戳記**，無法修改。</span><span class="sxs-lookup"><span data-stu-id="934c5-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="934c5-327">一起 hello **PartitionKey**和**RowKey**唯一識別資料表中的每個實體。</span><span class="sxs-lookup"><span data-stu-id="934c5-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="934c5-328">**PartitionKey**： 決定 hello 實體儲存在中的 hello 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="934c5-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="934c5-329">**RowKey**： 唯一識別 hello hello 磁碟分割內的實體。</span><span class="sxs-lookup"><span data-stu-id="934c5-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="934c5-330">您可以定義 too252 實體的自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="934c5-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="934c5-331">如需詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="934c5-332">hello 下列範例會示範如何 tooadd 實體 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="934c5-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="934c5-333">hello 範例示範如何 tooretrieve hello 員工資料表，以及加入數個項目。</span><span class="sxs-lookup"><span data-stu-id="934c5-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="934c5-334">首先，它會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包括 hello 儲存體帳戶名稱和其存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="934c5-335">接下來，它會擷取給定資料表中使用 hello hello [Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="934c5-336">如果 hello 資料表不存在，hello[新增 AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable)指令程式是使用的 toocreate Azure 儲存體中的資料表。</span><span class="sxs-lookup"><span data-stu-id="934c5-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="934c5-337">接下來，hello 範例會定義自訂函式加入實體 tooadd 實體 toohello 資料表，藉由指定每個實體磁碟分割和資料列索引鍵。</span><span class="sxs-lookup"><span data-stu-id="934c5-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="934c5-338">加入實體 hello 函式呼叫 hello [New-object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx)類別 toocreate 實體物件。</span><span class="sxs-lookup"><span data-stu-id="934c5-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="934c5-339">稍後，hello 範例會呼叫 hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx)方法在此實體物件 tooadd 它 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="934c5-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
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

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="934c5-340">如何 tooquery 資料表實體</span><span class="sxs-lookup"><span data-stu-id="934c5-340">How tooquery table entities</span></span>
<span data-ttu-id="934c5-341">tooquery 資料表時，使用 hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="934c5-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="934c5-342">hello 下列範例假設您已已經執行 hello 指令碼中 hello 如何提供本指南的 tooadd [實體] 區段。</span><span class="sxs-lookup"><span data-stu-id="934c5-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="934c5-343">hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存內容，包括 hello 儲存體帳戶名稱和其存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="934c5-344">接下來，它會嘗試使用 hello tooretrieve hello 先前建立 「 員工 」 資料表[Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="934c5-345">呼叫 hello [New-object](http://technet.microsoft.com/library/hh849885.aspx) hello Microsoft.WindowsAzure.Storage.Table.TableQuery 類別上的指令程式會建立新的查詢物件。</span><span class="sxs-lookup"><span data-stu-id="934c5-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="934c5-346">hello 範例會尋找具有 'ID' 資料行，其值為 1 所指定字串篩選條件中的 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="934c5-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="934c5-347">如需詳細資訊，請參閱 [查詢資料表和實體](http://msdn.microsoft.com/library/azure/dd894031.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="934c5-348">當您執行此查詢時，它會傳回符合 hello 篩選準則的所有實體。</span><span class="sxs-lookup"><span data-stu-id="934c5-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="934c5-349">如何 toodelete 資料表實體</span><span class="sxs-lookup"><span data-stu-id="934c5-349">How toodelete table entities</span></span>
<span data-ttu-id="934c5-350">您可以使用實體的資料分割和資料列索引鍵來刪除實體。</span><span class="sxs-lookup"><span data-stu-id="934c5-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="934c5-351">hello 下列範例假設您已已經執行 hello 指令碼中 hello 如何提供本指南的 tooadd [實體] 區段。</span><span class="sxs-lookup"><span data-stu-id="934c5-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="934c5-352">hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存內容，包括 hello 儲存體帳戶名稱和其存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="934c5-353">接下來，它會嘗試使用 hello tooretrieve hello 先前建立 「 員工 」 資料表[Get AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="934c5-354">如果 hello 資料表存在，hello 範例會呼叫 hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx)方法 tooretrieve 實體會根據其資料分割和資料列的索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="934c5-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="934c5-355">然後，傳遞 hello 實體 toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx)方法 toodelete。</span><span class="sxs-lookup"><span data-stu-id="934c5-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="934c5-356">Toomanage Azure 佇列的方式，以及佇列訊息</span><span class="sxs-lookup"><span data-stu-id="934c5-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="934c5-357">Azure 佇列儲存體是用於儲存大量訊息，可透過使用 HTTP 或 HTTPS 驗證呼叫的 hello world 中從任何地方存取服務。</span><span class="sxs-lookup"><span data-stu-id="934c5-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="934c5-358">本節假設您已熟悉 hello Azure 佇列儲存體服務的概念。</span><span class="sxs-lookup"><span data-stu-id="934c5-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="934c5-359">如需詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](../storage-dotnet-how-to-use-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="934c5-359">For detailed information, see [Get started with Azure Queue storage using .NET](../storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="934c5-360">本章節將說明如何 toomanage Azure 佇列儲存體服務使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="934c5-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="934c5-361">hello 涵蓋案例包括**插入**和**刪除**佇列訊息，以及**建立**，**刪除**，和**擷取佇列**。</span><span class="sxs-lookup"><span data-stu-id="934c5-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="934c5-362">如何 toocreate 佇列</span><span class="sxs-lookup"><span data-stu-id="934c5-362">How toocreate a queue</span></span>
<span data-ttu-id="934c5-363">hello 下列範例首先會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包括 hello 儲存體帳戶名稱和其存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="934c5-364">接下來，它會呼叫[新增 AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate 名為 'queuename' 的佇列。</span><span class="sxs-lookup"><span data-stu-id="934c5-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="934c5-365">如需 Azure 佇列服務命名慣例的資訊，請參閱 [為佇列和中繼資料命名](http://msdn.microsoft.com/library/azure/dd179349.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="934c5-366">如何 tooretrieve 佇列</span><span class="sxs-lookup"><span data-stu-id="934c5-366">How tooretrieve a queue</span></span>
<span data-ttu-id="934c5-367">您可以查詢及擷取特定的佇列或所有儲存體帳戶中的 hello 佇列的清單。</span><span class="sxs-lookup"><span data-stu-id="934c5-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="934c5-368">hello 下列範例會示範如何指定的佇列，使用 tooretrieve hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="934c5-369">如果您呼叫 hello [Get AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue)沒有任何參數的 cmdlet，它會取得所有 hello 佇列的清單。</span><span class="sxs-lookup"><span data-stu-id="934c5-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="934c5-370">如何 toodelete 佇列</span><span class="sxs-lookup"><span data-stu-id="934c5-370">How toodelete a queue</span></span>
<span data-ttu-id="934c5-371">toodelete 佇列和所有 hello 訊息包含在它呼叫 hello 移除 AzureStorageQueue cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="934c5-372">hello 下列範例顯示如何指定的佇列，使用 toodelete hello 移除 AzureStorageQueue cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="934c5-373">如何將訊息插入佇列 tooinsert</span><span class="sxs-lookup"><span data-stu-id="934c5-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="934c5-374">tooinsert 將訊息插入現有佇列，先建立的新執行個體的 hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="934c5-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="934c5-375">接下來，呼叫 hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="934c5-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="934c5-376">您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 CloudQueueMessage。</span><span class="sxs-lookup"><span data-stu-id="934c5-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="934c5-377">hello 下列範例會示範如何 tooadd 訊息 tooa 佇列。</span><span class="sxs-lookup"><span data-stu-id="934c5-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="934c5-378">hello 範例首先會建立連接 tooAzure 儲存體使用 hello 儲存體帳戶的內容，其中包括 hello 儲存體帳戶名稱和其存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="934c5-379">接下來，它會擷取使用 hello hello 指定的佇列[Get AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="934c5-380">如果 hello 佇列存在，hello [New-object](http://technet.microsoft.com/library/hh849885.aspx)指令程式是使用的 toocreate hello 的執行個體[Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="934c5-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="934c5-381">稍後，hello 範例會呼叫 hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx)方法在此訊息物件 tooadd 它 tooa 佇列。</span><span class="sxs-lookup"><span data-stu-id="934c5-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="934c5-382">以下是程式碼以擷取佇列，並插入 hello 訊息 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="934c5-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="934c5-383">在 hello toode 佇列下一個訊息</span><span class="sxs-lookup"><span data-stu-id="934c5-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="934c5-384">您的程式碼可以使用兩個步驟將訊息自佇列中清除佇列。</span><span class="sxs-lookup"><span data-stu-id="934c5-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="934c5-385">當您呼叫 hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx)方法，您會收到 hello 下一個訊息佇列中。</span><span class="sxs-lookup"><span data-stu-id="934c5-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="934c5-386">傳回訊息**GetMessage**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="934c5-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="934c5-387">toofinish 移除 hello 訊息從 hello 佇列，您必須呼叫 hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="934c5-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="934c5-388">這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="934c5-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="934c5-389">您的程式碼呼叫**DeleteMessage**處理 hello 訊息之後，以滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="934c5-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="934c5-390">如何 toomanage Azure 檔案共用及檔案</span><span class="sxs-lookup"><span data-stu-id="934c5-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="934c5-391">Azure 檔案儲存體提供共用存放裝置使用 hello 標準 SMB 通訊協定的應用程式。</span><span class="sxs-lookup"><span data-stu-id="934c5-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="934c5-392">Microsoft Azure 虛擬機器和雲端服務可以透過掛接共用，應用程式元件之間共用檔案資料，並在內部部署應用程式可以存取檔案共用，以透過 hello 檔案儲存體 API 或 Azure PowerShell 中的資料。</span><span class="sxs-lookup"><span data-stu-id="934c5-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="934c5-393">如需 Azure 檔案儲存體的詳細資訊，請參閱[在 Windows 上開始使用 Azure 檔案儲存體](../storage-dotnet-how-to-use-files.md)和[檔案服務 REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx)。</span><span class="sxs-lookup"><span data-stu-id="934c5-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="934c5-394">如何 tooset 並查詢儲存體分析</span><span class="sxs-lookup"><span data-stu-id="934c5-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="934c5-395">您可以使用[Azure 儲存體分析](../storage-analytics.md)toocollect 度量資訊。 您的 Azure 儲存體帳戶和記錄資料要求的相關傳送 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="934c5-395">You can use [Azure Storage Analytics](../storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="934c5-396">您可以使用儲存體度量 toomonitor hello 健全狀況的儲存體帳戶和儲存體記錄 toodiagnose 和疑難排解您的儲存體帳戶中的問題。</span><span class="sxs-lookup"><span data-stu-id="934c5-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="934c5-397">您可以使用設定監視 hello Azure 入口網站或 Windows PowerShell 或以程式設計方式使用 hello 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="934c5-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="934c5-398">儲存體記錄發生於用戶端，並讓您的儲存體帳戶中的成功和失敗要求的 toorecord 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="934c5-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="934c5-399">這些記錄檔可讓您讀取、 寫入和刪除作業，針對您資料表、 佇列和 blob 以及 hello 失敗要求的理由 toosee 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="934c5-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="934c5-400">如何使用 PowerShell、 tooenable 和檢視儲存體度量資料，請參閱的 toolearn[如何 tooenable 儲存體度量使用 PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell)。</span><span class="sxs-lookup"><span data-stu-id="934c5-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="934c5-401">如何 tooenable 並擷取儲存體記錄資料使用 PowerShell，請參閱 < 的 toolearn[如何 tooenable 儲存體記錄使用 PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell)和[尋找儲存體記錄 」 記錄檔資料](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata)。</span><span class="sxs-lookup"><span data-stu-id="934c5-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="934c5-402">如需使用儲存體度量 」 和 「 儲存體記錄 tootroubleshoot 儲存體問題的詳細資訊，請參閱[監控、 診斷及排解 Microsoft Azure 儲存體](../storage-monitoring-diagnosing-troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="934c5-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="934c5-403">如何 toomanage 共用存取簽章 (SAS) 和預存存取原則</span><span class="sxs-lookup"><span data-stu-id="934c5-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="934c5-404">共用的存取簽章是使用 Azure 儲存體的任何應用程式的 hello 安全性模型的重要一環。</span><span class="sxs-lookup"><span data-stu-id="934c5-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="934c5-405">它們可用於提供有限的權限 tooyour 儲存體帳戶 tooclients 不應有任何 hello 帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="934c5-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="934c5-406">根據預設，只有 hello 儲存體帳戶的 hello 擁有者可以存取 blob、 資料表，以及該帳戶內的佇列。</span><span class="sxs-lookup"><span data-stu-id="934c5-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="934c5-407">如果您的服務或應用程式需要 toomake 這些資源可用 tooother 用戶端而不需要共用您的存取金鑰，您會有三個選項：</span><span class="sxs-lookup"><span data-stu-id="934c5-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="934c5-408">設定容器的權限 toopermit 匿名讀取權限 toohello 容器和其 blob。</span><span class="sxs-lookup"><span data-stu-id="934c5-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="934c5-409">這不適用於資料表或佇列。</span><span class="sxs-lookup"><span data-stu-id="934c5-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="934c5-410">使用共用的存取簽章，授與特定時間間隔的有限的存取權限 toocontainers、 blob、 佇列和資料表。</span><span class="sxs-lookup"><span data-stu-id="934c5-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="934c5-411">容器或其 blob、 佇列或資料表，請使用預存的存取原則 tooobtain 一層額外的控制共用的存取簽章。</span><span class="sxs-lookup"><span data-stu-id="934c5-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="934c5-412">hello 預存的存取原則可讓您 toochange hello 開始時間、 到期時間或權限的簽章，或 toorevoke 它之後發出。</span><span class="sxs-lookup"><span data-stu-id="934c5-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="934c5-413">共用存取簽章可以是下列其中一種格式：</span><span class="sxs-lookup"><span data-stu-id="934c5-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="934c5-414">**臨機操作 SAS**： 當您建立臨機操作 SAS、 hello 開始時間、 到期時間，並 hello SAS 的權限會指定在 hello SAS URI。</span><span class="sxs-lookup"><span data-stu-id="934c5-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="934c5-415">您可以在容器、Blob、資料表或佇列上建立此類型的 SAS，而且無法撤銷它。</span><span class="sxs-lookup"><span data-stu-id="934c5-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="934c5-416">**與預存的存取原則 SAS**： 資源容器的 blob 容器、 資料表或佇列-佇列上定義的預存的存取原則，您可以使用它 toomanage 條件約束的一個或多個共用的存取簽章。</span><span class="sxs-lookup"><span data-stu-id="934c5-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="934c5-417">當您建立 SAS 關聯與預存的存取原則時，hello SAS 繼承 hello 的條件約束-hello 開始時間、 到期時間和權限-hello 預存存取原則的定義。</span><span class="sxs-lookup"><span data-stu-id="934c5-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="934c5-418">這種類型的 SAS 是可撤銷的。</span><span class="sxs-lookup"><span data-stu-id="934c5-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="934c5-419">如需詳細資訊，請參閱[使用共用存取簽章 (SAS)](../storage-dotnet-shared-access-signature-part-1.md)和[管理匿名讀取權限 toocontainers 和 blob](../blobs/storage-manage-access-to-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="934c5-419">For more information, see [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="934c5-420">在 hello 下一步 區段中，您將學習如何 toocreate Azure 資料表的共用的存取簽章語彙基元和預存存取原則。</span><span class="sxs-lookup"><span data-stu-id="934c5-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="934c5-421">Azure PowerShell 也會為容器、Blob 和佇列提供類似的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="934c5-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="934c5-422">在本節中的 toorun hello 指令碼下載中心 hello [Azure PowerShell 版本 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409)或更新版本。</span><span class="sxs-lookup"><span data-stu-id="934c5-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="934c5-423">如何以原則為基礎的 toocreate 共用存取簽章語彙基元</span><span class="sxs-lookup"><span data-stu-id="934c5-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="934c5-424">使用 hello 新增 AzureStorageTableStoredAccessPolicy cmdlet toocreate 新的預存的存取原則。</span><span class="sxs-lookup"><span data-stu-id="934c5-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="934c5-425">然後，呼叫 hello[新增 AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate Azure 儲存體資料表的新原則為基礎的共用的存取簽章 token。</span><span class="sxs-lookup"><span data-stu-id="934c5-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="934c5-426">如何 toocreate 臨機操作 （非廢止） 的共用存取簽章語彙基元</span><span class="sxs-lookup"><span data-stu-id="934c5-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="934c5-427">使用 hello[新增 AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate 新臨機操作 （非廢止） 共用存取簽章的權杖的 Azure 儲存體資料表：</span><span class="sxs-lookup"><span data-stu-id="934c5-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="934c5-428">如何 toocreate 預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="934c5-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="934c5-429">使用 Azure 儲存體資料表 hello 新增 AzureStorageTableStoredAccessPolicy cmdlet toocreate 新的預存的存取原則：</span><span class="sxs-lookup"><span data-stu-id="934c5-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="934c5-430">如何 tooupdate 預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="934c5-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="934c5-431">使用 Azure 儲存體資料表 hello 組 AzureStorageTableStoredAccessPolicy cmdlet tooupdate 現有的預存的存取原則：</span><span class="sxs-lookup"><span data-stu-id="934c5-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="934c5-432">如何 toodelete 預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="934c5-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="934c5-433">Azure 儲存體資料表上使用 hello 移除 AzureStorageTableStoredAccessPolicy cmdlet toodelete 預存的存取原則：</span><span class="sxs-lookup"><span data-stu-id="934c5-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="934c5-434">如何為美國政府和 Azure China toouse Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="934c5-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="934c5-435">Azure 環境是 Microsoft Azure 的獨立部署，例如[適用於美國政府的 Azure Government](https://azure.microsoft.com/features/gov/)、[適用於全球 Azure 的 AzureCloud](https://portal.azure.com) 和[由中國世紀互聯運作的 AzureChinaCloud for Azure](http://www.windowsazure.cn/)。</span><span class="sxs-lookup"><span data-stu-id="934c5-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="934c5-436">您可以針對美國政府與 Azure 中國部署新的 Azure 環境。</span><span class="sxs-lookup"><span data-stu-id="934c5-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="934c5-437">toouse AzureChinaCloud 與 Azure 儲存體，您需要 toocreate AzureChinaCloud 相關聯的儲存體內容。</span><span class="sxs-lookup"><span data-stu-id="934c5-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="934c5-438">請遵循這些步驟 tooget，您已啟動：</span><span class="sxs-lookup"><span data-stu-id="934c5-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="934c5-439">執行 hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello 可用的 Azure 環境：</span><span class="sxs-lookup"><span data-stu-id="934c5-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="934c5-440">新增 Azure China 帳戶 tooWindows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="934c5-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="934c5-441">建立 AzureChinaCloud 帳戶的儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="934c5-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="934c5-442">toouse Azure 儲存體與[美國Azure Government ](https://azure.microsoft.com/features/gov/) 搭配使用，請定義一個新環境，然後在此環境中建立新的儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="934c5-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="934c5-443">執行 hello [Get AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello 可用的 Azure 環境：</span><span class="sxs-lookup"><span data-stu-id="934c5-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="934c5-444">新增 Azure 美國政府帳戶 tooWindows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="934c5-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="934c5-445">建立 AzureUSGovernment 帳戶的儲存體內容：</span><span class="sxs-lookup"><span data-stu-id="934c5-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="934c5-446">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="934c5-446">For more information, see:</span></span>

* <span data-ttu-id="934c5-447">[Microsoft Azure Government 開發人員指南](../../azure-government/documentation-government-developer-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="934c5-447">[Microsoft Azure Government Developer Guide](../../azure-government/documentation-government-developer-guide.md).</span></span>
* [<span data-ttu-id="934c5-448">在 China 服務上建立應用程式時差異的概觀</span><span class="sxs-lookup"><span data-stu-id="934c5-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="934c5-449">後續步驟</span><span class="sxs-lookup"><span data-stu-id="934c5-449">Next Steps</span></span>
<span data-ttu-id="934c5-450">本指南中，您學到如何 toomanage 使用 Azure PowerShell 的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="934c5-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="934c5-451">以下是有助於您深入了解的一些相關文章和資源。</span><span class="sxs-lookup"><span data-stu-id="934c5-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="934c5-452">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="934c5-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="934c5-453">Azure 儲存體 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="934c5-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="934c5-454">Windows PowerShell 參考</span><span class="sxs-lookup"><span data-stu-id="934c5-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
