---
title: "aaaAccess 及安全性的 Windows Vm 的 Azure 範本 |Microsoft 文件"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>適用於 Windows VM 之 Azure Resource Manager 範本中的存取和安全性

應用程式裝載於 Azure 可能會需要 toobe 存取 hello 透過網際網路或 VPN / 使用 Azure Express Route 連線。 Hello Music Store 應用程式範例中，與 hello 網站可在網際網路 hello 與公用 IP 位址。 透過建立的存取權，連線 toohello 應用程式及存取 toohello 虛擬機器資源本身應該進行保護。 這項存取安全性是透過「網路安全性群組」來提供。 

這份文件詳細說明如何保護 hello 範例 Azure Resource Manager 範本中的 hello Music Store 應用程式。 所有相依項目和獨特的設定都會以醒目提示的方式標示。 Hello 獲得最佳經驗，針對預先部署 hello 方案 tooyour Azure 訂用帳戶和與 hello Azure Resource Manager 範本一起工作的執行個體。 hello 完成範本可以在這裡 – 找到[音樂存放部署在 Windows 上](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。

## <a name="public-ip-address"></a>公用 IP 位址
可以使用 tooprovide 公用存取 tooan Azure 資源，公用 IP 位址資源。 您可以使用靜態或動態 IP 位址來設定公用 IP 位址。 如果使用動態位址，而且 hello 虛擬機器停止並取消配置，則會移除 hello 位址。 當 hello 機器一次啟動時，它可能會指派不同的公用 IP 位址。 tooprevent 的 IP 位址變更，就可以使用保留的 IP 位址。 

公用 IP 位址可以加入 tooan Azure Resource Manager 範本使用 hello Visual Studio 新增資源精靈，或藉由插入範本中的有效的 JSON。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[公用 IP 位址](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110)。

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

「公用 IP 位址」可以與「虛擬網路介面卡」或「負載平衡器」關聯。 在此範例中，因為 hello Music Store 網站正進行負載平衡跨數個虛擬機器，hello 公用 IP 位址會是附加的 toohello 負載平衡器。

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[與負載平衡器的公用 IP 位址關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211)。

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

hello 做為公用 IP 位址從看到 hello Azure 入口網站。 請注意，hello 公用 IP 位址相關聯的 tooa 負載平衡器並不是虛擬機器。 網路負載平衡器的詳細 hello 本系列的下一個文件。

![公用 IP 位址](./media/dotnet-core-3-access-security/pubip-win.png)

如需有關「Azure 公用 IP 位址」的詳細資訊，請參閱 [Azure 中的 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)。

## <a name="network-security-group"></a>網路安全性群組
一旦存取已建立的 tooAzure 資源，這項存取應該限制。 就 Azure 虛擬機器而言，是使用「網路安全性群組」來達到保護存取的目的。 與 hello Music Store 應用程式範例中，所有存取 toohello 虛擬機器都是除了限制透過 http 存取的連接埠 80 與連接埠 3389 RDP 存取。 網路安全性群組可以加入 tooan Azure Resource Manager 範本使用 hello Visual Studio 新增資源精靈，或藉由插入範本中的有效的 JSON。

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[網路安全性群組](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57)。

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

在此範例中，hello 網路安全性群組是與 hello hello 虛擬網路的資源中宣告的子網路物件相關聯。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[與虛擬網路的網路安全性群組關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143)。

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

以下是哪個 hello 網路安全性群組看起來像 hello 從 Azure 入口網站。 請注意，NSG 可以與子網路和 (或) 網路介面關聯。 在此情況下，hello NSG 是相關聯的 tooa 子網路。 在此組態中，hello 輸入的規則套用 tooall 連接虛擬機器 toohello 子網路。

![網路安全性群組](./media/dotnet-core-3-access-security/nsg-win.png)

如需有關「網路安全性群組」的深入資訊，請參閱[什麼是網路安全性群組](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/)。

## <a name="next-step"></a>後續步驟
<hr>

[步驟 3 - Azure Resource Manager 範本中的可用性和規模](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

