---
title: "aaa\"補救自動化 runbook 的 Azure VM 警示 |Microsoft 文件 」"
description: "本文示範如何使用 Azure 自動化 runbook 警示 toointegrate Azure 虛擬機器的方式並自動補救問題"
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
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="7f3ba-103">Azure 自動化案例 - 補救 Azure VM 警示</span><span class="sxs-lookup"><span data-stu-id="7f3ba-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="7f3ba-104">Azure 自動化和 Azure 虛擬機器已發行的新功能，可讓您 tooconfigure 虛擬機器 (VM) 警示 toorun 自動化 runbook。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="7f3ba-105">這項新功能可讓您 tooautomatically 回應 tooVM 警示，例如重新啟動或停止 hello VM 中執行標準的修復。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="7f3ba-106">先前，在警示規則建立 VM 時您仍可太[指定自動化 webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa hello 警示觸發時順序 toorun hello runbook 中的 runbook。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="7f3ba-107">不過，這需要您建立 hello runbook、 建立 hello webhook hello runbook，然後複製和貼上 hello webhook 警示規則建立期間 toodo hello 工作。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="7f3ba-108">使用這個新的版本，因為您可以直接 runbook 從清單中選擇的警示規則建立期間，您可以選擇將執行 hello runbook 或輕鬆地建立帳戶的自動化帳戶，會比較容易 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="7f3ba-109">在本文中，即將顯示是多麼的輕鬆 tooset 向上 Azure VM 警示及設定自動化 runbook toorun 每當 hello 警示觸發程序。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="7f3ba-110">範例案例包括 hello 記憶體使用量超過 tooan 應用程式上 hello VM 有記憶體流失，因為某些閾值時，請重新啟動 VM，或停止 VM，hello CPU 使用者時間已低於 1%過去一小時，而且沒有使用中時。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="7f3ba-111">我們也將說明如何 hello 自動建立服務主體，在您的自動化帳戶可簡化 hello Azure 警示補救中的 runbook 使用。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="7f3ba-112">在 VM 上建立警示</span><span class="sxs-lookup"><span data-stu-id="7f3ba-112">Create an alert on a VM</span></span>
<span data-ttu-id="7f3ba-113">執行下列步驟 tooconfigure 警示 toolaunch runbook，在達到臨界值時的 hello。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="7f3ba-114">在此版本中，我們只支援 V2 虛擬機器，即將新增傳統 VM 的支援。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="7f3ba-115">登入 toohello Azure 入口網站，然後按一下**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="7f3ba-116">選取其中一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="7f3ba-117">hello 虛擬機器儀表板刀鋒視窗會顯示與 hello**設定**刀鋒視窗 tooits 權限。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="7f3ba-118">從 hello**設定**刀鋒視窗中的，在 hello 監視 區段選取**警示規則**。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="7f3ba-119">在 hello**警示規則**刀鋒視窗中，按一下 **新增警示**。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="7f3ba-120">這會開啟 hello**加入警示規則**刀鋒視窗中，您可以在此設定 hello hello 警示的條件，並選擇其中一個或所有這些選項： 傳送電子郵件 toosomeone，請使用 webhook tooforward hello 警示 tooanother 系統，和 （或)自動化 runbook 執行回應嘗試 tooremediate hello 問題。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="7f3ba-121">設定 Runbook</span><span class="sxs-lookup"><span data-stu-id="7f3ba-121">Configure a runbook</span></span>
<span data-ttu-id="7f3ba-122">選取當符合 hello VM 警示臨界值時，runbook toorun tooconfigure**自動化 Runbook**。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="7f3ba-123">在 hello**設定 runbook**刀鋒視窗中，您可以選取 hello runbook toorun 和 hello 自動化帳戶 toorun hello runbook 中的。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![設定自動化 Runbook 並建立新的自動化帳戶](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="7f3ba-125">此版本中，您可以選擇三個 runbook 的 hello 服務所提供 – 重新啟動 VM、 停止 VM 或移除的 VM （刪除）。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="7f3ba-126">hello 能力 tooselect 其他 runbook，或您自己的 runbook 的其中一個將可在未來的版本。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![從 Runbook toochoose](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="7f3ba-128">您選取其中一個 hello 三個可用之 runbook 之後，hello**自動化帳戶**下拉式清單隨即出現，而且您可以選取自動化帳戶 hello runbook 將會當做執行。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="7f3ba-129">Runbook 需要 hello 內容中的 toorun[自動化帳戶](automation-security-overview.md)位於您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="7f3ba-130">您可以選取已經建立的自動化帳戶，也可以為自己建立新的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="7f3ba-131">所提供的 hello runbook 驗證 tooAzure 使用服務主體。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="7f3ba-132">如果您選擇 toorun hello runbook 中的其中一個現有的自動化帳戶時，我們會自動建立 hello 服務主體為您。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="7f3ba-133">如果您選擇 toocreate 新的自動化帳戶，然後我們會自動建立 hello 帳戶和 hello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="7f3ba-134">在這兩種情況下，兩個資產也會建立在 hello 自動化帳戶 – 名為憑證資產**AzureRunAsCertificate**和名為連線資產**AzureRunAsConnection**。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="7f3ba-135">hello 的 runbook 會使用**AzureRunAsConnection** tooauthenticate 與 Azure 中針對 hello VM order tooperform hello 管理動作。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="7f3ba-136">hello 服務主體建立 hello 訂用帳戶範圍中，且 hello 參與者角色指派。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="7f3ba-137">為了讓 hello 帳戶 toohave 權限 toorun 自動化 runbook toomanage Azure Vm 需要此角色。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="7f3ba-138">hello 建立自動化帳戶及/或服務主體是一次性的活動。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="7f3ba-139">一旦建立，您可以使用 toorun runbook 的帳戶的其他 Azure VM 的警示。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="7f3ba-140">當您按一下**確定**hello 警示設定，如果您選取 hello 選項 toocreate 新的自動化帳戶時，就會建立以及 hello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="7f3ba-141">這可能需要幾秒鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-141">This can take a few seconds toocomplete.</span></span>  

![正在設定的 Runbook](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="7f3ba-143">Hello 組態完成後即會出現在 hello hello runbook hello 名稱**加入警示規則**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![已設定的 Runbook](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="7f3ba-145">按一下**確定**在 hello**加入警示規則**刀鋒視窗，然後 hello 警示的規則將會建立並啟用如果 hello 虛擬機器處於執行中狀態。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="7f3ba-146">啟用或停用 Runbook</span><span class="sxs-lookup"><span data-stu-id="7f3ba-146">Enable or disable a runbook</span></span>
<span data-ttu-id="7f3ba-147">如果您有設定警示的 runbook，您可以不會移除 hello runbook 設定停用它。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="7f3ba-148">這可讓您執行 tookeep hello 警示可能是測試一些 hello 警示規則，並之後再重新啟用 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="7f3ba-149">建立與 Azure 警示搭配運作的 Runbook</span><span class="sxs-lookup"><span data-stu-id="7f3ba-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="7f3ba-150">當您選擇 runbook 做為 Azure 的警示規則的一部分時，hello runbook 必須 toohave 邏輯 toomanage hello 警示傳遞的資料 tooit。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="7f3ba-151">Hello runbook; 警示規則中設定 runbook 時，建立 webhook使用的 toostart hello runbook 每個時間 hello 警示觸發程序，則該 webhook。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="7f3ba-152">hello 實際呼叫 toostart hello runbook 是 HTTP POST 要求 toohello webhook URL。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="7f3ba-153">hello hello POST 要求主體包含 JSON 格式的物件，其中包含有用的屬性相關的 toohello 警示。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="7f3ba-154">您可以看到下面，hello 警示資料就會包含訂用帳戶 Id、 資源群組名稱、 resourceName 和 resourceType 等詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="7f3ba-155">警示資料的範例</span><span class="sxs-lookup"><span data-stu-id="7f3ba-155">Example of Alert data</span></span>
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

<span data-ttu-id="7f3ba-156">Hello 自動化 webhook 服務收到 hello HTTP POST 時它會擷取 hello 警示的資料，並將其 hello WebhookData runbook 輸入參數中傳遞 toohello runbook。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="7f3ba-157">以下是範例 runbook 會顯示 toouse hello WebhookData 參數，將擷取 hello 警示資料並使用它 toomanage hello 觸發 hello 警示的 Azure 資源的方式。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="7f3ba-158">範例 Runbook</span><span class="sxs-lookup"><span data-stu-id="7f3ba-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="7f3ba-159">摘要</span><span class="sxs-lookup"><span data-stu-id="7f3ba-159">Summary</span></span>
<span data-ttu-id="7f3ba-160">當您在 Azure VM 上設定警示時，您現在可以有 hello 能力 tooeasily 設定自動化 runbook tooautomatically hello 警示觸發時，執行修復動作。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="7f3ba-161">此版本中，您可以選擇從 runbook toorestart 停止或刪除 VM，以根據警示的案例。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="7f3ba-162">這是讓您用來控制警示觸發時自動執行的 hello 動作 （通知，進行疑難排解，補救） 的案例只 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="7f3ba-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f3ba-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7f3ba-163">Next Steps</span></span>
* <span data-ttu-id="7f3ba-164">tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="7f3ba-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="7f3ba-165">tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="7f3ba-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="7f3ba-166">toolearn 深入了解 runbook 類型、 其優點和限制，請參閱[Azure 自動化 runbook 類型](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="7f3ba-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

