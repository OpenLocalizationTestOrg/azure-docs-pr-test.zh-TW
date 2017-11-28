---
title: "aaaMonitor VPN 閘道與 Azure 網路監看員疑難排解 |Microsoft 文件"
description: "本文說明如何使用 Azure 自動化和網路監看員診斷內部部署連線"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="872ba-103">使用網路監看員疑難排解來監視 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="872ba-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="872ba-104">取得對網路效能的深入分析是重大 tooprovide 可靠服務 toocustomers。</span><span class="sxs-lookup"><span data-stu-id="872ba-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="872ba-105">它是關鍵 toodetect 網路中斷狀況快速而採取矯正措施 toomitigate hello 中斷情況。</span><span class="sxs-lookup"><span data-stu-id="872ba-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="872ba-106">Azure 自動化可讓您 tooimplement，並透過 runbook，以程式設計的方式執行工作。</span><span class="sxs-lookup"><span data-stu-id="872ba-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="872ba-107">使用 Azure 自動化會建立一個完美的配方，讓您執行連續且主動的網路監視和警示。</span><span class="sxs-lookup"><span data-stu-id="872ba-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="872ba-108">案例</span><span class="sxs-lookup"><span data-stu-id="872ba-108">Scenario</span></span>

<span data-ttu-id="872ba-109">hello 下列映像中的 hello 案例位於多層式應用程式中，以建立使用 VPN 閘道和通道的內部部署連線。</span><span class="sxs-lookup"><span data-stu-id="872ba-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="872ba-110">確保的 hello VPN 閘道已啟動及執行 」 是重大 toohello 應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="872ba-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="872ba-111">Hello VPN 通道，使用 hello 資源疑難排解 API toocheck 的連線通道狀態的連接狀態的指令碼 toocheck 建立 runbook。</span><span class="sxs-lookup"><span data-stu-id="872ba-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="872ba-112">Tooadministrators 如果 hello 狀態狀況不良，傳送電子郵件觸發程序。</span><span class="sxs-lookup"><span data-stu-id="872ba-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![案例範例][scenario]

<span data-ttu-id="872ba-114">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="872ba-114">This scenario will:</span></span>

- <span data-ttu-id="872ba-115">建立 runbook 呼叫 hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot 連線狀態</span><span class="sxs-lookup"><span data-stu-id="872ba-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="872ba-116">排程 toohello runbook 連結</span><span class="sxs-lookup"><span data-stu-id="872ba-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="872ba-117">開始之前</span><span class="sxs-lookup"><span data-stu-id="872ba-117">Before you begin</span></span>

<span data-ttu-id="872ba-118">在開始這個案例之前，您必須擁有 hello 下列先決條件：</span><span class="sxs-lookup"><span data-stu-id="872ba-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="872ba-119">在 Azure 中使用 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="872ba-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="872ba-120">請確認 hello 自動化帳戶有 hello 最新的模組，然後也有 hello AzureRM.Network 模組。</span><span class="sxs-lookup"><span data-stu-id="872ba-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="872ba-121">hello AzureRM.Network 模組位於 hello 模組資源庫如果您需要 tooadd 它 tooyour 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="872ba-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="872ba-122">您必須在 Azure 自動化中設定一組認證。</span><span class="sxs-lookup"><span data-stu-id="872ba-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="872ba-123">在 [Azure 自動化安全性](../automation/automation-security-overview.md)深入了解</span><span class="sxs-lookup"><span data-stu-id="872ba-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="872ba-124">有效的 SMTP 伺服器 (Office 365、您的內部部署電子郵件或其他) 和 Azure 自動化中定義的認證</span><span class="sxs-lookup"><span data-stu-id="872ba-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="872ba-125">在 Azure 中已設定的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="872ba-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="872ba-126">現有的容器 toostore hello 的現有儲存體帳戶記錄中。</span><span class="sxs-lookup"><span data-stu-id="872ba-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="872ba-127">hello 前面影像所示的 hello 基礎結構供說明用途並不會建立 hello 本文中所包含的步驟。</span><span class="sxs-lookup"><span data-stu-id="872ba-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="872ba-128">建立 hello runbook</span><span class="sxs-lookup"><span data-stu-id="872ba-128">Create hello runbook</span></span>

<span data-ttu-id="872ba-129">hello 第一個步驟 tooconfiguring hello 範例是 toocreate hello runbook。</span><span class="sxs-lookup"><span data-stu-id="872ba-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="872ba-130">這個範例會使用「執行身分」帳戶。</span><span class="sxs-lookup"><span data-stu-id="872ba-130">This example uses a run-as account.</span></span> <span data-ttu-id="872ba-131">toolearn 需執行身分帳戶，請瀏覽[驗證 Runbook 與 Azure 執行身分帳戶](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="872ba-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="872ba-132">步驟 1</span><span class="sxs-lookup"><span data-stu-id="872ba-132">Step 1</span></span>

<span data-ttu-id="872ba-133">瀏覽 tooAzure 自動化在 hello [Azure 入口網站](https://portal.azure.com)按一下**Runbook**</span><span class="sxs-lookup"><span data-stu-id="872ba-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![自動化帳戶概觀][1]

### <a name="step-2"></a><span data-ttu-id="872ba-135">步驟 2</span><span class="sxs-lookup"><span data-stu-id="872ba-135">Step 2</span></span>

<span data-ttu-id="872ba-136">按一下**新增 runbook** toostart hello runbook 的 hello 建立程序。</span><span class="sxs-lookup"><span data-stu-id="872ba-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![runbook 刀鋒視窗][2]

### <a name="step-3"></a><span data-ttu-id="872ba-138">步驟 3</span><span class="sxs-lookup"><span data-stu-id="872ba-138">Step 3</span></span>

<span data-ttu-id="872ba-139">在下**快速建立**，按一下 **建立新的 runbook** toocreate hello runbook。</span><span class="sxs-lookup"><span data-stu-id="872ba-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![新增 runbook 刀鋒視窗][3]

### <a name="step-4"></a><span data-ttu-id="872ba-141">步驟 4</span><span class="sxs-lookup"><span data-stu-id="872ba-141">Step 4</span></span>

<span data-ttu-id="872ba-142">在此步驟中，我們為 hello runbook 的名稱，在 hello 範例中呼叫它**Get VPNGatewayStatus**。</span><span class="sxs-lookup"><span data-stu-id="872ba-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="872ba-143">它是重要的 toogive hello runbook 的描述性的名稱，並建議以遵循標準 PowerShell 命名標準的名稱。</span><span class="sxs-lookup"><span data-stu-id="872ba-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="872ba-144">此範例中的 hello runbook 類型為**PowerShell**，hello 其他選項包括圖形，PowerShell 工作流程，以及圖形化 PowerShell 工作流程。</span><span class="sxs-lookup"><span data-stu-id="872ba-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![runbook 刀鋒視窗][4]

### <a name="step-5"></a><span data-ttu-id="872ba-146">步驟 5</span><span class="sxs-lookup"><span data-stu-id="872ba-146">Step 5</span></span>

<span data-ttu-id="872ba-147">在此步驟中 hello 建立 runbook、 hello 下列程式碼範例提供所有 hello hello 範例所需的程式碼。</span><span class="sxs-lookup"><span data-stu-id="872ba-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="872ba-148">hello hello 程式碼中包含的項目\<值\>需要 toobe hello 從您的訂用帳戶的值取代。</span><span class="sxs-lookup"><span data-stu-id="872ba-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="872ba-149">使用 hello 下列程式碼為按一下**儲存**</span><span class="sxs-lookup"><span data-stu-id="872ba-149">Use hello following code as click **Save**</span></span>

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a><span data-ttu-id="872ba-150">步驟 6</span><span class="sxs-lookup"><span data-stu-id="872ba-150">Step 6</span></span>

<span data-ttu-id="872ba-151">排程 hello runbook 儲存之後，必須是連結的 hello runbook tooit tooautomate hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="872ba-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="872ba-152">toostart hello 程序中，按一下 **排程**。</span><span class="sxs-lookup"><span data-stu-id="872ba-152">toostart hello process, click **Schedule**.</span></span>

![步驟 6][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="872ba-154">排程 toohello runbook 連結</span><span class="sxs-lookup"><span data-stu-id="872ba-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="872ba-155">您必須建立新的排程。</span><span class="sxs-lookup"><span data-stu-id="872ba-155">A new schedule must be created.</span></span> <span data-ttu-id="872ba-156">按一下**排程 tooyour runbook 連結**。</span><span class="sxs-lookup"><span data-stu-id="872ba-156">Click **Link a schedule tooyour runbook**.</span></span>

![步驟 7][7]

### <a name="step-1"></a><span data-ttu-id="872ba-158">步驟 1</span><span class="sxs-lookup"><span data-stu-id="872ba-158">Step 1</span></span>

<span data-ttu-id="872ba-159">在 hello**排程**刀鋒視窗中，按一下 **建立新的排程**</span><span class="sxs-lookup"><span data-stu-id="872ba-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![步驟 8][8]

### <a name="step-2"></a><span data-ttu-id="872ba-161">步驟 2</span><span class="sxs-lookup"><span data-stu-id="872ba-161">Step 2</span></span>

<span data-ttu-id="872ba-162">在 hello**新排程**刀鋒視窗填滿 hello 排程資訊。</span><span class="sxs-lookup"><span data-stu-id="872ba-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="872ba-163">您可以將的 hello 值為 hello 下列清單中：</span><span class="sxs-lookup"><span data-stu-id="872ba-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="872ba-164">**名稱**-hello hello 排程的好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="872ba-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="872ba-165">**描述**-hello 排程的描述。</span><span class="sxs-lookup"><span data-stu-id="872ba-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="872ba-166">**啟動**-這個值是日期、 時間和時區 hello 時間 hello 排程觸發程序所構成的組合。</span><span class="sxs-lookup"><span data-stu-id="872ba-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="872ba-167">**循環**-這個值會決定 hello 排程重複。</span><span class="sxs-lookup"><span data-stu-id="872ba-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="872ba-168">有效值為 [一次] 或 [重複]。</span><span class="sxs-lookup"><span data-stu-id="872ba-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="872ba-169">**循環每**-小時、 天、 週或月中的 hello 排程 hello 循環間隔。</span><span class="sxs-lookup"><span data-stu-id="872ba-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="872ba-170">**設定到期日**-hello 值會決定 hello 排程是否應過期。</span><span class="sxs-lookup"><span data-stu-id="872ba-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="872ba-171">您可以將太**是**或**否**。</span><span class="sxs-lookup"><span data-stu-id="872ba-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="872ba-172">有效的日期和時間是 toobe 提供如果選擇 [是]。</span><span class="sxs-lookup"><span data-stu-id="872ba-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="872ba-173">如果您需要 toohave 頻率超過每個小時以上執行 runbook 時，必須在不同的時間間隔 （也就是 15、 30-45 分鐘內，在 hello 小時後） 建立多個排程</span><span class="sxs-lookup"><span data-stu-id="872ba-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![步驟 9][9]

### <a name="step-3"></a><span data-ttu-id="872ba-175">步驟 3</span><span class="sxs-lookup"><span data-stu-id="872ba-175">Step 3</span></span>

<span data-ttu-id="872ba-176">按一下 儲存 toosave hello 排程 toohello runbook。</span><span class="sxs-lookup"><span data-stu-id="872ba-176">Click Save toosave hello schedule toohello runbook.</span></span>

![步驟 10][10]

## <a name="next-steps"></a><span data-ttu-id="872ba-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="872ba-178">Next steps</span></span>

<span data-ttu-id="872ba-179">既然您已了解如何 toointegrate 網路監看員疑難排解 Azure 自動化中，以了解如何 tootrigger 擷取封包 VM 警示造訪[與 Azure 網路監看員建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="872ba-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
