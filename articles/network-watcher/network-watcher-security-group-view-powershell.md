---
title: "與 Azure 網路監看員安全性群組檢視 PowerShell aaaAnalyze 網路安全性 |Microsoft 文件"
description: "本文將說明如何 toouse PowerShell tooanalyze 的虛擬機器安全性與安全性的群組檢視。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a>使用 PowerShell，利用安全性群組檢視分析虛擬機器的安全性

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

安全性的群組檢視會傳回已設定且有效的網路安全性規則所套用的 tooa 虛擬機器。 這項功能會很有用的 tooaudit 及診斷網路安全性群組和 VM tooensure 流量所設定的規則已正確地允許或拒絕。 在本文中，我們會示範如何設定 tooretrieve hello 和有效的安全性規則 tooa 虛擬機器使用 PowerShell

## <a name="before-you-begin"></a>開始之前

在此案例中，您會執行 hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello 安全性規則資訊。

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

## <a name="scenario"></a>案例

hello 案例涵蓋在本文中擷取設定的 hello 和指定的虛擬機器的有效的安全性規則。

## <a name="retrieve-network-watcher"></a>擷取網路監看員

hello 第一個步驟是 tooretrieve hello 網路監看員執行個體。 這個變數會傳遞 toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet。

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a>取得 VM

虛擬機器為必要的 toorun hello`Get-AzureRmNetworkWatcherSecurityGroupView`針對 cmdlet。 下列範例中的 hello 取得 VM 物件。

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a>擷取安全性群組檢視

hello 下一個步驟是 tooretrieve hello 安全性的群組檢視結果。

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a>檢視 hello 結果

hello 下列範例是縮短的回應 hello 傳回的結果。 hello 結果會顯示所有 hello 有效且套用安全性規則 hello 細分的群組中的虛擬機器上**NetworkInterfaceSecurityRules**， **DefaultSecurityRules**，和**EffectiveSecurityRules**。

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a>後續步驟

請瀏覽[稽核網路安全性群組群組 (NSG) 與網路監看員](network-watcher-nsg-auditing-powershell.md)toolearn 如何 tooautomate 驗證的網路安全性群組。


