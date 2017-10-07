---
title: "aaaUse 封包擷取 toodo 主動式網路監視的警示和 Azure 函式 |Microsoft 文件"
description: "本文說明如何 toocreate 警示觸發與 Azure 網路監看員的封包擷取"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="3fd79-103">使用封包擷取搭配警示和 Azure Functions 進行主動式網路監視</span><span class="sxs-lookup"><span data-stu-id="3fd79-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="3fd79-104">網路監看員封包擷取會擷取工作階段建立 tootrack 流量進出虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3fd79-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="3fd79-105">hello 擷取檔案可以有篩選定義 tootrack 只 hello 想 toomonitor 的流量。</span><span class="sxs-lookup"><span data-stu-id="3fd79-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="3fd79-106">此資料會儲存在儲存體 blob，或在本機 hello 客體機器上。</span><span class="sxs-lookup"><span data-stu-id="3fd79-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="3fd79-107">這項功能可以從其他的自動化案例遠端啟動，例如 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="3fd79-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="3fd79-108">Hello 功能 toorun 主動式擷取根據封包擷取提供定義網路異常狀況。</span><span class="sxs-lookup"><span data-stu-id="3fd79-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="3fd79-109">其他用途包括收集網路統計資料、取得有關網路入侵的資訊，以及偵錯用戶端與伺服器間的通訊等等。</span><span class="sxs-lookup"><span data-stu-id="3fd79-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="3fd79-110">在 Azure 中部署的資源會全年無休地執行。</span><span class="sxs-lookup"><span data-stu-id="3fd79-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="3fd79-111">您和您的員工無法主動監視所有資源 24/7 hello 的狀態。</span><span class="sxs-lookup"><span data-stu-id="3fd79-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="3fd79-112">例如，如果凌晨 2 點發生問題，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="3fd79-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="3fd79-113">使用網路監看員，警示，以及從 hello Azure 生態系統內的函式，您可以主動回應 hello 資料與工具 toosolve 問題與您網路中。</span><span class="sxs-lookup"><span data-stu-id="3fd79-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![案例][scenario]

## <a name="prerequisites"></a><span data-ttu-id="3fd79-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="3fd79-115">Prerequisites</span></span>

* <span data-ttu-id="3fd79-116">hello 最新版本的[Azure PowerShell](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="3fd79-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="3fd79-117">網路監看員的現有執行個體。</span><span class="sxs-lookup"><span data-stu-id="3fd79-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="3fd79-118">如果您還沒有，請[建立網路監看員執行個體](network-watcher-create.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd79-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="3fd79-119">在 [hello 中現有的虛擬機器網路監看員與相同的區域以 hello [Windows 擴充功能](../virtual-machines/windows/extensions-nwa.md)或[Linux 虛擬機器擴充功能](../virtual-machines/linux/extensions-nwa.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd79-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="3fd79-120">案例</span><span class="sxs-lookup"><span data-stu-id="3fd79-120">Scenario</span></span>

<span data-ttu-id="3fd79-121">在此範例中，您的 VM 正在傳送多個 TCP 區段比平常更久，而且您想 toobe 收到警示。</span><span class="sxs-lookup"><span data-stu-id="3fd79-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="3fd79-122">此處使用 TCP 區段做為範例，但您可以使用任何警示條件。</span><span class="sxs-lookup"><span data-stu-id="3fd79-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="3fd79-123">當您收到警示時，您想 tooreceive 封包層級資料 toounderstand 為什麼增加通訊。</span><span class="sxs-lookup"><span data-stu-id="3fd79-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="3fd79-124">然後您可以採取步驟 tooreturn hello 虛擬機器的 tooregular 通訊。</span><span class="sxs-lookup"><span data-stu-id="3fd79-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="3fd79-125">此案例假設您有現有的網路監看員執行個體，以及具有有效虛擬機器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3fd79-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="3fd79-126">下列清單中的 hello 是發生 hello 工作流程的概觀：</span><span class="sxs-lookup"><span data-stu-id="3fd79-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="3fd79-127">會在您的 VM 上觸發警示。</span><span class="sxs-lookup"><span data-stu-id="3fd79-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="3fd79-128">hello 警示呼叫 webhook 透過您 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="3fd79-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="3fd79-129">您的 Azure 函式會處理 hello 警示，並啟動網路監看員封包擷取工作階段。</span><span class="sxs-lookup"><span data-stu-id="3fd79-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="3fd79-130">hello 封包擷取 hello VM 上執行，並收集資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="3fd79-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="3fd79-131">hello 封包擷取檔案上傳 tooa 檢閱及診斷的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd79-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="3fd79-132">tooautomate 程序中，我們建立，並 hello 事件發生時，在我們的 VM tootrigger 連線警示。</span><span class="sxs-lookup"><span data-stu-id="3fd79-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="3fd79-133">我們也會建立到網路監看員的函式 toocall。</span><span class="sxs-lookup"><span data-stu-id="3fd79-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="3fd79-134">此案例中沒有 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="3fd79-134">This scenario does hello following:</span></span>

* <span data-ttu-id="3fd79-135">建立啟動封包擷取的 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="3fd79-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="3fd79-136">虛擬機器上建立警示規則並設定 hello 警示規則 toocall hello Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="3fd79-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="3fd79-137">建立 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="3fd79-137">Create an Azure function</span></span>

<span data-ttu-id="3fd79-138">hello 第一個步驟是 toocreate Azure 函式 tooprocess hello 警示，並建立封包擷取。</span><span class="sxs-lookup"><span data-stu-id="3fd79-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="3fd79-139">在 [hello [Azure 入口網站](https://portal.azure.com)，選取**新增** > **計算** > **函式應用程式**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![建立函數應用程式][1-1]

2. <span data-ttu-id="3fd79-141">在 [hello**函式應用程式**刀鋒視窗中，輸入下列值的 hello，然後選取**確定**toocreate hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="3fd79-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="3fd79-142">**設定**</span><span class="sxs-lookup"><span data-stu-id="3fd79-142">**Setting**</span></span> | <span data-ttu-id="3fd79-143">**值**</span><span class="sxs-lookup"><span data-stu-id="3fd79-143">**Value**</span></span> | <span data-ttu-id="3fd79-144">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="3fd79-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="3fd79-145">**應用程式名稱**</span><span class="sxs-lookup"><span data-stu-id="3fd79-145">**App name**</span></span>|<span data-ttu-id="3fd79-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="3fd79-146">PacketCaptureExample</span></span>|<span data-ttu-id="3fd79-147">hello 的 hello 函式應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fd79-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="3fd79-148">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="3fd79-148">**Subscription**</span></span>|<span data-ttu-id="3fd79-149">[訂用帳戶] hello 哪些 toocreate hello 函式應用程式的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd79-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="3fd79-150">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="3fd79-150">**Resource Group**</span></span>|<span data-ttu-id="3fd79-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="3fd79-151">PacketCaptureRG</span></span>|<span data-ttu-id="3fd79-152">hello 資源群組 toocontain hello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fd79-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="3fd79-153">**主控方案**</span><span class="sxs-lookup"><span data-stu-id="3fd79-153">**Hosting Plan**</span></span>|<span data-ttu-id="3fd79-154">取用方案</span><span class="sxs-lookup"><span data-stu-id="3fd79-154">Consumption Plan</span></span>| <span data-ttu-id="3fd79-155">hello 類型的計劃您函式的應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="3fd79-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="3fd79-156">選項有「取用」或 Azure App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="3fd79-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="3fd79-157">**位置**</span><span class="sxs-lookup"><span data-stu-id="3fd79-157">**Location**</span></span>|<span data-ttu-id="3fd79-158">美國中部</span><span class="sxs-lookup"><span data-stu-id="3fd79-158">Central US</span></span>| <span data-ttu-id="3fd79-159">哪些 toocreate hello 函式應用程式中的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="3fd79-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="3fd79-160">**儲存體帳戶**</span><span class="sxs-lookup"><span data-stu-id="3fd79-160">**Storage Account**</span></span>|<span data-ttu-id="3fd79-161">{自動產生}</span><span class="sxs-lookup"><span data-stu-id="3fd79-161">{autogenerated}</span></span>| <span data-ttu-id="3fd79-162">hello Azure 函式需要一般用途儲存體的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fd79-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="3fd79-163">在 [hello **PacketCaptureExample 函式應用程式**刀鋒視窗中，選取**函式** > **自訂函式** > ** +**.</span><span class="sxs-lookup"><span data-stu-id="3fd79-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="3fd79-164">選取**HttpTrigger Powershell**，然後輸入 hello 剩餘資訊。</span><span class="sxs-lookup"><span data-stu-id="3fd79-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="3fd79-165">最後，toocreate hello 函式，選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="3fd79-166">**設定**</span><span class="sxs-lookup"><span data-stu-id="3fd79-166">**Setting**</span></span> | <span data-ttu-id="3fd79-167">**值**</span><span class="sxs-lookup"><span data-stu-id="3fd79-167">**Value**</span></span> | <span data-ttu-id="3fd79-168">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="3fd79-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="3fd79-169">**案例**</span><span class="sxs-lookup"><span data-stu-id="3fd79-169">**Scenario**</span></span>|<span data-ttu-id="3fd79-170">實驗性</span><span class="sxs-lookup"><span data-stu-id="3fd79-170">Experimental</span></span>|<span data-ttu-id="3fd79-171">案例類型</span><span class="sxs-lookup"><span data-stu-id="3fd79-171">Type of scenario</span></span>|
    |<span data-ttu-id="3fd79-172">**函式命名**</span><span class="sxs-lookup"><span data-stu-id="3fd79-172">**Name your function**</span></span>|<span data-ttu-id="3fd79-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="3fd79-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="3fd79-174">Hello 函式的名稱</span><span class="sxs-lookup"><span data-stu-id="3fd79-174">Name of hello function</span></span>|
    |<span data-ttu-id="3fd79-175">**授權層級**</span><span class="sxs-lookup"><span data-stu-id="3fd79-175">**Authorization level**</span></span>|<span data-ttu-id="3fd79-176">函式</span><span class="sxs-lookup"><span data-stu-id="3fd79-176">Function</span></span>|<span data-ttu-id="3fd79-177">授權層級的 hello 函式</span><span class="sxs-lookup"><span data-stu-id="3fd79-177">Authorization level for hello function</span></span>|

![函式範例][functions1]

> [!NOTE]
> <span data-ttu-id="3fd79-179">hello PowerShell 範本屬實驗性質，而且沒有完整的支援。</span><span class="sxs-lookup"><span data-stu-id="3fd79-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="3fd79-180">自訂所需的這個範例與 hello 步驟中說明。</span><span class="sxs-lookup"><span data-stu-id="3fd79-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="3fd79-181">新增模組</span><span class="sxs-lookup"><span data-stu-id="3fd79-181">Add modules</span></span>

<span data-ttu-id="3fd79-182">toouse 網路監看員 PowerShell 指令程式上, 傳 hello 最新 PowerShell 模組 toohello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fd79-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="3fd79-183">在本機電腦與 hello 安裝最新 Azure PowerShell 模組，執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="3fd79-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="3fd79-184">此範例提供下列 hello Azure PowerShell 模組的本機路徑。</span><span class="sxs-lookup"><span data-stu-id="3fd79-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="3fd79-185">在接下來的步驟中會用到這些資料夾。</span><span class="sxs-lookup"><span data-stu-id="3fd79-185">These folders are used in a later step.</span></span> <span data-ttu-id="3fd79-186">此案例中使用的 hello 模組為：</span><span class="sxs-lookup"><span data-stu-id="3fd79-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="3fd79-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="3fd79-187">AzureRM.Network</span></span>

    * <span data-ttu-id="3fd79-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="3fd79-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="3fd79-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="3fd79-189">AzureRM.Resources</span></span>

    ![PowerShell 資料夾][functions5]

1. <span data-ttu-id="3fd79-191">選取**函式應用程式設定** > **移 tooApp 服務編輯器**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![函數應用程式設定][functions2]

1. <span data-ttu-id="3fd79-193">以滑鼠右鍵按一下 hello **AlertPacketCapturePowershell**資料夾，然後建立名為的資料夾**azuremodules**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="3fd79-194">為您需要的每個模組建立子資料夾。</span><span class="sxs-lookup"><span data-stu-id="3fd79-194">Create a subfolder for each module that you need.</span></span>

    ![資料夾和子資料夾][functions3]

    * <span data-ttu-id="3fd79-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="3fd79-196">AzureRM.Network</span></span>

    * <span data-ttu-id="3fd79-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="3fd79-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="3fd79-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="3fd79-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="3fd79-199">以滑鼠右鍵按一下 hello **AzureRM.Network**子資料夾，然後再選取**上載檔案**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="3fd79-200">移 tooyour Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="3fd79-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="3fd79-201">Hello 本機**AzureRM.Network**資料夾中，選取 hello 資料夾中的 hello 的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="3fd79-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="3fd79-202">然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="3fd79-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="3fd79-203">針對 **AzureRM.Profile** 和 **AzureRM.Resources** 重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="3fd79-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![上傳檔案][functions6]

1. <span data-ttu-id="3fd79-205">您已完成，每個資料夾應該具有 hello PowerShell 模組檔案從本機電腦。</span><span class="sxs-lookup"><span data-stu-id="3fd79-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![PowerShell 檔案][functions7]

### <a name="authentication"></a><span data-ttu-id="3fd79-207">驗證</span><span class="sxs-lookup"><span data-stu-id="3fd79-207">Authentication</span></span>

<span data-ttu-id="3fd79-208">toouse hello PowerShell cmdlet，您必須進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3fd79-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="3fd79-209">您可以設定驗證 hello 函式應用程式中。</span><span class="sxs-lookup"><span data-stu-id="3fd79-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="3fd79-210">tooconfigure 驗證，您必須設定環境變數，並上傳加密的金鑰檔 toohello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fd79-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="3fd79-211">此案例中提供一個範例將示範如何搭配 Azure 函式的 tooimplement 驗證。</span><span class="sxs-lookup"><span data-stu-id="3fd79-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="3fd79-212">有其他方式 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="3fd79-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="3fd79-213">加密的認證</span><span class="sxs-lookup"><span data-stu-id="3fd79-213">Encrypted credentials</span></span>

<span data-ttu-id="3fd79-214">下列 PowerShell 指令碼的 hello 建立金鑰檔稱為**PassEncryptKey.key**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="3fd79-215">它也提供 hello 密碼所提供的加密的版本。</span><span class="sxs-lookup"><span data-stu-id="3fd79-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="3fd79-216">此密碼為 hello 定義用來驗證 hello Azure Active Directory 應用程式的相同密碼。</span><span class="sxs-lookup"><span data-stu-id="3fd79-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="3fd79-217">在 hello 的 hello 函式應用程式的應用程式服務編輯器，建立資料夾，稱為**金鑰**下**AlertPacketCapturePowerShell**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="3fd79-218">然後上傳 hello **PassEncryptKey.key**在 hello 先前的 PowerShell 範例中所建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="3fd79-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![函式金鑰][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="3fd79-220">擷取環境變數的值</span><span class="sxs-lookup"><span data-stu-id="3fd79-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="3fd79-221">hello 最終的需求是 tooset hello 環境變數是可驗證的必要 tooaccess hello 值組成。</span><span class="sxs-lookup"><span data-stu-id="3fd79-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="3fd79-222">hello 下列清單顯示 hello 而建立的環境變數：</span><span class="sxs-lookup"><span data-stu-id="3fd79-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="3fd79-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="3fd79-223">AzureClientID</span></span>

* <span data-ttu-id="3fd79-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="3fd79-224">AzureTenant</span></span>

* <span data-ttu-id="3fd79-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="3fd79-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="3fd79-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="3fd79-226">AzureClientID</span></span>

<span data-ttu-id="3fd79-227">hello 用戶端識別碼是在 Azure Active Directory 之應用程式的應用程式識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="3fd79-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="3fd79-228">如果您還沒有應用程式 toouse，執行下列範例 toocreate hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fd79-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="3fd79-229">hello 密碼時建立 hello 應用程式應該是 hello 使用您稍早建立 hello 金鑰檔案儲存時的相同密碼。</span><span class="sxs-lookup"><span data-stu-id="3fd79-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="3fd79-230">在 [hello Azure 入口網站，選取 [**訂閱**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="3fd79-231">選取 hello 訂用帳戶 toouse，，然後選取**存取控制 (IAM)**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![函式 IAM][functions9]

1. <span data-ttu-id="3fd79-233">選擇 hello 帳戶 toouse，，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="3fd79-234">複製 hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="3fd79-234">Copy hello Application ID.</span></span>

    ![函數應用程式識別碼][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="3fd79-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="3fd79-236">AzureTenant</span></span>

<span data-ttu-id="3fd79-237">藉由執行下列 PowerShell 範例 hello 取得 hello 租用戶識別碼：</span><span class="sxs-lookup"><span data-stu-id="3fd79-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="3fd79-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="3fd79-238">AzureCredPassword</span></span>

<span data-ttu-id="3fd79-239">您從執行下列 PowerShell 範例 hello 取得的 hello 值為 hello hello AzureCredPassword 環境變數值。</span><span class="sxs-lookup"><span data-stu-id="3fd79-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="3fd79-240">這個範例是 hello 同一個 hello 前面所示**加密認證**> 一節。</span><span class="sxs-lookup"><span data-stu-id="3fd79-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="3fd79-241">hello 所需的值是 hello hello 輸出`$Encryptedpassword`變數。</span><span class="sxs-lookup"><span data-stu-id="3fd79-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="3fd79-242">這是 hello 服務主體的密碼加密使用 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="3fd79-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="3fd79-243">存放區 hello 環境變數</span><span class="sxs-lookup"><span data-stu-id="3fd79-243">Store hello environment variables</span></span>

1. <span data-ttu-id="3fd79-244">移 toohello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3fd79-244">Go toohello function app.</span></span> <span data-ttu-id="3fd79-245">然後選取 [函數應用程式設定] > [設定應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="3fd79-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![進行應用程式設定][functions11]

1. <span data-ttu-id="3fd79-247">加入 hello 環境變數和其值 toohello 應用程式設定，然後選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![應用程式設定][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="3fd79-249">新增 PowerShell toohello 函式</span><span class="sxs-lookup"><span data-stu-id="3fd79-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="3fd79-250">它是現在時間 toomake 內 hello Azure 函式呼叫從網路監看員。</span><span class="sxs-lookup"><span data-stu-id="3fd79-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="3fd79-251">根據 hello 的需求，此函式 hello 實作而有所不同。</span><span class="sxs-lookup"><span data-stu-id="3fd79-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="3fd79-252">不過，hello hello 程式碼的一般流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="3fd79-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="3fd79-253">處理輸入參數。</span><span class="sxs-lookup"><span data-stu-id="3fd79-253">Process input parameters.</span></span>
2. <span data-ttu-id="3fd79-254">查詢現有的封包擷取 tooverify 限制，並解決名稱衝突。</span><span class="sxs-lookup"><span data-stu-id="3fd79-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="3fd79-255">使用適當的參數建立封包擷取。</span><span class="sxs-lookup"><span data-stu-id="3fd79-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="3fd79-256">定期輪詢封包擷取，直到完成。</span><span class="sxs-lookup"><span data-stu-id="3fd79-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="3fd79-257">通知 hello 使用者 hello 封包擷取工作階段已完成。</span><span class="sxs-lookup"><span data-stu-id="3fd79-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="3fd79-258">hello 下列範例是可以在 hello 函式中使用的 PowerShell 程式碼。</span><span class="sxs-lookup"><span data-stu-id="3fd79-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="3fd79-259">沒有需要 toobe 取代的值**subscriptionId**， **resourceGroupName**，和**storageAccountName**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="3fd79-260">擷取 hello 函式 URL</span><span class="sxs-lookup"><span data-stu-id="3fd79-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="3fd79-261">您已建立您的函式之後，設定您的警示 toocall hello URL 與 hello 函式相關聯。</span><span class="sxs-lookup"><span data-stu-id="3fd79-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="3fd79-262">tooget 此值，請從您的函式應用程式複本 hello 函式的 URL。</span><span class="sxs-lookup"><span data-stu-id="3fd79-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![尋找 hello 函式 URL][functions13]

2. <span data-ttu-id="3fd79-264">複製應用程式函式的 hello 函式 URL。</span><span class="sxs-lookup"><span data-stu-id="3fd79-264">Copy hello function URL for your function app.</span></span>

    ![複製的 hello 函式 URL][2]

<span data-ttu-id="3fd79-266">如果您需要在 hello 承載中的 hello webhook POST 要求的自訂屬性，請參閱太[Azure 度量警示上設定的 webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd79-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="3fd79-267">在 VM 上設定警示</span><span class="sxs-lookup"><span data-stu-id="3fd79-267">Configure an alert on a VM</span></span>

<span data-ttu-id="3fd79-268">當特定的度量超出指定閾值時，警示可以是設定的 toonotify 個人 tooit。</span><span class="sxs-lookup"><span data-stu-id="3fd79-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="3fd79-269">在此範例中，hello 警示在 hello TCP 區段傳送，但可以用於許多其他的度量觸發 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="3fd79-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="3fd79-270">在此範例中，警示會是設定的 toocall webhook toocall hello 函式。</span><span class="sxs-lookup"><span data-stu-id="3fd79-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="3fd79-271">建立 hello 警示規則</span><span class="sxs-lookup"><span data-stu-id="3fd79-271">Create hello alert rule</span></span>

<span data-ttu-id="3fd79-272">移 tooan 現有的虛擬機器，然後再加入 [警示規則。</span><span class="sxs-lookup"><span data-stu-id="3fd79-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="3fd79-273">如需設定警示相關的詳細文件，請參閱[在 Azure 服務的 Azure 監視器中建立警示 - Azure 入口網站](../monitoring-and-diagnostics/insights-alerts-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd79-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="3fd79-274">輸入下列 hello 中的值的 hello**警示規則**刀鋒視窗中，然後再選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="3fd79-275">**設定**</span><span class="sxs-lookup"><span data-stu-id="3fd79-275">**Setting**</span></span> | <span data-ttu-id="3fd79-276">**值**</span><span class="sxs-lookup"><span data-stu-id="3fd79-276">**Value**</span></span> | <span data-ttu-id="3fd79-277">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="3fd79-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="3fd79-278">**名稱**</span><span class="sxs-lookup"><span data-stu-id="3fd79-278">**Name**</span></span>|<span data-ttu-id="3fd79-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="3fd79-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="3fd79-280">Hello 警示規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fd79-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="3fd79-281">**說明**</span><span class="sxs-lookup"><span data-stu-id="3fd79-281">**Description**</span></span>|<span data-ttu-id="3fd79-282">傳送的 TCP 區段超出閾值</span><span class="sxs-lookup"><span data-stu-id="3fd79-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="3fd79-283">hello hello 警示規則的描述。</span><span class="sxs-lookup"><span data-stu-id="3fd79-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="3fd79-284">**度量**</span><span class="sxs-lookup"><span data-stu-id="3fd79-284">**Metric**</span></span>|<span data-ttu-id="3fd79-285">傳送的 TCP 區段</span><span class="sxs-lookup"><span data-stu-id="3fd79-285">TCP segments sent</span></span>| <span data-ttu-id="3fd79-286">hello 度量 toouse tootrigger hello 警示。</span><span class="sxs-lookup"><span data-stu-id="3fd79-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="3fd79-287">**Condition**</span><span class="sxs-lookup"><span data-stu-id="3fd79-287">**Condition**</span></span>|<span data-ttu-id="3fd79-288">大於</span><span class="sxs-lookup"><span data-stu-id="3fd79-288">Greater than</span></span>| <span data-ttu-id="3fd79-289">hello 條件 toouse 評估 hello 度量時。</span><span class="sxs-lookup"><span data-stu-id="3fd79-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="3fd79-290">**閾值**</span><span class="sxs-lookup"><span data-stu-id="3fd79-290">**Threshold**</span></span>|<span data-ttu-id="3fd79-291">100</span><span class="sxs-lookup"><span data-stu-id="3fd79-291">100</span></span>| <span data-ttu-id="3fd79-292">hello 觸發 hello 警示的 hello 標準值。</span><span class="sxs-lookup"><span data-stu-id="3fd79-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="3fd79-293">這個值應該設定 tooa 有效的值，為您的環境。</span><span class="sxs-lookup"><span data-stu-id="3fd79-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="3fd79-294">**期間**</span><span class="sxs-lookup"><span data-stu-id="3fd79-294">**Period**</span></span>|<span data-ttu-id="3fd79-295">透過 hello 前五分鐘</span><span class="sxs-lookup"><span data-stu-id="3fd79-295">Over hello last five minutes</span></span>| <span data-ttu-id="3fd79-296">決定哪些 toolook 中的 hello 期間 hello 上 hello 度量的閾值。</span><span class="sxs-lookup"><span data-stu-id="3fd79-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="3fd79-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="3fd79-297">**Webhook**</span></span>|<span data-ttu-id="3fd79-298">[函數應用程式中的 Webhook URL]</span><span class="sxs-lookup"><span data-stu-id="3fd79-298">[webhook URL from function app]</span></span>| <span data-ttu-id="3fd79-299">hello 前述步驟中建立的 hello 函式應用程式中的 hello webhook URL。</span><span class="sxs-lookup"><span data-stu-id="3fd79-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="3fd79-300">預設不啟用 hello TCP 區段度量。</span><span class="sxs-lookup"><span data-stu-id="3fd79-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="3fd79-301">深入了解如何 tooenable 其他度量造訪[啟用監視和診斷](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd79-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="3fd79-302">檢閱 hello 結果</span><span class="sxs-lookup"><span data-stu-id="3fd79-302">Review hello results</span></span>

<span data-ttu-id="3fd79-303">之後的 hello 警示觸發程序 hello 準則中，會建立封包擷取。</span><span class="sxs-lookup"><span data-stu-id="3fd79-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="3fd79-304">移 tooNetwork 監看員，然後再選取**封包擷取**。</span><span class="sxs-lookup"><span data-stu-id="3fd79-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="3fd79-305">這個頁面上，您可以選取 hello 封包擷取檔案連結 toodownload hello 封包擷取。</span><span class="sxs-lookup"><span data-stu-id="3fd79-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![檢視封包擷取][functions14]

<span data-ttu-id="3fd79-307">如果在本機儲存 hello 擷取檔案，您可以登入 toohello 虛擬機器來擷取。</span><span class="sxs-lookup"><span data-stu-id="3fd79-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="3fd79-308">如需從 Azure 儲存體帳戶下載檔案的指示，請參閱[以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd79-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="3fd79-309">另一個可用的工具是[儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="3fd79-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="3fd79-310">下載您的擷取後，您可以使用可讀取 **.cap** 檔案的任何工具來檢視它。</span><span class="sxs-lookup"><span data-stu-id="3fd79-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="3fd79-311">以下是這些工具的連結 tootwo:</span><span class="sxs-lookup"><span data-stu-id="3fd79-311">Following are links tootwo of these tools:</span></span>

- [<span data-ttu-id="3fd79-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="3fd79-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="3fd79-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="3fd79-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="3fd79-314">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fd79-314">Next steps</span></span>

<span data-ttu-id="3fd79-315">了解如何 tooview 您擷取封包造訪[Wireshark 封包擷取分析](network-watcher-deep-packet-inspection.md)。</span><span class="sxs-lookup"><span data-stu-id="3fd79-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
