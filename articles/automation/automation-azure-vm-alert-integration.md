---
title: " 使用自動化 Runbook 補救 Azure VM 警示 | Microsoft Docs"
description: "本文示範如何使用 Azure 自動化 Runbook 整合 Azure 虛擬機器警示，並自動補救問題"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: 738959b8e1ee5da989bb996d1ce8148cbf912781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="60433-103">Azure 自動化案例 - 補救 Azure VM 警示</span><span class="sxs-lookup"><span data-stu-id="60433-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="60433-104">Azure 自動化和 Azure 虛擬機器發行了一項新功能，可讓您設定虛擬機器 (VM) 警示以便執行自動化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="60433-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span></span> <span data-ttu-id="60433-105">這項新功能可讓您自動執行標準補救以回應 VM 警示，例如重新啟動或停止 VM。</span><span class="sxs-lookup"><span data-stu-id="60433-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span></span>

<span data-ttu-id="60433-106">先前，在建立 VM 警示規則期間，您能夠 [指定自動化 Webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) 給 Runbook，以便在觸發警示時執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="60433-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span></span> <span data-ttu-id="60433-107">不過，您需要進行建立 Runbook 的工作，為 Runbook 建立 Webhook，然後在警示規則建立期間複製並貼上 Webhook。</span><span class="sxs-lookup"><span data-stu-id="60433-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span></span> <span data-ttu-id="60433-108">使用這個新版本，此程序會更加容易，因為您可以在警示規則建立期間直接從清單中選擇 Runbook，而且可以選擇將執行 Runbook 或輕鬆建立帳戶的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="60433-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span></span>

<span data-ttu-id="60433-109">在本文中，我們將說明設定 Azure VM 警示以及設定在警示觸發時所要執行的自動化 Runbook 有多麼容易。</span><span class="sxs-lookup"><span data-stu-id="60433-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span></span> <span data-ttu-id="60433-110">範例案例包括：當記憶體使用量由於 VM 上的應用程式有記憶體流失而超過某個臨界值時重新啟動 VM，或是當 CPU 使用者時間在過去一小時已低於 1% 且不在使用中時停止 VM。</span><span class="sxs-lookup"><span data-stu-id="60433-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="60433-111">我們也將說明在您的自動化帳戶中自動建立服務主體，如何簡化在 Azure 警示補救中使用 Runbook。</span><span class="sxs-lookup"><span data-stu-id="60433-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="60433-112">在 VM 上建立警示</span><span class="sxs-lookup"><span data-stu-id="60433-112">Create an alert on a VM</span></span>
<span data-ttu-id="60433-113">執行下列步驟來設定警示，以在符合其臨界值時啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="60433-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="60433-114">在此版本中，我們只支援 V2 虛擬機器，即將新增傳統 VM 的支援。</span><span class="sxs-lookup"><span data-stu-id="60433-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="60433-115">登入 Azure 入口網站，然後按一下 [虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="60433-115">Log in to the Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="60433-116">選取其中一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="60433-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="60433-117">將會出現虛擬機器儀表板刀鋒視窗，而 [設定]  刀鋒視窗會出現在其右邊。</span><span class="sxs-lookup"><span data-stu-id="60433-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span></span>  
3. <span data-ttu-id="60433-118">在 [設定] 刀鋒視窗的 [監視] 區段之下，選取 [警示規則]。</span><span class="sxs-lookup"><span data-stu-id="60433-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="60433-119">在 [警示規則] 刀鋒視窗上，按一下 [加入警示]。</span><span class="sxs-lookup"><span data-stu-id="60433-119">On the **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="60433-120">這會開啟 [加入警示規則]  刀鋒視窗，您可以在此設定警示的條件，並選擇下列其中一個或所有選項︰傳送電子郵件給某人、使用 Webhook 將警示轉寄至另一個系統，及/或執行自動化 Runbook 以回應修補問題的嘗試。</span><span class="sxs-lookup"><span data-stu-id="60433-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="60433-121">設定 Runbook</span><span class="sxs-lookup"><span data-stu-id="60433-121">Configure a runbook</span></span>
<span data-ttu-id="60433-122">若要設定 Runbook 以在符合 VM 警示臨界值時執行，請選取 [自動化 Runbook] 。</span><span class="sxs-lookup"><span data-stu-id="60433-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="60433-123">在 [設定 Runbook]  刀鋒視窗中，您可以選取要執行的 Runbook 以及用來執行 Runbook 的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="60433-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span></span>

![設定自動化 Runbook 並建立新的自動化帳戶](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="60433-125">在此版本中，您可以從服務所提供的三個 Runbook 進行選擇 – 重新啟動 VM、停止 VM 或移除 VM (刪除它)。</span><span class="sxs-lookup"><span data-stu-id="60433-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="60433-126">在未來版本中將提供選取其他 Runbook 或您自己的其中一個 Runbook 的功能。</span><span class="sxs-lookup"><span data-stu-id="60433-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![可從中選擇的 Runbook](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="60433-128">在您選取其中一個可用的 Runbook 之後，[自動化帳戶]  下拉式清單隨即出現，以便您選取用來執行 Runbook 的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="60433-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span></span> <span data-ttu-id="60433-129">Runbook 必須在您的 Azure 訂用帳戶中的 [自動化帳戶](automation-security-overview.md) 內容中執行。</span><span class="sxs-lookup"><span data-stu-id="60433-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="60433-130">您可以選取已經建立的自動化帳戶，也可以為自己建立新的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="60433-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="60433-131">所提供的 Runbook 會使用服務主體進行Azure 驗證。</span><span class="sxs-lookup"><span data-stu-id="60433-131">The runbooks that are provided authenticate to Azure using a service principal.</span></span> <span data-ttu-id="60433-132">如果您選擇在其中一個現有的自動化帳戶中執行 Runbook，我們將會自動為您建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="60433-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span></span> <span data-ttu-id="60433-133">如果您選擇建立新的自動化帳戶，則我們會自動建立帳戶和服務主體。</span><span class="sxs-lookup"><span data-stu-id="60433-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span></span> <span data-ttu-id="60433-134">在這兩種情況下，也會在自動化帳戶中建立兩項資產 – 名為 **AzureRunAsCertificate** 的憑證資產和名為 **AzureRunAsConnection** 的連接資產。</span><span class="sxs-lookup"><span data-stu-id="60433-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="60433-135">Runbook 將使用 **AzureRunAsConnection** 進行 Azure 驗證，以便對 VM 執行管理動作。</span><span class="sxs-lookup"><span data-stu-id="60433-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="60433-136">服務主體會建立於訂用帳戶範圍並獲得參與者角色。</span><span class="sxs-lookup"><span data-stu-id="60433-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span></span> <span data-ttu-id="60433-137">需要此角色，有權執行自動化 Runbook 的帳戶才能管理 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="60433-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span></span>  <span data-ttu-id="60433-138">建立自動化帳戶及/或服務主體是一次性事件。</span><span class="sxs-lookup"><span data-stu-id="60433-138">The creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="60433-139">一旦建立，您可以使用該帳戶來對其他 Azure VM 警示執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="60433-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="60433-140">當您按一下 [確定]  時，便會設定警示，如果您選取要建立新的自動化帳戶的選項，則會隨著服務主體一起建立。</span><span class="sxs-lookup"><span data-stu-id="60433-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span></span>  <span data-ttu-id="60433-141">這可能需要幾秒鐘才會完成。</span><span class="sxs-lookup"><span data-stu-id="60433-141">This can take a few seconds to complete.</span></span>  

![正在設定的 Runbook](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="60433-143">完成設定之後，您會看到 Runbook 名稱出現在 [加入警示規則]  刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="60433-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span></span>

![已設定的 Runbook](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="60433-145">按一下 [加入警示規則]  in the  ，如果虛擬機器處於執行中狀態，則會建立並啟動警示規則。</span><span class="sxs-lookup"><span data-stu-id="60433-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="60433-146">啟用或停用 Runbook</span><span class="sxs-lookup"><span data-stu-id="60433-146">Enable or disable a runbook</span></span>
<span data-ttu-id="60433-147">如果您有針對警示設定的 Runbook，您可以將它停用，而不需移除 Runbook 組態。</span><span class="sxs-lookup"><span data-stu-id="60433-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span></span> <span data-ttu-id="60433-148">這可讓警示保持執行中，而且您或許可測試某些警示規則，稍後重新啟用 Runbook。</span><span class="sxs-lookup"><span data-stu-id="60433-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="60433-149">建立與 Azure 警示搭配運作的 Runbook</span><span class="sxs-lookup"><span data-stu-id="60433-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="60433-150">當您選擇 Runbook 做為 Azure 警示規則的一部分時，Runbook 內必須有負責管理所收到之警示資料的邏輯。</span><span class="sxs-lookup"><span data-stu-id="60433-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span></span>  <span data-ttu-id="60433-151">在警示規則中設定 Runbook 時，便會為 Runbook 建立 Webhook；該 Webhook 接著會在每次觸發警示時用來啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="60433-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span></span>  <span data-ttu-id="60433-152">實際用來啟動 Runbook 的呼叫是 Webhook URL 的 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="60433-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span></span> <span data-ttu-id="60433-153">POST 要求的本文包含 JSON 格式的物件，此物件中包含與警示相關的實用屬性。</span><span class="sxs-lookup"><span data-stu-id="60433-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span></span>  <span data-ttu-id="60433-154">如下面所見，警示資料包含 subscriptionID、resourceGroupName、resourceName 和 resourceType 等詳細資料。</span><span class="sxs-lookup"><span data-stu-id="60433-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="60433-155">警示資料的範例</span><span class="sxs-lookup"><span data-stu-id="60433-155">Example of Alert data</span></span>
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

<span data-ttu-id="60433-156">當自動化 Webhook 服務收到 HTTP POST 時，它會擷取警示資料，並將它傳遞給 WebhookData Runbook 輸入參數中的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="60433-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span></span>  <span data-ttu-id="60433-157">以下範例 Runbook 會示範如何使用 WebhookData 參數，以及擷取警示資料並用它來管理觸發警示的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="60433-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="60433-158">範例 Runbook</span><span class="sxs-lookup"><span data-stu-id="60433-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response to an Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get the data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that the alert status is 'Activated' (alert condition went from false to true)
    # and not 'Resolved' (alert condition went from true to false)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get the info needed to identify the VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is the expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate to Azure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart the VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # The alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant to be started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="60433-159">摘要</span><span class="sxs-lookup"><span data-stu-id="60433-159">Summary</span></span>
<span data-ttu-id="60433-160">當您在 Azure VM 上設定警示時，您現在能夠輕鬆地設定自動化 Runbook，以在警示觸發時自動執行補救動作。</span><span class="sxs-lookup"><span data-stu-id="60433-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span></span> <span data-ttu-id="60433-161">在此版本中，您可以根據您的警示情況，從 Runbook 中選擇重新啟動、停止或刪除 VM。</span><span class="sxs-lookup"><span data-stu-id="60433-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="60433-162">這只是讓您用來控制警示觸發時會自動採取的動作 (通知、疑難排解、補救) 的案例開頭。</span><span class="sxs-lookup"><span data-stu-id="60433-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60433-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60433-163">Next Steps</span></span>
* <span data-ttu-id="60433-164">若要開始使用圖形化 Runbook，請參閱 [我的第一個圖形化 Runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="60433-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="60433-165">若要開始使用 PowerShell 工作流程 Runbook，請參閱 [我的第一個 PowerShell 工作流程 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="60433-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="60433-166">若要深入了解 Runbook 類型、其優點和限制，請參閱 [Azure 自動化 Runbook 類型](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="60433-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

