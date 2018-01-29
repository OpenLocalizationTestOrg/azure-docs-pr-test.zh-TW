---
title: "使用 Webhook 啟動 Azure 自動化 Runbook | Microsoft Docs"
description: "可讓用戶端透過 HTTP 呼叫在 Azure 自動化中啟動 Runbook 的 Webhook。  本文說明如何建立 Webhook，以及如何進行呼叫以啟動 Runbook。"
services: automation
documentationcenter: 
author: georgewallace
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 03d1617eb64c48b6a90925ae76e1ab3ce0312ff1
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2018
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>使用 Webhook 啟動 Azure 自動化 Runbook
*Webhook* 可讓您在 Azure 自動化中透過單一 HTTP 要求啟動特定的 Runbook。 這可讓外部服務，例如 Visual Studio Team Services、GitHub、Microsoft Operations Management Suite Log Analytics 或自訂應用程式，不需使用 Azure 自動化 API 實作完整的解決方案，即可啟動 Runbook。  
![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)

您可以透過 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Webhook 的詳細資料
下表描述您必須為 Webhook 設定的屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 名稱 |您可以為 Webhook 提供任何想要的名稱，因為這並不會向用戶端公開。  該名稱僅供您用來識別 Azure 自動化中的 Runbook。 <br>  最佳做法是您給予 Webhook 的名稱應該與會使用其的用戶端相關。 |
| URL |Webhook 的 URL 是一種唯一性的位址，即用戶端用來呼叫 HTTP POST 以啟動連結至 Webhook的 Runbook。  當您建立 Webhook 時其會自動產生。  您無法指定自訂 URL。 <br> <br>  URL 包含可讓協力廠商系統不需進一步驗證即可叫用 Runbook 的安全性權杖。 基於這個原因，應該將其視為一種密碼。  基於安全性原因，您僅能於 Webhook 建立時在 Azure 入口網站中檢視 URL。 您應該在安全的位置記下 URL 以供日後使用。 |
| 到期日期 |例如憑證，每個 Webhook 都會有一個到期日期，到期後便無法再使用。  此到期日期可在 Webhook 建立後加以修改。 |
| 已啟用 |建立 Runbook 時 Webhook 會預設為啟用。  如果您將其設定為 [停用]，則任何用戶端皆無法使用。  當您建立 Webhook 時或在建立後的任何時候，您可以設定 [ **啟用** ] 屬性。 |

### <a name="parameters"></a>參數
Webhook 可以定義由該 Webhook 啟動 Runbook 時所使用的 Runbook 參數值。 Webhook 必須包含任何 Runbook 的強制參數值，且可能包含選擇性的參數值。 設定 webhook 參數值可以修改甚至之後建立 webhook。 多個 Webhook 連結至單一 Runbook 時，可以個別使用不同的參數值。

當用戶端使用 Webhook 啟動 Runbook 時，其無法覆寫 Webhook 中定義的參數值。  若要從用戶端接收資料，Runbook 可以接受單一參數，稱之為 **$WebhookData** 的 [物件] 類型，其中包含用戶端在 POST 要求中所包含的資料。

![Webhookdata 屬性](media/automation-webhooks/webhook-data-properties.png)

**$WebhookData** 物件具有下列屬性：

| 屬性 | 說明 |
|:--- |:--- |
| WebhookName |Webhook 的名稱。 |
| RequestHeader |雜湊表包含傳入 POST 要求的標頭。 |
| RequestBody |傳入 POST 要求的本文。  這會保留任何的格式，如字串、JSON、XML，或表單已編碼的資料。 Runbook 必須撰寫用來搭配預期的資料格式。 |

支援 **$WebhookData** 參數不需要 Webhook 的組態，且 Runbook 不需要接受其。  若 Runbook 並未定義參數，則會忽略從用戶端所傳送要求的任何詳細資料。

如果您指定的值 $WebhookData 建立 webhook 時，值將會覆寫時 webhook 啟動 runbook 的資料從用戶端的 POST 要求，即使在要求主體中用戶端不包含任何資料。  若您使用 Webhook 以外的方式啟動具有 $WebhookData 的 Runbook，您可以提供可讓 Runbook 識別的 $WebhookData 值。  這個值應該是 [屬性](#details-of-a-webhook) 相同皆為 $Webhookdata 的物件，Runbook 如此即可正確地與其一起運作，就像是其使用 webhook 所傳遞的實際 WebhookData 一般。

例如，如果要從 Azure 入口網站啟動下列 Runbook，並想要傳遞一些 WebhookData 範例進行測試，因為 WebhookData 為物件，所以應以 UI 中的 JSON 加以傳遞。

![來自 UI 的 WebhookData 參數](media/automation-webhooks/WebhookData-parameter-from-UI.png)

針對上述 Runbook，如果您對 WebhookData 參數具有下列屬性：

1. WebhookName: *MyWebhook*
2. RequestHeader: *From=Test User*
3. RequestBody: *[“VM1”, “VM2”]*

則應對 WebhookData 參數傳遞下列 UI 中的 JSON 值：  

* {"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}

![啟動來自 UI 的 WebhookData 參數](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> 所有輸入參數的值會使用 Runbook 工作進行記錄。  這表示，任何由用戶端在 Webhook 要求中提供的輸入將會進行記錄，並可讓任何有自動化工作存取權的人使用。  基於這個原因，您在 Webhook 呼叫中包含機密資訊時應該特別謹慎。
>

## <a name="security"></a>安全性
Webhook 的安全性仰賴其 URL 的隱私權，其中包含可允許其接受叫用的安全性權杖。 只要針對正確的 URL 進行要求，Azure 自動化就不會對要求執行任何驗證。 基於這個原因，若不使用驗證要求的替代方式時，Webhooks 不應用於執行高度機密功能的 Runbook。

您可以透過檢查 $WebhookData 參數的 **WebhookName** 屬性，在 Runbook 中包含邏輯來判斷其是否由 Webhook 所呼叫。 Runbook 可以透過尋找 **RequestHeader** 或 **RequestBody** 屬性中的特定資訊來執行進一步的驗證。

另一個策略是當 Runbook 收到 Webhook 要求時，使其執行某些外部條件的驗證。  例如，當 GitHub 儲存機制出現新的認可時，考慮使用由 GitHub 呼叫的 Runbook。  Runbook 可能會連接到 GitHub 以驗證在繼續之前實際上已出現新的認可。

## <a name="creating-a-webhook"></a>建立 Webhook
使用下列程序在 Azure 入口網站中建立連結至 Runbook 的全新 Webhook。

1. 從**Runbook 頁面**在 Azure 入口網站中，按一下 runbook webhook 啟動，檢視其詳細資料頁面。
2. 按一下**Webhook**頂端的頁面，即可開啟**新增 Webhook**頁面。 <br>
   ![Webhook 按鈕](media/automation-webhooks/webhooks-button.png)
3. 按一下**建立新的 webhook**開啟**建立 webhook 頁面**。
4. 指定 Webhook 的 [名稱]、[到期日期] 以及是否應該啟用。 請參閱 [Webhook 的詳細資料](#details-of-a-webhook) 以取得這些屬性的詳細資訊。
5. 按一下複製圖示，然後按 Ctrl + C 以複製 Webhook 的 URL。  然後將其記錄在安全的地方。  **一旦您建立 Webhook，即無法再次擷取 URL。** <br>
   ![Webhook URL](media/automation-webhooks/copy-webhook-url.png)
6. 按一下 [參數]  來提供 Runbook 的參數值。  如果 Runbook 有強制參數，除非提供該值，否則您將無法建立 Webhook。
7. 按一下 [ **建立** ] 來建立 Webhook。

## <a name="using-a-webhook"></a>使用 Webhook
建立 Webhook 之後若要使用它，您的用戶端應用程式必須使用 Webhook 的 URL 來發出 HTTP POST。  Webhook 的語法將遵循以下列格式。

    http://<Webhook Server>/token?=<Token Value>

用戶端將會從 POST 要求中接收下列其中一個傳回代碼。  

| 代碼 | 文字 | 說明 |
|:--- |:--- |:--- |
| 202 |已接受 |已接受要求，且 Runbook 已經成功排入佇列。 |
| 400 |不正確的要求 |基於下列原因之一不接受此要求。 <ul> <li>Webhook 已過期。</li> <li>Webhook 已停用。</li> <li>URL 中的權杖無效。</li>  </ul> |
| 404 |找不到 |基於下列原因之一不接受此要求。 <ul> <li>找不到該 Webhook。</li> <li>找不到該 Runbook。</li> <li>找不到帳戶。</li>  </ul> |
| 500 |內部伺服器錯誤 |URL 有效，但發生錯誤。  請重新提交要求。 |

假設要求成功，Webhook 會回應包含 JSON 格式的工作識別碼，如下所示。 它會包含單一的工作識別碼，但是 JSON 格式允許未來可能的增強功能。

    {"JobIds":["<JobId>"]}  

用戶端無法從 Webhook 判斷 Runbook 的工作何時完成或完成狀態。  這項資訊可使用工作識別碼搭配其他方法 (例如 [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) 或 [Azure 自動化 API](https://msdn.microsoft.com/library/azure/mt163826.aspx)) 來判斷。

### <a name="example"></a>範例
下列範例使用 Windows PowerShell 搭配 Webhook 來啟動 Runbook。  請注意，任何可以進行 HTTP 要求的語言都可以使用 Webhook；Windows PowerShell 在這裡僅作為範例使用。

Runbook 預期在要求的主體中有 JSON 格式的虛擬機器清單。 我們也在要求的標頭中，列入了有關於啟動 Runbook 的人員、啟動的日期和時間資訊。      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


下圖顯示來自要求的標頭資訊 (使用 [Fiddler](http://www.telerik.com/fiddler) 追蹤)。 這包括了 HTTP 要求的標準標頭，除此之外，還有我們加入的自訂「日期」和「時間」標頭。  這些值都可在 **WebhookData** 的**RequestHeaders** 屬性中提供給 Runbook 使用。

![Webhook 按鈕](media/automation-webhooks/webhook-request-headers.png)

下圖顯示要求的主體 (使用 [Fiddler](http://www.telerik.com/fiddler) 追蹤) 可在 **WebhookData** 的 **RequestBody** 屬性中提供給 Runbook 使用。 格式化為 JSON 是因為其格式是要求的主體中所包含之格式。     

![Webhook 按鈕](media/automation-webhooks/webhook-request-body.png)

下圖顯示由 Windows PowerShell 送出的要求以及產生的回應。  工作識別碼從回應中擷取，再轉換為字串。

![Webhook 按鈕](media/automation-webhooks/webhook-request-response.png)

下列範例 Runbook 接受之前的範例要求，並啟動要求主體中指定的虛擬機器。

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate to Azure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a>啟動 Runbook 以回應 Azure 警示
啟用 Webhook 的 Runbook 可用以回應 [Azure 警示](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。 Azure 中的資源可以透過 Azure 警示的協助，藉由收集如效能、可用性和使用方式的統計資料進行監視。 您可以收到根據監視您 Azure 資源的計量或事件的警示，目前自動化帳戶僅支援度量。 當指定的計量值超過指派的閾值，或者如果觸發了設定的事件，就會傳送通知給服務管理員或共同管理員以解決該警示，如需計量與事件的詳細資訊，請參閱 [Azure 警示](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。

除了使用 Azure 的警示做為通知系統，也可以使用 Runbook 回應警示。 Azure 自動化可讓您使用 Azure 警示執行啟用 Webhook 的 Runbook。 當計量超過設定的閾值時，警示規則就會變成作用中，並且觸發自動化 Webhook，連帶執行 Runbook。

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>警示內容
考量如虛擬機器的 Azure 資源，這台電腦的 CPU 使用率是其中一個關鍵效能計量。 如果 CPU 使用率是 100% 或者在一段長時間超過某個量，您可能會想要重新啟動虛擬機器以修正問題。 這可以藉由設定虛擬機器的警示規則來解決，而此規則可以使用 CPU 百分比做為計量。 這裡的 CPU 百分比只是一個範例，但是還有許多您可以對 Azure 資源設定的其他計量，重新啟動虛擬機器是修正此問題所採取的一個動作，您可以設定 Runbook 採取其他動作。

當此警示規則變成作用中並且觸發啟用 Webhook 的 Runbook 時，會傳送警示內容到 Runbook。 [警示內容](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)包含的詳細資料包括 **SubscriptionID**、**ResourceGroupName**、**ResourceName**、**ResourceType**、**ResourceId** 和 **Timestamp**，這些都是 Runbook 識別要在其上採取動作的資源所需的項目。 警示內容內嵌在傳送至 Runbook 的 **WebhookData** 物件的內文部分，可以使用 **Webhook.RequestBody** 屬性存取

### <a name="example"></a>範例
在訂用帳戶中建立 Azure 虛擬機器，並關聯[警示以監視 CPU 百分比計量](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。 建立警示時，請確定以建立 Webhook 時所產生的 Webhook URL 填入 Webhook 欄位。

下列範例 Runbook 會在警示規則變成作用中時觸發，而且會收集 Runbook 識別在上面採取動作的資源所需的警示內容參數。

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>後續步驟
* 如需以不同方式啟動 Runbook 的詳細資訊，請參閱[啟動 Runbook](automation-starting-a-runbook.md)。
* 如需檢視 Runbook 作業狀態的相關資訊，請參閱 [Azure 自動化中的 Runbook 執行](automation-runbook-execution.md)。
* 若要了解如何使用 Azure 自動化來對 Azure 警示採取動作，請參閱[使用自動化 Runbook 修復 Azure VM 警示](automation-azure-vm-alert-integration.md)。
