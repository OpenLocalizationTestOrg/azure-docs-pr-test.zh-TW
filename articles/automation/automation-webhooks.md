---
title: "Azure 自動化 runbook 的 webhook aaaStarting |Microsoft 文件"
description: "Webhook，可讓用戶端 toostart runbook 在 Azure 自動化中從 HTTP 呼叫。  本文說明如何 toocreate webhook 以及 toocall 一個 toostart runbook。"
services: automation
documentationcenter: 
author: mgoedtel
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
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>使用 Webhook 啟動 Azure 自動化 Runbook
A *webhook*可讓您 toostart 特定 runbook 在 Azure 自動化中透過單一 HTTP 要求。 這可讓外部服務，例如 Visual Studio Team Services、 GitHub、 Microsoft Operations Management Suite 記錄分析或自訂應用程式 toostart runbook 而不需要實作使用 hello Azure 自動化 API 的完整方案。  
![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)

您可以比較啟動 runbook 的 webhook tooother 方法[Azure 自動化中啟動 runbook](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Webhook 的詳細資料
hello 下表描述您必須設定的 webhook hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 名稱 |您可以提供任何的名稱的 webhook 因為這是不公開 toohello 用戶端。  僅用於您 tooidentify hello Azure 自動化中 runbook。 <br>  最佳做法，您應該給予 hello webhook 名稱相關的 toohello 用戶端將使用它。 |
| URL |hello hello webhook URL 是 hello 唯一的位址，用戶端呼叫使用的 HTTP POST toostart hello runbook 連結 toohello webhook。  它會自動產生的當您建立 hello webhook。  您無法指定自訂 URL。 <br> <br>  hello URL 包含可讓 hello runbook toobe 叫用由沒有進一步的驗證與第三方系統的安全性權杖。 基於這個原因，應該將其視為一種密碼。  基於安全性理由，您可以只檢視 hello 建立 hello hello 時間 hello webhook 在 Azure 入口網站中的 URL。 您應該注意 hello URL 在安全的位置，供日後使用。 |
| 到期日期 |例如憑證，每個 Webhook 都會有一個到期日期，到期後便無法再使用。  Hello webhook 建立之後，就可以修改此到期日。 |
| 已啟用 |建立 Runbook 時 Webhook 會預設為啟用。  如果設定 tooDisabled，則沒有用戶端可以 toouse 它。  您可以設定 hello**啟用**會建立屬性，當您建立 hello webhook 或一次安裝它。 |

### <a name="parameters"></a>參數
Webhook 可以定義該 webhook 啟動 hello runbook 時所使用的 runbook 參數的值。 hello webhook 必須包含 hello runbook 的必要參數的值，而且可能包含選擇性參數的值。 參數值設定 tooa webhook 可以修改甚至建立 hello webhoook 之後。 多個連結的 webhook tooa 單一 runbook 每個可以使用不同的參數值。

當用戶端啟動使用 webhook runbook 時，它無法覆寫 hello hello webhook 中定義的參數值。  tooreceive 資料來自 hello 用戶端 hello runbook 可以接受單一參數來呼叫**$WebhookData** hello 用戶端包含 hello POST 要求中的類型 [object]，將包含資料。

![Webhookdata 屬性](media/automation-webhooks/webhook-data-properties.png)

hello **$WebhookData**物件都有下列屬性的 hello:

| 屬性 | 說明 |
|:--- |:--- |
| WebhookName |hello hello webhook 名稱。 |
| RequestHeader |包含 hello hello 傳入的 POST 要求的標頭的雜湊資料表。 |
| RequestBody |hello hello 傳入的 POST 要求主體。  這會保留任何的格式，如字串、JSON、XML，或表單已編碼的資料。 hello runbook 必須寫入 toowork 與 hello 預期的資料格式。 |

沒有任何設定的 hello webhook 必要的 toosupport hello **$WebhookData**參數，而且不需要的 tooaccept hello runbook。 它。  如果 hello runbook 未定義 hello 參數，則會忽略任何要求詳細資料的 hello hello 用戶端送出。

如果您指定的值 $WebhookData 當您建立 hello webhook 值將會覆寫時 hello webhook 啟動 hello runbook hello 資料 hello 用戶端 POST 要求，即使 hello 用戶端 hello 要求主體中未包含任何資料。  如果您啟動 runbook 具有 $WebhookData 使用 webhook 以外的方法，您可以為 hello runbook 可辨識的 $Webhookdata 提供值。  這個值應該是以 hello 物件相同[屬性](#details-of-a-webhook)$Webhookdata 以便讓該 hello runbook 可以正確搭配就如同它已使用 webhook 所傳遞的實際 WebhookData 為。

例如，如果您正在啟動 hello hello Azure 入口網站中的下列 runbook，而且想要進行測試，因為 WebhookData 是物件的一些範例 WebhookData toopass，它應該中進行傳遞為 JSON hello UI。

![來自 UI 的 WebhookData 參數](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Hello 上方的 runbook，如果您擁有 hello hello WebhookData 參數的下列屬性：

1. WebhookName: *MyWebhook*
2. RequestHeader: *From=Test User*
3. RequestBody: *[“VM1”, “VM2”]*

然後您可以傳遞下列 JSON 值 hello UI hello WebhookData 參數中的 hello:  

* {"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}

![啟動來自 UI 的 WebhookData 參數](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> hello 的所有輸入參數的值會記錄與 hello runbook 工作。  這表示，任何 hello hello webhook 要求中的用戶端所提供的輸入將會記錄並且可 tooanyone 與存取 toohello 自動化工作。  基於這個原因，您在 Webhook 呼叫中包含機密資訊時應該特別謹慎。
>

## <a name="security"></a>安全性
webhook hello 安全性依賴其 URL，其中包含可讓它 toobe 叫用的安全性權杖的 hello 隱私權。 Azure 自動化不會執行任何驗證 hello 要求，只要它由 toohello 正確的 URL。 基於這個理由，webhook 不應該使用的 runbook，而不使用其他驗證 hello 要求的方式執行高度敏感的功能。

您可以將邏輯包含在已呼叫它的 webhook 藉由檢查 hello hello runbook toodetermine **WebhookName** hello $WebhookData 參數的屬性。 hello runbook 無法執行進一步來驗證特定中尋找資訊 hello **RequestHeader**或**RequestBody**屬性。

另一個策略是 toohave hello runbook 它收到 webhook 要求時，請執行一些外部條件的驗證。  例如，請考慮 GitHub 新認可 tooa GitHub 儲存機制時呼叫的 runbook。  hello runbook 可能會連線 tooGitHub toovalidate 新認可具有實際上只發生在之前繼續進行。

## <a name="creating-a-webhook"></a>建立 Webhook
使用下列程序 toocreate hello Azure 入口網站中的新連結的 webhook tooa runbook hello。

1. 從 hello **Runbook 刀鋒視窗**hello Azure 入口網站，在按一下 hello webhook 的 hello runbook 將會開始 tooview 其詳細資料 刀鋒視窗。
2. 按一下**Webhook**頂端的 hello 刀鋒視窗 tooopen hello hello**新增 Webhook**刀鋒視窗。 <br>
   ![Webhook 按鈕](media/automation-webhooks/webhooks-button.png)
3. 按一下**建立新的 webhook** tooopen hello**建立 webhook 刀鋒視窗**。
4. 指定**名稱**，**到期日**hello webhook 和是否應該啟用。 請參閱 [Webhook 的詳細資料](#details-of-a-webhook) 以取得這些屬性的詳細資訊。
5. 按一下 hello 複製圖示，然後按 Ctrl + C toocopy hello URL hello webhook。  然後將其記錄在安全的地方。  **一旦您建立 hello webhook，就無法再次擷取 hello URL。** <br>
   ![Webhook URL](media/automation-webhooks/copy-webhook-url.png)
6. 按一下**參數**tooprovide hello runbook 參數的值。  如果 hello runbook 有強制性參數，然後就可以 toocreate hello webhook 除非提供值。
7. 按一下**建立**toocreate hello webhook。

## <a name="using-a-webhook"></a>使用 Webhook
toouse webhook 建立之後，用戶端應用程式必須發出 HTTP POST 與 hello hello webhook URL。  hello webhook hello 語法會以下列格式的 hello。

    http://<Webhook Server>/token?=<Token Value>

hello 用戶端會收到 hello hello POST 要求中的下列傳回碼的其中一個。  

| 代碼 | 文字 | 說明 |
|:--- |:--- |:--- |
| 202 |已接受 |已接受 hello 的要求，並已成功排入佇列 hello runbook。 |
| 400 |不正確的要求 |其中一個 hello 下列原因而不接受 hello 要求。 <ul> <li>hello webhook 已到期。</li> <li>hello webhook 已停用。</li> <li>hello URL 中的 hello 語彙基元無效。</li>  </ul> |
| 404 |找不到 |其中一個 hello 下列原因而不接受 hello 要求。 <ul> <li>找不到 hello webhook。</li> <li>找不到 hello runbook。</li> <li>找不到 hello 帳戶。</li>  </ul> |
| 500 |內部伺服器錯誤 |hello URL 有效，但發生錯誤。  請重新送出 hello 要求。 |

假設 hello 要求成功時，hello webhook 回應包含 hello 工作識別碼以 JSON 格式，如下所示。 它會包含單一作業識別碼，但 hello JSON 格式允許潛在未來增強功能。

    {"JobIds":["<JobId>"]}  

hello 用戶端無法判斷 hello runbook 作業完成時，或從 hello webhook 及其完成狀態。  它可以判定這項資訊與另一種方法使用 hello 作業識別碼，例如[Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx)或 hello [Azure 自動化 API](https://msdn.microsoft.com/library/azure/mt163826.aspx)。

### <a name="example"></a>範例
hello 下列範例會使用 Windows PowerShell toostart runbook webhook。  請注意，任何可以進行 HTTP 要求的語言都可以使用 Webhook；Windows PowerShell 在這裡僅作為範例使用。

hello runbook 並收到 hello hello 要求主體中的 JSON 格式的虛擬機器的清單。 我們也會包括啟動 hello hello 要求標頭中誰正在啟動 hello runbook 及 hello 日期和時間的相關資訊。      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


hello 下列影像顯示 hello 標頭資訊 (使用[Fiddler](http://www.telerik.com/fiddler)追蹤) 從這項要求。 這包括標準 HTTP 要求的標頭中加入 toohello 自訂日期和從我們加入的標頭。  每個這些值都是可用 toohello runbook 在 hello **RequestHeaders**屬性**WebhookData**。

![Webhook 按鈕](media/automation-webhooks/webhook-request-headers.png)

hello 下列影像顯示 hello hello 要求主體 (使用[Fiddler](http://www.telerik.com/fiddler)追蹤) 也就是可用 toohello runbook 在 hello **RequestBody**屬性**WebhookData**。 這是因為這是包含 hello hello 要求主體中的 hello 格式格式化為 JSON。     

![Webhook 按鈕](media/automation-webhooks/webhook-request-body.png)

hello 下列影像顯示 hello 要求從 Windows PowerShell 和回應 hello 結果送出。  從回應 hello 和轉換的 tooa 字串擷取 hello 作業識別碼。

![Webhook 按鈕](media/automation-webhooks/webhook-request-response.png)

hello 下列 runbook 範例 hello 先前的範例要求會接受並啟動 hello hello 要求主體中指定的虛擬機器。

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

            # Authenticate tooAzure resources
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
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>回應 tooAzure 警示中啟動 runbook
Webhook 啟用 runbook 可以使用的 tooreact 太[Azure 警示](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。 可以藉由收集 hello 統計資料，例如效能、 可用性及使用量 hello 協助 Azure 警示監視 Azure 中的資源。 您可以收到根據監視您 Azure 資源的計量或事件的警示，目前自動化帳戶僅支援度量。 當 hello 的值指定標準超過指派的 hello 臨界值，或如果觸發 hello 設定事件則 toohello 服務管理員或共同管理員 tooresolve hello 警示，如需度量資訊會傳送通知和事件，請參閱太[Azure 警示](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。

除了使用 Azure 警示以通知系統，您可以也啟動回應 tooalerts 中的 runbook。 Azure 自動化提供 hello 功能 toorun webhook 啟用 runbook 與 Azure 的警示。 當標準超過 hello 會設定臨界值，然後 hello 警示規則變成使用中和觸發程序 hello 依次執行 hello runbook 自動化 webhook。

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>警示內容
Azure 資源，例如虛擬機器，請考慮為此機器的 CPU 使用率 hello 關鍵效能度量的其中一個。 如果 hello CPU 使用率很長一段時間是 100%或更多超過特定大小，您可能想 toorestart hello 虛擬機器 toofix hello 問題。 這可以解決所設定的警示規則 toohello 虛擬機器，此規則會作為其度量的 CPU 百分比。 CPU 百分比這裡只會被視為範例，但有許多其他度量，您可以設定 tooyour Azure 資源，並重新啟動 hello 虛擬機器是動作採取 toofix 此問題，您可以設定 hello runbook tootake 其他動作。

當這個 hello 警示規則變成使用中並觸發程序 hello webhook 啟動 runbook 時，它會傳送 hello 警示內容 toohello runbook。 [警示內容](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)包含詳細資料包括**SubscriptionID**， **ResourceGroupName**， **ResourceName**， **ResourceType**， **ResourceId**和**時間戳記**所需的 hello runbook tooidentify hello 資源所在它將會採取動作。 警示內容內嵌在 hello hello 內文部分**WebhookData**物件傳送的 toohello runbook，並使用可以存取**Webhook.RequestBody**屬性

### <a name="example"></a>範例
建立 Azure 虛擬機器在您的訂用帳戶和相關聯[警示 toomonitor CPU 百分比度量](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。 在建立 hello 警示務必填入 hello webhook hello URL hello webhook 建立 hello webhook 時所產生的欄位。

hello 下列 runbook 範例 hello 警示規則變成使用中，並觸發收集 hello 警示的內容參數所需的 hello runbook tooidentify hello 資源所在它將會採取動作。

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

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
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

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>後續步驟
* 如需不同的方式 toostart runbook 的詳細資訊，請參閱[Starting a Runbook](automation-starting-a-runbook.md)。
* 如需檢視 hello Runbook 工作的狀態資訊，請參閱太[在 Azure 自動化中的執行 Runbook](automation-runbook-execution.md)。
* 如何 toouse Azure 自動化 tootake 動作 Azure 警示，請參閱的 toolearn[修復 Azure VM 警示與自動化 Runbook](automation-azure-vm-alert-integration.md)。
