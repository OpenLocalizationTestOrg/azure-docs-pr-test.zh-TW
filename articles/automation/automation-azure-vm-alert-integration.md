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
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a>Azure 自動化案例 - 補救 Azure VM 警示
Azure 自動化和 Azure 虛擬機器已發行的新功能，可讓您 tooconfigure 虛擬機器 (VM) 警示 toorun 自動化 runbook。 這項新功能可讓您 tooautomatically 回應 tooVM 警示，例如重新啟動或停止 hello VM 中執行標準的修復。

先前，在警示規則建立 VM 時您仍可太[指定自動化 webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa hello 警示觸發時順序 toorun hello runbook 中的 runbook。 不過，這需要您建立 hello runbook、 建立 hello webhook hello runbook，然後複製和貼上 hello webhook 警示規則建立期間 toodo hello 工作。 使用這個新的版本，因為您可以直接 runbook 從清單中選擇的警示規則建立期間，您可以選擇將執行 hello runbook 或輕鬆地建立帳戶的自動化帳戶，會比較容易 hello 程序。

在本文中，即將顯示是多麼的輕鬆 tooset 向上 Azure VM 警示及設定自動化 runbook toorun 每當 hello 警示觸發程序。 範例案例包括 hello 記憶體使用量超過 tooan 應用程式上 hello VM 有記憶體流失，因為某些閾值時，請重新啟動 VM，或停止 VM，hello CPU 使用者時間已低於 1%過去一小時，而且沒有使用中時。 我們也將說明如何 hello 自動建立服務主體，在您的自動化帳戶可簡化 hello Azure 警示補救中的 runbook 使用。

## <a name="create-an-alert-on-a-vm"></a>在 VM 上建立警示
執行下列步驟 tooconfigure 警示 toolaunch runbook，在達到臨界值時的 hello。

> [!NOTE]
> 在此版本中，我們只支援 V2 虛擬機器，即將新增傳統 VM 的支援。  
> 
> 

1. 登入 toohello Azure 入口網站，然後按一下**虛擬機器**。  
2. 選取其中一部虛擬機器。  hello 虛擬機器儀表板刀鋒視窗會顯示與 hello**設定**刀鋒視窗 tooits 權限。  
3. 從 hello**設定**刀鋒視窗中的，在 hello 監視 區段選取**警示規則**。
4. 在 hello**警示規則**刀鋒視窗中，按一下 **新增警示**。

這會開啟 hello**加入警示規則**刀鋒視窗中，您可以在此設定 hello hello 警示的條件，並選擇其中一個或所有這些選項： 傳送電子郵件 toosomeone，請使用 webhook tooforward hello 警示 tooanother 系統，和 （或)自動化 runbook 執行回應嘗試 tooremediate hello 問題。

## <a name="configure-a-runbook"></a>設定 Runbook
選取當符合 hello VM 警示臨界值時，runbook toorun tooconfigure**自動化 Runbook**。 在 hello**設定 runbook**刀鋒視窗中，您可以選取 hello runbook toorun 和 hello 自動化帳戶 toorun hello runbook 中的。

![設定自動化 Runbook 並建立新的自動化帳戶](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> 此版本中，您可以選擇三個 runbook 的 hello 服務所提供 – 重新啟動 VM、 停止 VM 或移除的 VM （刪除）。  hello 能力 tooselect 其他 runbook，或您自己的 runbook 的其中一個將可在未來的版本。
> 
> 

![從 Runbook toochoose](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

您選取其中一個 hello 三個可用之 runbook 之後，hello**自動化帳戶**下拉式清單隨即出現，而且您可以選取自動化帳戶 hello runbook 將會當做執行。 Runbook 需要 hello 內容中的 toorun[自動化帳戶](automation-security-overview.md)位於您的 Azure 訂用帳戶。 您可以選取已經建立的自動化帳戶，也可以為自己建立新的自動化帳戶。

所提供的 hello runbook 驗證 tooAzure 使用服務主體。 如果您選擇 toorun hello runbook 中的其中一個現有的自動化帳戶時，我們會自動建立 hello 服務主體為您。 如果您選擇 toocreate 新的自動化帳戶，然後我們會自動建立 hello 帳戶和 hello 服務主體。 在這兩種情況下，兩個資產也會建立在 hello 自動化帳戶 – 名為憑證資產**AzureRunAsCertificate**和名為連線資產**AzureRunAsConnection**。 hello 的 runbook 會使用**AzureRunAsConnection** tooauthenticate 與 Azure 中針對 hello VM order tooperform hello 管理動作。

> [!NOTE]
> hello 服務主體建立 hello 訂用帳戶範圍中，且 hello 參與者角色指派。 為了讓 hello 帳戶 toohave 權限 toorun 自動化 runbook toomanage Azure Vm 需要此角色。  hello 建立自動化帳戶及/或服務主體是一次性的活動。 一旦建立，您可以使用 toorun runbook 的帳戶的其他 Azure VM 的警示。
> 
> 

當您按一下**確定**hello 警示設定，如果您選取 hello 選項 toocreate 新的自動化帳戶時，就會建立以及 hello 服務主體。  這可能需要幾秒鐘的時間 toocomplete。  

![正在設定的 Runbook](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

Hello 組態完成後即會出現在 hello hello runbook hello 名稱**加入警示規則**刀鋒視窗。

![已設定的 Runbook](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

按一下**確定**在 hello**加入警示規則**刀鋒視窗，然後 hello 警示的規則將會建立並啟用如果 hello 虛擬機器處於執行中狀態。

### <a name="enable-or-disable-a-runbook"></a>啟用或停用 Runbook
如果您有設定警示的 runbook，您可以不會移除 hello runbook 設定停用它。 這可讓您執行 tookeep hello 警示可能是測試一些 hello 警示規則，並之後再重新啟用 hello runbook。

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a>建立與 Azure 警示搭配運作的 Runbook
當您選擇 runbook 做為 Azure 的警示規則的一部分時，hello runbook 必須 toohave 邏輯 toomanage hello 警示傳遞的資料 tooit。  Hello runbook; 警示規則中設定 runbook 時，建立 webhook使用的 toostart hello runbook 每個時間 hello 警示觸發程序，則該 webhook。  hello 實際呼叫 toostart hello runbook 是 HTTP POST 要求 toohello webhook URL。 hello hello POST 要求主體包含 JSON 格式的物件，其中包含有用的屬性相關的 toohello 警示。  您可以看到下面，hello 警示資料就會包含訂用帳戶 Id、 資源群組名稱、 resourceName 和 resourceType 等詳細資料。

### <a name="example-of-alert-data"></a>警示資料的範例
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

Hello 自動化 webhook 服務收到 hello HTTP POST 時它會擷取 hello 警示的資料，並將其 hello WebhookData runbook 輸入參數中傳遞 toohello runbook。  以下是範例 runbook 會顯示 toouse hello WebhookData 參數，將擷取 hello 警示資料並使用它 toomanage hello 觸發 hello 警示的 Azure 資源的方式。

### <a name="example-runbook"></a>範例 Runbook
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

## <a name="summary"></a>摘要
當您在 Azure VM 上設定警示時，您現在可以有 hello 能力 tooeasily 設定自動化 runbook tooautomatically hello 警示觸發時，執行修復動作。 此版本中，您可以選擇從 runbook toorestart 停止或刪除 VM，以根據警示的案例。 這是讓您用來控制警示觸發時自動執行的 hello 動作 （通知，進行疑難排解，補救） 的案例只 hello 開頭。

## <a name="next-steps"></a>後續步驟
* tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md)
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)
* toolearn 深入了解 runbook 類型、 其優點和限制，請參閱[Azure 自動化 runbook 類型](automation-runbook-types.md)

