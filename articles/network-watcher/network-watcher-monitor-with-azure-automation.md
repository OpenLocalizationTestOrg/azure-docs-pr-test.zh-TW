---
title: "使用 Azure 網路監看員疑難排解來監視 VPN 閘道 | Microsoft Docs"
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
ms.openlocfilehash: 55ec52dd0d94a0347cc67a8785b89611da955111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="636ac-103">使用網路監看員疑難排解來監視 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="636ac-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="636ac-104">深入了解網路效能對於為客戶提供可靠的服務相當重要。</span><span class="sxs-lookup"><span data-stu-id="636ac-104">Gaining deep insights on your network performance is critical to provide reliable services to customers.</span></span> <span data-ttu-id="636ac-105">因此務必快速偵測網路中斷狀況，並採取更正動作以降低中斷條件。</span><span class="sxs-lookup"><span data-stu-id="636ac-105">It is therefore critical to detect network outage conditions quickly and take corrective action to mitigate the outage condition.</span></span> <span data-ttu-id="636ac-106">Azure 自動化可讓您實作，並透過 runbook 以程式設計方式執行工作。</span><span class="sxs-lookup"><span data-stu-id="636ac-106">Azure Automation enables you to implement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="636ac-107">使用 Azure 自動化會建立一個完美的配方，讓您執行連續且主動的網路監視和警示。</span><span class="sxs-lookup"><span data-stu-id="636ac-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="636ac-108">案例</span><span class="sxs-lookup"><span data-stu-id="636ac-108">Scenario</span></span>

<span data-ttu-id="636ac-109">下圖中的案例是多層式應用程式，並具有使用 VPN 閘道與通道建立的內部部署連線。</span><span class="sxs-lookup"><span data-stu-id="636ac-109">The scenario in the following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="636ac-110">確保 VPN 閘道已啟動且執行對於應用程式效能很重要。</span><span class="sxs-lookup"><span data-stu-id="636ac-110">Ensuring the VPN Gateway is up and running is critical to the applications performance.</span></span>

<span data-ttu-id="636ac-111">Runbook 會使用資源疑難排解 API 檢查連線狀態，利用指令碼檢查 VPN 通道連線狀態來建立。</span><span class="sxs-lookup"><span data-stu-id="636ac-111">A runbook is created with a script to check for connection status of the VPN tunnel, using the Resource Troubleshooting API to check for connection tunnel status.</span></span> <span data-ttu-id="636ac-112">如果狀態不是狀況良好，會傳送電子郵件觸發程序給系統管理員。</span><span class="sxs-lookup"><span data-stu-id="636ac-112">If the status is not healthy, an email trigger is sent to administrators.</span></span>

![案例範例][scenario]

<span data-ttu-id="636ac-114">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="636ac-114">This scenario will:</span></span>

- <span data-ttu-id="636ac-115">建立 runbook 呼叫 `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet 來疑難排解連線狀態</span><span class="sxs-lookup"><span data-stu-id="636ac-115">Create a runbook calling the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet to troubleshoot connection status</span></span>
- <span data-ttu-id="636ac-116">將排程連結至 runbook</span><span class="sxs-lookup"><span data-stu-id="636ac-116">Link a schedule to the runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="636ac-117">開始之前</span><span class="sxs-lookup"><span data-stu-id="636ac-117">Before you begin</span></span>

<span data-ttu-id="636ac-118">開始進行本案例之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="636ac-118">Before you start this scenario, you must have the following pre-requisites:</span></span>

- <span data-ttu-id="636ac-119">在 Azure 中使用 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="636ac-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="636ac-120">確認自動化帳戶有最新模組，並且也有 AzureRM.Network 模組。</span><span class="sxs-lookup"><span data-stu-id="636ac-120">Ensure that the automation account has the latest modules and also has the AzureRM.Network module.</span></span> <span data-ttu-id="636ac-121">如果您需要將 AzureRM.Network 模組新增至自動化帳戶，可從模組庫取得。</span><span class="sxs-lookup"><span data-stu-id="636ac-121">The AzureRM.Network module is available in the module gallery if you need to add it to your automation account.</span></span>
- <span data-ttu-id="636ac-122">您必須在 Azure 自動化中設定一組認證。</span><span class="sxs-lookup"><span data-stu-id="636ac-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="636ac-123">在 [Azure 自動化安全性](../automation/automation-security-overview.md)深入了解</span><span class="sxs-lookup"><span data-stu-id="636ac-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="636ac-124">有效的 SMTP 伺服器 (Office 365、您的內部部署電子郵件或其他) 和 Azure 自動化中定義的認證</span><span class="sxs-lookup"><span data-stu-id="636ac-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="636ac-125">在 Azure 中已設定的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="636ac-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="636ac-126">具有現有容器的儲存體帳戶，用於儲存記錄。</span><span class="sxs-lookup"><span data-stu-id="636ac-126">An existing storage account with an existing container to store the logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="636ac-127">上圖所示的基礎結構供說明用途，並不會使用本文中所包含的步驟建立。</span><span class="sxs-lookup"><span data-stu-id="636ac-127">The infrastructure depicted in the preceding image is for illustration purposes and are not created with the steps contained in this article.</span></span>

### <a name="create-the-runbook"></a><span data-ttu-id="636ac-128">建立 runbook</span><span class="sxs-lookup"><span data-stu-id="636ac-128">Create the runbook</span></span>

<span data-ttu-id="636ac-129">設定範例的第一個步驟是建立 runbook。</span><span class="sxs-lookup"><span data-stu-id="636ac-129">The first step to configuring the example is to create the runbook.</span></span> <span data-ttu-id="636ac-130">這個範例會使用「執行身分」帳戶。</span><span class="sxs-lookup"><span data-stu-id="636ac-130">This example uses a run-as account.</span></span> <span data-ttu-id="636ac-131">若要深入了解執行身分帳戶，請造訪[使用 Azure 執行身分帳戶驗證 Runbook](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="636ac-131">To learn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="636ac-132">步驟 1</span><span class="sxs-lookup"><span data-stu-id="636ac-132">Step 1</span></span>

<span data-ttu-id="636ac-133">在 [Azure 入口網站](https://portal.azure.com)中瀏覽至 Azure 自動化中並按一下 **Runbook**</span><span class="sxs-lookup"><span data-stu-id="636ac-133">Navigate to Azure Automation in the [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![自動化帳戶概觀][1]

### <a name="step-2"></a><span data-ttu-id="636ac-135">步驟 2</span><span class="sxs-lookup"><span data-stu-id="636ac-135">Step 2</span></span>

<span data-ttu-id="636ac-136">按一下 [新增 runbook] 來啟動 runbook 的建立程序。</span><span class="sxs-lookup"><span data-stu-id="636ac-136">Click **Add a runbook** to start the creation process of the runbook.</span></span>

![runbook 刀鋒視窗][2]

### <a name="step-3"></a><span data-ttu-id="636ac-138">步驟 3</span><span class="sxs-lookup"><span data-stu-id="636ac-138">Step 3</span></span>

<span data-ttu-id="636ac-139">在 [快速建立] 下，按一下 [建立新的 runbook] 來建立 runbook。</span><span class="sxs-lookup"><span data-stu-id="636ac-139">Under **Quick Create**, click **Create a new runbook** to create the runbook.</span></span>

![新增 runbook 刀鋒視窗][3]

### <a name="step-4"></a><span data-ttu-id="636ac-141">步驟 4</span><span class="sxs-lookup"><span data-stu-id="636ac-141">Step 4</span></span>

<span data-ttu-id="636ac-142">在此步驟中，我們為 runbook 命名，在範例中它稱為 **Get-VPNGatewayStatus**。</span><span class="sxs-lookup"><span data-stu-id="636ac-142">In this step, we give the runbook a name, in the example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="636ac-143">為 runbook 提供描述性的名稱很重要，且建議以遵循標準 PowerShell 命名標準來命名。</span><span class="sxs-lookup"><span data-stu-id="636ac-143">It is important to give the runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="636ac-144">此範例中的 runbook 類型是 **PowerShell**，其他選項包括圖形、PowerShell 工作流程和圖形化的 PowerShell 工作流程。</span><span class="sxs-lookup"><span data-stu-id="636ac-144">The runbook type for this example is **PowerShell**, the other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![runbook 刀鋒視窗][4]

### <a name="step-5"></a><span data-ttu-id="636ac-146">步驟 5</span><span class="sxs-lookup"><span data-stu-id="636ac-146">Step 5</span></span>

<span data-ttu-id="636ac-147">runbook 會在此步驟中建立，下列程式碼範例會提供範例所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="636ac-147">In this step the runbook is created, the following code example provides all the code needed for the example.</span></span> <span data-ttu-id="636ac-148">在程式碼中包含\<值\>的項目必須換成您訂用帳戶中的值。</span><span class="sxs-lookup"><span data-stu-id="636ac-148">The items in the code that contain \<value\> need to be replaced with the values from your subscription.</span></span>

<span data-ttu-id="636ac-149">按一下 [儲存] 使用下列程式碼</span><span class="sxs-lookup"><span data-stu-id="636ac-149">Use the following code as click **Save**</span></span>

```PowerShell
# Set these variables to the proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<to email address>"
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

# Get the connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in to Azure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context to a specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView the logs at $($storagePath) to learn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -To $toEmail `
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

### <a name="step-6"></a><span data-ttu-id="636ac-150">步驟 6</span><span class="sxs-lookup"><span data-stu-id="636ac-150">Step 6</span></span>

<span data-ttu-id="636ac-151">儲存 runbook 後，排程必須連結到它以自動啟動 runbook。</span><span class="sxs-lookup"><span data-stu-id="636ac-151">Once the runbook is saved, a schedule must be linked to it to automate the start of the runbook.</span></span> <span data-ttu-id="636ac-152">若要啟動處理程序，請按一下 [排程]。</span><span class="sxs-lookup"><span data-stu-id="636ac-152">To start the process, click **Schedule**.</span></span>

![步驟 6][6]

## <a name="link-a-schedule-to-the-runbook"></a><span data-ttu-id="636ac-154">將排程連結至 runbook</span><span class="sxs-lookup"><span data-stu-id="636ac-154">Link a schedule to the runbook</span></span>

<span data-ttu-id="636ac-155">您必須建立新的排程。</span><span class="sxs-lookup"><span data-stu-id="636ac-155">A new schedule must be created.</span></span> <span data-ttu-id="636ac-156">按一下 [將排程連結至您的 runbook]。</span><span class="sxs-lookup"><span data-stu-id="636ac-156">Click **Link a schedule to your runbook**.</span></span>

![步驟 7][7]

### <a name="step-1"></a><span data-ttu-id="636ac-158">步驟 1</span><span class="sxs-lookup"><span data-stu-id="636ac-158">Step 1</span></span>

<span data-ttu-id="636ac-159">在 [排程] 刀鋒視窗中，按一下 [建立新的排程]</span><span class="sxs-lookup"><span data-stu-id="636ac-159">On the **Schedule** blade, click **Create a new schedule**</span></span>

![步驟 8][8]

### <a name="step-2"></a><span data-ttu-id="636ac-161">步驟 2</span><span class="sxs-lookup"><span data-stu-id="636ac-161">Step 2</span></span>

<span data-ttu-id="636ac-162">在 [新增排程] 刀鋒視窗中填寫排程資訊。</span><span class="sxs-lookup"><span data-stu-id="636ac-162">On the **New Schedule** blade fill out the schedule information.</span></span> <span data-ttu-id="636ac-163">下列清單中，是可以設定的值︰</span><span class="sxs-lookup"><span data-stu-id="636ac-163">The values that can be set are in the following list:</span></span>

- <span data-ttu-id="636ac-164">**名稱** - 排程的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="636ac-164">**Name** - The friendly name of the schedule.</span></span>
- <span data-ttu-id="636ac-165">**說明** - 排程的說明。</span><span class="sxs-lookup"><span data-stu-id="636ac-165">**Description** - A description of the schedule.</span></span>
- <span data-ttu-id="636ac-166">**啟動** - 這個值是組成排程所觸發之時間的日期、時間和時區的組合。</span><span class="sxs-lookup"><span data-stu-id="636ac-166">**Starts** - This value is a combination of date, time, and time zone that make up the time the schedule triggers.</span></span>
- <span data-ttu-id="636ac-167">**循環** - 這個值會決定排程重複。</span><span class="sxs-lookup"><span data-stu-id="636ac-167">**Recurrence** - This value determines the schedules repetition.</span></span>  <span data-ttu-id="636ac-168">有效值為 [一次] 或 [重複]。</span><span class="sxs-lookup"><span data-stu-id="636ac-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="636ac-169">**重複頻率** - 小時、天、週或月的排程循環間隔。</span><span class="sxs-lookup"><span data-stu-id="636ac-169">**Recur every** - The recurrence interval of the schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="636ac-170">**設定到期日** - 值會決定排程是否應過期。</span><span class="sxs-lookup"><span data-stu-id="636ac-170">**Set Expiration** - The value determines if the schedule should expire or not.</span></span> <span data-ttu-id="636ac-171">可以設定為 [是] 或 [否]。</span><span class="sxs-lookup"><span data-stu-id="636ac-171">Can be set to **Yes** or **No**.</span></span> <span data-ttu-id="636ac-172">如果選擇 [是]，則會提供有效的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="636ac-172">A valid date and time are to be provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="636ac-173">如果您需要一個 runbook 的執行頻率超過一小時，必須在不同的時間間隔建立多個排程 (也就是在每小時後 15、 30、45 分鐘)</span><span class="sxs-lookup"><span data-stu-id="636ac-173">If you need to have a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after the hour)</span></span>

![步驟 9][9]

### <a name="step-3"></a><span data-ttu-id="636ac-175">步驟 3</span><span class="sxs-lookup"><span data-stu-id="636ac-175">Step 3</span></span>

<span data-ttu-id="636ac-176">按一下 [儲存] 以將排程儲存至 runbook。</span><span class="sxs-lookup"><span data-stu-id="636ac-176">Click Save to save the schedule to the runbook.</span></span>

![步驟 10][10]

## <a name="next-steps"></a><span data-ttu-id="636ac-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="636ac-178">Next steps</span></span>

<span data-ttu-id="636ac-179">現在您已了解如何將網路監看員疑難排解與 Azure 自動化整合，請造訪[使用 Azure 網路監看員建立觸發封包擷取的警示](network-watcher-alert-triggered-packet-capture.md)，了解如何在 VM 警示上觸發封包擷取。</span><span class="sxs-lookup"><span data-stu-id="636ac-179">Now that you have an understanding on how to integrate Network Watcher troubleshooting with Azure Automation, learn how to trigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
