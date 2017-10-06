---
title: "aaaTroubleshoot Azure 虛擬網路閘道與連線-PowerShell |Microsoft 文件"
description: "此頁面說明 toouse hello Azure 網路監看員如何疑難排解 PowerShell cmdlet"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>使用 Azure 網路監看員 PowerShell 來針對虛擬網路閘道和連線進行疑難排解

> [!div class="op_single_selector"]
> - [入口網站](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

網路監看員會提供許多功能與 toounderstanding 您在 Azure 中的網路資源。 這些功能的其中之一便是資源疑難排解。 疑難排解資源可以透過 hello 入口網站、 PowerShell、 CLI 或 REST API 呼叫。 呼叫時，網路監看員會檢查 hello 的虛擬網路閘道或連線的健全狀況，並傳回其發現。

## <a name="before-you-begin"></a>開始之前

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

如需支援的閘道類型清單，請瀏覽[支援的閘道類型](network-watcher-troubleshoot-overview.md#supported-gateway-types)。

## <a name="overview"></a>概觀

疑難排解資源提供 hello 功能的虛擬網路閘道與連線發生問題進行疑難排解。 當提出要求時 tooresource 疑難排解記錄檔正在檢查和查詢。 檢查完成時，會傳回 hello 結果。 疑難排解要求是長時間執行的資源要求，但這可能需要多個分鐘 tooreturn 結果。 hello 疑難排解記錄檔會儲存在指定的儲存體帳戶的容器。

## <a name="retrieve-network-watcher"></a>擷取網路監看員

hello 第一個步驟是 tooretrieve hello 網路監看員執行個體。 hello`$networkWatcher`變數傳遞 toohello`Start-AzureRmNetworkWatcherResourceTroubleshooting`步驟 4 中的 cmdlet。

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a>擷取虛擬網路閘道連線

在此範例中，系統會對連線執行資源疑難排解。 您也可以將它傳遞給虛擬網路閘道。

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a>建立儲存體帳戶

疑難排解資源傳回 hello hello 資源健全狀況的相關資料，它也會儲存記錄檔 tooa 儲存體帳戶 toobe 檢閱。 在此步驟中，我們會建立儲存體帳戶，如果已有現有的儲存體帳戶，您也可以使用它。

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a>執行網路監看員資源疑難排解

疑難排解資源以 hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet。 我們傳遞 hello cmdlet hello 網路監看員物件、 hello hello 連線的識別碼或虛擬網路閘道、 hello 儲存體帳戶的識別碼，以及 hello 路徑 toostore hello 結果。

> [!NOTE]
> hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet 是長時間執行，而且可能要花幾分鐘的時間 toocomplete。

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

一旦您執行 hello cmdlet，網路監看員會檢閱 hello 資源 tooverify hello 健全狀況。 它會傳回 hello 結果 toohello shell，並將指定 hello 儲存體帳戶中的 hello 結果的記錄檔。

## <a name="understanding-hello-results"></a>了解 hello 結果

動作的 hello 文字上 tooresolve hello 問題的方式，提供一般指引。 Hello 問題，可以採取的動作，如果是其他指南提供的連結。 Hello 案例中的任何其他指引，hello 回應提供 hello url tooopen 支援案例。  如需回應 hello 和時要包含的 hello 屬性的詳細資訊，請瀏覽[網路監看員疑難排解概觀](network-watcher-troubleshoot-overview.md)

如需從 azure 儲存體帳戶下載檔案的指示，請參閱太[開始使用適用於.NET 的 Azure Blob 儲存體使用](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。 另一項可用工具為儲存體總管。 儲存體總管的詳細資訊可以在這裡找到在 hello 下列連結：[存放裝置總管](http://storageexplorer.com/)

## <a name="next-steps"></a>後續步驟

如果設定已變更為該停止 VPN 連線能力，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack 向 hello 網路安全性群組和安全性規則，可能會有問題。
