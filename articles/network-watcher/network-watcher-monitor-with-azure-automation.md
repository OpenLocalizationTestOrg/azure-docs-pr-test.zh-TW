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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>使用網路監看員疑難排解來監視 VPN 閘道

取得對網路效能的深入分析是重大 tooprovide 可靠服務 toocustomers。 它是關鍵 toodetect 網路中斷狀況快速而採取矯正措施 toomitigate hello 中斷情況。 Azure 自動化可讓您 tooimplement，並透過 runbook，以程式設計的方式執行工作。 使用 Azure 自動化會建立一個完美的配方，讓您執行連續且主動的網路監視和警示。

## <a name="scenario"></a>案例

hello 下列映像中的 hello 案例位於多層式應用程式中，以建立使用 VPN 閘道和通道的內部部署連線。 確保的 hello VPN 閘道已啟動及執行 」 是重大 toohello 應用程式效能。

Hello VPN 通道，使用 hello 資源疑難排解 API toocheck 的連線通道狀態的連接狀態的指令碼 toocheck 建立 runbook。 Tooadministrators 如果 hello 狀態狀況不良，傳送電子郵件觸發程序。

![案例範例][scenario]

此案例將會：

- 建立 runbook 呼叫 hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot 連線狀態
- 排程 toohello runbook 連結

## <a name="before-you-begin"></a>開始之前

在開始這個案例之前，您必須擁有 hello 下列先決條件：

- 在 Azure 中使用 Azure 自動化帳戶。 請確認 hello 自動化帳戶有 hello 最新的模組，然後也有 hello AzureRM.Network 模組。 hello AzureRM.Network 模組位於 hello 模組資源庫如果您需要 tooadd 它 tooyour 自動化帳戶。
- 您必須在 Azure 自動化中設定一組認證。 在 [Azure 自動化安全性](../automation/automation-security-overview.md)深入了解
- 有效的 SMTP 伺服器 (Office 365、您的內部部署電子郵件或其他) 和 Azure 自動化中定義的認證
- 在 Azure 中已設定的虛擬網路閘道。
- 現有的容器 toostore hello 的現有儲存體帳戶記錄中。

> [!NOTE]
> hello 前面影像所示的 hello 基礎結構供說明用途並不會建立 hello 本文中所包含的步驟。

### <a name="create-hello-runbook"></a>建立 hello runbook

hello 第一個步驟 tooconfiguring hello 範例是 toocreate hello runbook。 這個範例會使用「執行身分」帳戶。 toolearn 需執行身分帳戶，請瀏覽[驗證 Runbook 與 Azure 執行身分帳戶](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>步驟 1

瀏覽 tooAzure 自動化在 hello [Azure 入口網站](https://portal.azure.com)按一下**Runbook**

![自動化帳戶概觀][1]

### <a name="step-2"></a>步驟 2

按一下**新增 runbook** toostart hello runbook 的 hello 建立程序。

![runbook 刀鋒視窗][2]

### <a name="step-3"></a>步驟 3

在下**快速建立**，按一下 **建立新的 runbook** toocreate hello runbook。

![新增 runbook 刀鋒視窗][3]

### <a name="step-4"></a>步驟 4

在此步驟中，我們為 hello runbook 的名稱，在 hello 範例中呼叫它**Get VPNGatewayStatus**。 它是重要的 toogive hello runbook 的描述性的名稱，並建議以遵循標準 PowerShell 命名標準的名稱。 此範例中的 hello runbook 類型為**PowerShell**，hello 其他選項包括圖形，PowerShell 工作流程，以及圖形化 PowerShell 工作流程。

![runbook 刀鋒視窗][4]

### <a name="step-5"></a>步驟 5

在此步驟中 hello 建立 runbook、 hello 下列程式碼範例提供所有 hello hello 範例所需的程式碼。 hello hello 程式碼中包含的項目\<值\>需要 toobe hello 從您的訂用帳戶的值取代。

使用 hello 下列程式碼為按一下**儲存**

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

### <a name="step-6"></a>步驟 6

排程 hello runbook 儲存之後，必須是連結的 hello runbook tooit tooautomate hello 開頭。 toostart hello 程序中，按一下 **排程**。

![步驟 6][6]

## <a name="link-a-schedule-toohello-runbook"></a>排程 toohello runbook 連結

您必須建立新的排程。 按一下**排程 tooyour runbook 連結**。

![步驟 7][7]

### <a name="step-1"></a>步驟 1

在 hello**排程**刀鋒視窗中，按一下 **建立新的排程**

![步驟 8][8]

### <a name="step-2"></a>步驟 2

在 hello**新排程**刀鋒視窗填滿 hello 排程資訊。 您可以將的 hello 值為 hello 下列清單中：

- **名稱**-hello hello 排程的好記的名稱。
- **描述**-hello 排程的描述。
- **啟動**-這個值是日期、 時間和時區 hello 時間 hello 排程觸發程序所構成的組合。
- **循環**-這個值會決定 hello 排程重複。  有效值為 [一次] 或 [重複]。
- **循環每**-小時、 天、 週或月中的 hello 排程 hello 循環間隔。
- **設定到期日**-hello 值會決定 hello 排程是否應過期。 您可以將太**是**或**否**。 有效的日期和時間是 toobe 提供如果選擇 [是]。

> [!NOTE]
> 如果您需要 toohave 頻率超過每個小時以上執行 runbook 時，必須在不同的時間間隔 （也就是 15、 30-45 分鐘內，在 hello 小時後） 建立多個排程

![步驟 9][9]

### <a name="step-3"></a>步驟 3

按一下 儲存 toosave hello 排程 toohello runbook。

![步驟 10][10]

## <a name="next-steps"></a>後續步驟

既然您已了解如何 toointegrate 網路監看員疑難排解 Azure 自動化中，以了解如何 tootrigger 擷取封包 VM 警示造訪[與 Azure 網路監看員建立警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md).

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
