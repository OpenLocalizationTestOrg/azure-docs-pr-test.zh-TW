---
title: "驗證與 Azure 網路監看員 IP 流量 aaaVerify 流量-REST |Microsoft 文件"
description: "本文說明如何 toocheck 如果允許或拒絕流量 tooor 從虛擬機器"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>使用 Azure 網路監看員的 IP 流程驗證元件來檢查流量是被允許或拒絕

> [!div class="op_single_selector"]
> - [Azure 入口網站](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)


IP 流量驗證是一項功能可讓您 tooverify 如果允許 tooor 從虛擬機器的流量的網路監看員。 hello 驗證可以執行傳入或傳出的流量。 這個案例中很有用 tooget 的虛擬機器是否可以彼此通訊 tooan 外部資源或後端的目前狀態。 IP 流量確認是否可使用的 tooverify，是否您的網路安全性群組 (NSG) 規則都已正確設定及疑難排解 NSG 規則而遭到封鎖的流量。 另一個原因需要使用 IP 流程可讓您確認是否想要封鎖 tooensure 流量正在封鎖正確 hello NSG。

## <a name="before-you-begin"></a>開始之前

ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。 您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

## <a name="scenario"></a>案例

此案例使用 IP 流量確認 tooverify，如果虛擬機器可以彼此 tooanother 機器通訊透過連接埠 443。 如果 hello 流量遭到拒絕，它會傳回 hello 安全性規則，拒絕的流量。 進一步了解 IP 流量，請確認 toolearn 造訪[IP 流量確認概觀](network-watcher-ip-flow-verify-overview.md)

在此案例中，您將會：

* 擷取虛擬機器
* 呼叫 IP 流程驗證
* 驗證結果

## <a name="log-in-with-armclient"></a>使用 ARMClient 登入

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>擷取虛擬機器

執行下列指令碼 tooreturn hello 虛擬機器。 hello 下列程式碼需要的值為 hello 變數：

* **subscriptionId** -hello 訂用帳戶 Id toouse。
* **resourceGroupName** -hello 包含虛擬機器的資源群組的名稱。

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

hello 所需的資訊是 hello 識別碼 hello 類型之下`Microsoft.Compute/virtualMachines`。 hello 結果應該類似下列程式碼範例的 toohello:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a>呼叫 IP 流程驗證

hello 下列範例會建立指定的虛擬機器要求 tooverify hello 流量。 如果允許 hello 流量或 hello 流量遭到拒絕，就會傳回 hello 回應。 如果已拒絕的流量，它也會傳回哪些規則區塊 hello 流量。

> [!NOTE]
> IP 流量確認需要 hello VM 資源一配置。

hello 指令碼需要 hello 資源識別碼和 hello 虛擬機器上的網路介面卡的虛擬機器。 Hello，上述輸出會提供這些值。

> [!Important]
> 所有網路監看員 REST 呼叫 hello hello 要求 URI 為 hello 另一個則包含 hello 網路監看員執行個體，不會 hello 您執行的 hello 診斷動作的資源中的資源群組名稱。

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a>了解 hello 結果

您會回到 hello 回應會告訴您是否允許或拒絕 hello 流量。 hello 回應看起來像 hello 遵循範例的其中一個：

**允許**

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

**拒絕**

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a>後續步驟

如果正在封鎖流量，不應該看到[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)toolearn 更多關於網路安全性群組。












