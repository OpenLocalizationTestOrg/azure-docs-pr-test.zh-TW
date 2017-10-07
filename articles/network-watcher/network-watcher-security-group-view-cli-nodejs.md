---
title: "與 Azure 網路監看員安全性群組檢視 Azure CLI 1.0 aaaAnalyze 網路安全性 |Microsoft 文件"
description: "本文將說明如何 toouse Azure CLI 1.0 tooanalyze 的虛擬機器安全性與安全性的群組檢視。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a>使用 Azure CLI 1.0，利用安全性群組檢視分析虛擬機器的安全性

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [CLI 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

安全性的群組檢視會傳回已設定且有效的網路安全性規則所套用的 tooa 虛擬機器。 這項功能會很有用的 tooaudit 及診斷網路安全性群組和 VM tooensure 流量所設定的規則已正確地允許或拒絕。 在本文中，我們會示範如何設定 tooretrieve hello 和有效的安全性規則 tooa 虛擬機器使用 Azure CLI

本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。 網路監看員目前使用 Azure CLI 1.0 提供 CLI 支援。

## <a name="before-you-begin"></a>開始之前

此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。

## <a name="scenario"></a>案例

hello 案例涵蓋在本文中擷取設定的 hello 和指定的虛擬機器的有效的安全性規則。

## <a name="get-a-vm"></a>取得 VM

虛擬機器為必要的 toorun hello `vm list` cmdlet。 hello 下列命令會列出資源群組中的 hello 虛擬 machinese:

```azurecli
azure vm list -g resourceGroupName
```

一旦您知道 hello 虛擬機器，您可以使用 hello `vm show` cmdlet tooget 其資源識別碼：

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a>擷取安全性群組檢視

hello 下一個步驟是 tooretrieve hello 安全性的群組檢視結果。 新增 hello"-json 」 旗標將會在 json 中的 hello 結果格式化。

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a>檢視 hello 結果

hello 下列範例是縮短的回應 hello 傳回的結果。 hello 結果會顯示所有 hello 有效且套用安全性規則 hello 細分的群組中的虛擬機器上**NetworkInterfaceSecurityRules**， **DefaultSecurityRules**，和**EffectiveSecurityRules**。

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a>後續步驟

請瀏覽[稽核網路安全性群組群組 (NSG) 與網路監看員](network-watcher-nsg-auditing-powershell.md)toolearn 如何 tooautomate 驗證的網路安全性群組。

深入了解 hello 安全性規則所套用的 tooyour 網路資源，造訪[安全性的群組檢視概觀](network-watcher-security-group-view-overview.md)
