---
title: "使用 Azure 網路監看員安全性的群組檢視稽核的 aaaAutomate NSG |Microsoft 文件"
description: "此頁面提供有關指示 tooconfigure 稽核的網路安全性群組"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a>使用 Azure 網路監看員安全性群組檢視自動化 NSG 稽核

客戶通常會面對 hello 挑戰的驗證基礎結構的 hello 安全性狀態。 這項挑戰在其 Azure 中的 VM 沒有不同。 很重要的 toohave 類似的安全性設定檔為基礎套用 hello 網路安全性群組 (NSG) 規則。 使用 hello 安全性的群組檢視，您現在可以取得 hello 套用規則 tooa NSG 中的 VM 清單。 您可以定義標準的 NSG 安全性設定檔並起始以每週的步調安全性的群組檢視和比較 hello 輸出 toohello 標準設定檔和建立報表。 如此一來您可以識別就能輕鬆所有不符合規定的安全性設定檔的 toohello hello Vm。

如果您不熟悉網路安全性群組，請造訪[網路安全性概觀](../virtual-network/virtual-networks-nsg.md)

## <a name="before-you-begin"></a>開始之前

在此案例中，您可以比較已知的理想基準 toohello 安全性群組檢視虛擬機器所傳回的結果。

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。 hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。

## <a name="scenario"></a>案例

本文涵蓋的 hello 案例取得 hello 安全性的群組檢視虛擬機器。

在此案例中，您將會：

- 擷取已知的良好規則集
- 使用 REST API 擷取虛擬機器
- 取得虛擬機器的安全性群組檢視
- 評估回應

## <a name="retrieve-rule-set"></a>擷取規則集

在此範例中的 hello 第一個步驟是 toowork 與現有的基準。 hello 下列範例是擷取自現有網路安全性群組使用 hello 某些 json `Get-AzureRmNetworkSecurityGroup` hello 基準為用於此範例中的 cmdlet。

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-toopowershell-objects"></a>轉換規則集 tooPowerShell 物件

在此步驟中，我們正在閱讀的 hello 規則，會在此範例中的 hello 網路安全性群組的預期的 toobe 稍早建立的 json 檔案。

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a>擷取網路監看員

hello 下一個步驟是 tooretrieve hello 網路監看員執行個體。 hello`$networkWatcher`變數傳遞 toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet。

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>取得 VM

虛擬機器為必要的 toorun hello`Get-AzureRmNetworkWatcherSecurityGroupView`針對 cmdlet。 下列範例中的 hello 取得 VM 物件。

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a>擷取安全性群組檢視

hello 下一個步驟是 tooretrieve hello 安全性的群組檢視結果。 這個結果會是比較的 toohello 稍早顯示的 「 數基準 」 json。

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a>分析 hello 結果

hello 回應分組依據的網路介面。 hello 不同類型傳回的規則會生效，且預設安全性規則。 hello 結果進一步細分由及其套用方式，在子網路或虛擬 nic。

hello 下列 PowerShell 指令碼比較 hello hello NSG 的安全性的群組檢視 tooan 現有輸出結果。 hello 下列範例是簡單的範例的方式比較 hello 結果與`Compare-Object`cmdlet。

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

下列範例中的 hello 是 hello 結果。 您可以看到兩個已 hello 第一個規則集合中的 hello 規則沒有出現在 hello 比較。

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a>後續步驟

如果設定已變更，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack 向 hello 網路安全性群組和安全性規則，會有問題。













