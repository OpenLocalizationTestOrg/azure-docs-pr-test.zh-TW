---
title: "從 Azure 金鑰保存庫的 aaaIntegrate 記錄使用事件中心 |Microsoft 文件"
description: "提供 hello 必要步驟 toomake 金鑰保存庫的教學課程使用 Azure 記錄檔整合記錄可用 tooa SIEM"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="099a5-103">Azure 記錄整合教學課程：使用事件中樞處理Azure Key Vault 事件</span><span class="sxs-lookup"><span data-stu-id="099a5-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="099a5-104">您可以使用 Azure 記錄檔整合 tooretrieve 記錄事件，並讓它們使用 tooyour 安全性資訊和事件管理 (SIEM) 系統。</span><span class="sxs-lookup"><span data-stu-id="099a5-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="099a5-105">本教學課程示範如何 Azure 記錄檔整合可以透過 Azure 事件中心取得的使用的 tooprocess 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="099a5-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="099a5-106">使用此教學課程 tooget 熟悉 Azure 記錄檔整合和事件中心的工作，同時透過下列方式 hello 範例步驟，並了解每個步驟如何支援 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="099a5-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="099a5-107">然後您可以採取什麼您已學習到以下 toocreate 自己步驟 toosupport 貴公司的獨特需求。</span><span class="sxs-lookup"><span data-stu-id="099a5-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="099a5-108">hello 步驟與本教學課程中的命令不是預期的 toobe 複製和貼上。</span><span class="sxs-lookup"><span data-stu-id="099a5-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="099a5-109">這些步驟和命令僅供範例之用。</span><span class="sxs-lookup"><span data-stu-id="099a5-109">They're examples only.</span></span> <span data-ttu-id="099a5-110">請勿使用即時環境中的 「 現狀 」 hello PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="099a5-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="099a5-111">您必須根據自己專屬的環境自訂這些命令。</span><span class="sxs-lookup"><span data-stu-id="099a5-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="099a5-112">本教學課程會引導您進行 Azure 金鑰保存庫活動記錄的 tooan 事件中心，並且讓它成為可從 JSON 檔案 tooyour SIEM 系統的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="099a5-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="099a5-113">接著，您可以設定您的 SIEM 系統 tooprocess hello 的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="099a5-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="099a5-114">大部分的 hello 本教學課程步驟包括設定金鑰保存庫、 儲存體帳戶和事件中心。</span><span class="sxs-lookup"><span data-stu-id="099a5-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="099a5-115">hello 特定 Azure 記錄檔整合步驟會在本教學課程中的 hello 結尾處。</span><span class="sxs-lookup"><span data-stu-id="099a5-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="099a5-116">請勿在生產環境中執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="099a5-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="099a5-117">這些步驟僅供實驗室環境之用。</span><span class="sxs-lookup"><span data-stu-id="099a5-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="099a5-118">您必須自訂 hello 步驟，然後才在生產環境中使用。</span><span class="sxs-lookup"><span data-stu-id="099a5-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="099a5-119">提供資訊沿著 hello 方式可協助您了解每個步驟的 hello 動機。</span><span class="sxs-lookup"><span data-stu-id="099a5-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="099a5-120">連結 tooother 文件可讓您更多詳細資料的特定主題。</span><span class="sxs-lookup"><span data-stu-id="099a5-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="099a5-121">如需本教學課程提到的 hello 服務的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="099a5-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="099a5-122">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="099a5-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="099a5-123">Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="099a5-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="099a5-124">Azure 記錄整合</span><span class="sxs-lookup"><span data-stu-id="099a5-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="099a5-125">初始設定</span><span class="sxs-lookup"><span data-stu-id="099a5-125">Initial setup</span></span>

<span data-ttu-id="099a5-126">您可以完成這篇文章中的 hello 步驟之前，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="099a5-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="099a5-127">Azure 訂用帳戶和該訂用帳戶上具有系統管理員權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="099a5-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="099a5-128">如果您沒有訂用帳戶，則可以建立[免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="099a5-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="099a5-129">存取 toohello 的系統符合 hello 安裝 Azure 記錄檔整合需求的網際網路。</span><span class="sxs-lookup"><span data-stu-id="099a5-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="099a5-130">hello 系統可在雲端服務，或裝載於內部。</span><span class="sxs-lookup"><span data-stu-id="099a5-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="099a5-131">已安裝 [Azure 記錄整合](https://www.microsoft.com/download/details.aspx?id=53324)。</span><span class="sxs-lookup"><span data-stu-id="099a5-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="099a5-132">tooinstall 它：</span><span class="sxs-lookup"><span data-stu-id="099a5-132">tooinstall it:</span></span>

   <span data-ttu-id="099a5-133">a.</span><span class="sxs-lookup"><span data-stu-id="099a5-133">a.</span></span> <span data-ttu-id="099a5-134">使用上述步驟 2 中的遠端桌面 tooconnect toohello 系統。</span><span class="sxs-lookup"><span data-stu-id="099a5-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="099a5-135">b.</span><span class="sxs-lookup"><span data-stu-id="099a5-135">b.</span></span> <span data-ttu-id="099a5-136">將複製 hello Azure 記錄檔整合安裝程式 toohello 系統。</span><span class="sxs-lookup"><span data-stu-id="099a5-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="099a5-137">您可以[下載 hello 安裝檔案](https://www.microsoft.com/download/details.aspx?id=53324)。</span><span class="sxs-lookup"><span data-stu-id="099a5-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="099a5-138">c.</span><span class="sxs-lookup"><span data-stu-id="099a5-138">c.</span></span> <span data-ttu-id="099a5-139">啟動 hello 安裝程式，並接受 hello Microsoft 軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="099a5-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="099a5-140">d.</span><span class="sxs-lookup"><span data-stu-id="099a5-140">d.</span></span> <span data-ttu-id="099a5-141">如果您將提供的遙測資訊，請保留 hello 選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="099a5-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="099a5-142">如果不而是傳送使用方式資訊 tooMicrosoft，清除 [hello] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="099a5-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="099a5-143">如需有關 Azure 記錄檔整合以及 tooinstall，請參閱[Azure 記錄與整合 Azure 診斷記錄 Windows 事件轉送](security-azure-log-integration-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="099a5-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="099a5-144">hello 最新的 PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="099a5-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="099a5-145">如果您已安裝 Windows Server 2016，便至少擁有 PowerShell 5.0。</span><span class="sxs-lookup"><span data-stu-id="099a5-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="099a5-146">如果您正在使用任何其他版本的 Windows Server，則可能已安裝舊版 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="099a5-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="099a5-147">您可以檢查 hello 版本輸入```get-host```PowerShell 視窗中。</span><span class="sxs-lookup"><span data-stu-id="099a5-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="099a5-148">如果您尚未安裝 PowerShell 5.0，則可以[進行下載](https://www.microsoft.com/download/details.aspx?id=50395)。</span><span class="sxs-lookup"><span data-stu-id="099a5-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="099a5-149">您至少有之後 PowerShell 5.0 中，您可以繼續 tooinstall hello 最新版本：</span><span class="sxs-lookup"><span data-stu-id="099a5-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="099a5-150">a.</span><span class="sxs-lookup"><span data-stu-id="099a5-150">a.</span></span> <span data-ttu-id="099a5-151">在 PowerShell 視窗中，輸入 hello```Install-Module Azure```命令。</span><span class="sxs-lookup"><span data-stu-id="099a5-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="099a5-152">完成 hello 安裝步驟。</span><span class="sxs-lookup"><span data-stu-id="099a5-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="099a5-153">b.</span><span class="sxs-lookup"><span data-stu-id="099a5-153">b.</span></span> <span data-ttu-id="099a5-154">輸入 hello```Install-Module AzureRM```命令。</span><span class="sxs-lookup"><span data-stu-id="099a5-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="099a5-155">完成 hello 安裝步驟。</span><span class="sxs-lookup"><span data-stu-id="099a5-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="099a5-156">如需詳細資訊，請參閱[安裝 Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0) (英文)。</span><span class="sxs-lookup"><span data-stu-id="099a5-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="099a5-157">建立支援基礎結構元素</span><span class="sxs-lookup"><span data-stu-id="099a5-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="099a5-158">開啟提升權限的 PowerShell 視窗，並移過**C:\Program Files\Microsoft Azure 記錄檔整合**。</span><span class="sxs-lookup"><span data-stu-id="099a5-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="099a5-159">執行 hello 指令碼 LoadAzLogModule.ps1 匯入 hello AzLog cmdlet。</span><span class="sxs-lookup"><span data-stu-id="099a5-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="099a5-160">輸入 hello`.\LoadAzLogModule.ps1`命令。</span><span class="sxs-lookup"><span data-stu-id="099a5-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="099a5-161">(請注意 hello"。 \"命令中。)您應該會看到如下的結果：</span><span class="sxs-lookup"><span data-stu-id="099a5-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![載入的模組清單](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="099a5-163">輸入 hello`Login-AzureRmAccount`命令。</span><span class="sxs-lookup"><span data-stu-id="099a5-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="099a5-164">在 hello 登入視窗中，輸入 hello 訂用帳戶將用於此教學課程中的 hello 認證資訊。</span><span class="sxs-lookup"><span data-stu-id="099a5-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="099a5-165">如果這是 hello tooAzure 下從這部電腦中登入您的第一次，您會看到訊息，以允許 Microsoft toocollect PowerShell 使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="099a5-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="099a5-166">我們建議您啟用此資料集合，因為它會在使用的 tooimprove Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="099a5-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="099a5-167">成功驗證之後，您登入，您會看到 hello hello 下列螢幕擷取畫面中的資訊。</span><span class="sxs-lookup"><span data-stu-id="099a5-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="099a5-168">記下 hello 訂用帳戶 ID 與訂用帳戶名稱，因為您需要它們 toocomplete 稍後步驟。</span><span class="sxs-lookup"><span data-stu-id="099a5-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![PowerShell 視窗](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="099a5-170">建立變數，稍後將會用 toostore 值。</span><span class="sxs-lookup"><span data-stu-id="099a5-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="099a5-171">輸入每個 hello 下列 PowerShell 程式行。</span><span class="sxs-lookup"><span data-stu-id="099a5-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="099a5-172">您可能需要 tooadjust hello 值 toomatch 您的環境。</span><span class="sxs-lookup"><span data-stu-id="099a5-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="099a5-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (您的訂用帳戶名稱可能會不同。</span><span class="sxs-lookup"><span data-stu-id="099a5-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="099a5-174">您可以看到它作為 hello 輸出的 hello 前一個命令的一部分。）</span><span class="sxs-lookup"><span data-stu-id="099a5-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="099a5-175">```$location = 'West US'```（這個變數會使用的 toopass hello 位置建立資源的位置。</span><span class="sxs-lookup"><span data-stu-id="099a5-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="099a5-176">您可以變更這個變數 toobe 您所選擇任何的位置。）</span><span class="sxs-lookup"><span data-stu-id="099a5-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="099a5-177">``` $name = 'azlogtest' + $random```（hello 名稱可以是任何項目，但它應該包含小寫字母和數字）。</span><span class="sxs-lookup"><span data-stu-id="099a5-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="099a5-178">``` $storageName = $name```（hello 儲存體帳戶名稱將會使用此變數）。</span><span class="sxs-lookup"><span data-stu-id="099a5-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="099a5-179">```$rgname = $name ```（這個變數會使用 hello 資源群組名稱）。</span><span class="sxs-lookup"><span data-stu-id="099a5-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="099a5-180">``` $eventHubNameSpaceName = $name```（這是 hello hello 事件中樞命名空間名稱）。</span><span class="sxs-lookup"><span data-stu-id="099a5-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="099a5-181">指定您將使用的 hello 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="099a5-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="099a5-182">建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="099a5-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="099a5-183">如果您輸入`$rg`此時，您應該會看到輸出類似 toothis 螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="099a5-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![建立資源群組之後的輸出](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="099a5-185">建立儲存體帳戶將會使用的 tookeep 追蹤的狀態資訊：</span><span class="sxs-lookup"><span data-stu-id="099a5-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="099a5-186">建立 hello 事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="099a5-186">Create hello event hub namespace.</span></span> <span data-ttu-id="099a5-187">這是必要的 toocreate 事件中心。</span><span class="sxs-lookup"><span data-stu-id="099a5-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="099a5-188">取得將用於與 hello insights 提供者的 hello 規則識別碼：</span><span class="sxs-lookup"><span data-stu-id="099a5-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="099a5-189">取得所有可能的 Azure 位置，並在稍後步驟中加入可用的 hello 名稱 tooa 變數：</span><span class="sxs-lookup"><span data-stu-id="099a5-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="099a5-190">a.</span><span class="sxs-lookup"><span data-stu-id="099a5-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="099a5-191">b.</span><span class="sxs-lookup"><span data-stu-id="099a5-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="099a5-192">如果您輸入`$locations`此時，您看到 hello 位置名稱不含 hello Get AzureRmLocation 所傳回的額外資訊。</span><span class="sxs-lookup"><span data-stu-id="099a5-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="099a5-193">建立 Azure Resource Manager 記錄設定檔：</span><span class="sxs-lookup"><span data-stu-id="099a5-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="099a5-194">如需 hello Azure 記錄檔的設定檔的詳細資訊，請參閱[hello Azure 活動記錄檔的概觀](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="099a5-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="099a5-195">當您嘗試 toocreate 記錄檔的設定檔，您可能會收到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="099a5-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="099a5-196">然後，您可以檢閱 Get AzureRmLogProfile 和移除 AzureRmLogProfile hello 文件。</span><span class="sxs-lookup"><span data-stu-id="099a5-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="099a5-197">如果您執行 Get AzureRmLogProfile，您會看到 hello 記錄檔的設定檔的資訊。</span><span class="sxs-lookup"><span data-stu-id="099a5-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="099a5-198">您可以刪除現有記錄檔 hello 設定檔輸入 hello```Remove-AzureRmLogProfile -name 'Log Profile Name' ```命令。</span><span class="sxs-lookup"><span data-stu-id="099a5-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![資源管理員設定檔錯誤](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="099a5-200">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="099a5-200">Create a key vault</span></span>

1. <span data-ttu-id="099a5-201">建立 hello 金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="099a5-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="099a5-202">設定金鑰保存庫 hello 的記錄：</span><span class="sxs-lookup"><span data-stu-id="099a5-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="099a5-203">產生記錄活動</span><span class="sxs-lookup"><span data-stu-id="099a5-203">Generate log activity</span></span>

<span data-ttu-id="099a5-204">要求需要 toobe 傳送 tooKey 保存庫 toogenerate 記錄檔 」 活動。</span><span class="sxs-lookup"><span data-stu-id="099a5-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="099a5-205">產生金鑰、儲存密碼或從金鑰保存庫讀取密碼等動作都會建立記錄項目。</span><span class="sxs-lookup"><span data-stu-id="099a5-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="099a5-206">顯示目前儲存體金鑰 hello:</span><span class="sxs-lookup"><span data-stu-id="099a5-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="099a5-207">產生新的 **key2**：</span><span class="sxs-lookup"><span data-stu-id="099a5-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="099a5-208">再次顯示 hello 索引鍵，並看到**key2**會保存不同的值：</span><span class="sxs-lookup"><span data-stu-id="099a5-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="099a5-209">設定和讀取密碼 toogenerate 額外的記錄項目：</span><span class="sxs-lookup"><span data-stu-id="099a5-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="099a5-210">a.</span><span class="sxs-lookup"><span data-stu-id="099a5-210">a.</span></span> <span data-ttu-id="099a5-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="099a5-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![傳回的密碼](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="099a5-213">設定 Azure 記錄整合</span><span class="sxs-lookup"><span data-stu-id="099a5-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="099a5-214">既然您已經設定所有 hello 必要的項目 toohave 金鑰保存庫記錄 tooan 事件中樞，您會需要 tooconfigure Azure 記錄檔整合：</span><span class="sxs-lookup"><span data-stu-id="099a5-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="099a5-215">執行每個事件中樞的 hello AzLog 命令：</span><span class="sxs-lookup"><span data-stu-id="099a5-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="099a5-216">之後約一分鐘執行 hello 最後兩個命令，您應該會看到所產生的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="099a5-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="099a5-217">您可以藉由監視 hello 目錄，確認**C:\users\AzLog\EventHubJson**。</span><span class="sxs-lookup"><span data-stu-id="099a5-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="099a5-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="099a5-218">Next steps</span></span>

- [<span data-ttu-id="099a5-219">Azure 記錄整合常見問題集</span><span class="sxs-lookup"><span data-stu-id="099a5-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="099a5-220">開始使用 Azure 記錄整合</span><span class="sxs-lookup"><span data-stu-id="099a5-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="099a5-221">將記錄從 Azure 資源整合到 SIEM 系統</span><span class="sxs-lookup"><span data-stu-id="099a5-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
