---
title: "aaaAvailability 和 Azure 資源管理員範本中的小數位數 |Microsoft 文件"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a>適用於 Linux VM 之 Azure Resource Manager 範本中的可用性和規模

可用性和延展性，請參閱 toouptime 且 hello 能力 toomeet 要求。 如果應用程式必須是 99.9%的 hello 時間，它會需要 toohave 架構，可以讓多個並行的計算資源。 比方說，而不是單一網站，具有高可用性的組態包含多個執行個體的 hello 相同站台，以平衡前面的技術。 此設定會 hello 應用程式的一個執行個體可以進行停機維護，剩餘的 hello 繼續 toofunction 時。 標尺上 hello 另一方面參考 tooan 應用程式的能力 tooserve 需求。 負載平衡應用程式，新增或移除執行個體從 hello 集區可讓應用程式 tooscale toomeet 需求。

本文件詳述 hello Music Store 範例部署可用性與延展性的設定方式。 所有相依項目和獨特的設定都會以醒目提示的方式標示。 Hello 獲得最佳經驗，針對預先部署 hello 方案 tooyour Azure 訂用帳戶和與 hello Azure Resource Manager 範本一起工作的執行個體。 hello 完成範本可以在這裡 – 找到[音樂存放部署在 Ubuntu 上](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。

## <a name="availability-set"></a>可用性設定組
「可用性設定組」可讓「Azure 虛擬機器」以邏輯方式跨不同的實體主機和其他基礎結構元件，例如電源供應器和實體網路硬體。 可用性設定組可確保在維護期間，裝置故障或其他停機狀況不會影響到所有虛擬機器。 可用性設定組可以加入 tooan Azure Resource Manager 範本使用 hello Visual Studio 新增資源精靈，或插入範本中的有效的 JSON。

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[可用性設定組](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387)。

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

「可用性設定組」會宣告為「虛擬機器」資源的屬性。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[與虛擬機器的可用性設定組關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313)。

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
hello 可用性設定組如同 hello Azure 入口網站。 此處所述每個虛擬機器以及 hello 設定詳細資料。

![可用性設定組](./media/dotnet-core-4-availability-scale/aset.png)

如需有關「可用性設定組」的深入資訊，請參閱 [管理虛擬機器的可用性](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 

## <a name="network-load-balancer"></a>網路負載平衡器
可用性設定組會提供應用程式容錯移轉，而負載平衡器讓 hello 應用程式的許多執行個體上可使用單一網路位址。 應用程式的多個執行個體可以裝載多個虛擬機器，每個連接 tooa 負載平衡器。 存取 hello 應用程式時，則 hello 負載平衡器路由 hello hello 附加成員之間連入要求。 負載平衡器可以使用 hello Visual Studio 新增資源精靈，加入或插入正確格式化 JSON 資源到 hello Azure Resource Manager 範本。

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[網路負載平衡器](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208)。

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

因為 hello 範例應用程式公開的 toohello 網際網路的公用 IP 位址，此位址是 hello 負載平衡器相關聯。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[公用 IP 位址的網路負載平衡器關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221)。

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Hello Azure 入口網站，從 hello 網路負載平衡器概觀會顯示 hello 和 hello 公用 IP 位址之間的關聯。

![網路負載平衡器](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a>負載平衡器規則
使用負載平衡器，當規則被設定可控制流量如何平衡 hello 適合資源。 Hello 範例 Music Store 應用程式時，流量會到達連接埠 80 的公用 IP 位址 hello 和分散到所有虛擬機器的通訊埠 80。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[負載平衡器規則](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270)。

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

檢視 hello 網路負載平衡器規則從 hello 入口網站。

![網路負載平衡器規則](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a>負載平衡器探查
hello 負載平衡器也需要 toomonitor 每部虛擬機器，以便要求是只有 toorunning 系統。 這項監視會透過經常探查預先定義的連接埠來進行。 hello Music Store 部署是設定的 tooprobe 連接埠 80 上所有包含虛擬機器。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[負載平衡器探查](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257)。

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

從 hello Azure 入口網站看到 hello 負載平衡器探查。

![網路負載平衡器探查](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a>輸入 NAT 規則
當使用負載平衡器時，需要 toobe 規則放置提供非負載平衡的存取 tooeach 虛擬機器。 例如，建立與每個虛擬機器的 SSH 連線時，不應該對此流量進行負載平衡，而是應該設定一個預先決定的路徑。 設定預先決定的路徑時是使用「輸入 NAT 規則」資源來設定。 輸入的通訊使用這項資源，可以是對應的 tooindividual 虛擬機器。 

以 hello Music Store 應用程式，開始 5000 連接埠會是對應的 tooport 22 每部虛擬機器上進行 SSH 存取。 hello`copyindex()`函式是使用的 tooincrement hello 連入通訊埠，例如 hello 第二個虛擬機器接收 5001 連入通訊埠、 hello 第三個 5002，依此類推。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[輸入 NAT 規則](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270)。 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

其中一個範例中所見 hello Azure 入口網站與輸入 NAT 規則。 SSH NAT 規則會建立 hello 部署中每部虛擬機器。

![輸入 NAT 規則](./media/dotnet-core-4-availability-scale/natrule.png)

深入了解 hello Azure 網路負載平衡器的詳細資訊，請參閱[Azure 基礎結構服務部署的負載平衡](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="deploy-multiple-vms"></a>部署多個 VM
最後，可用性設定組或負載平衡器 tooeffectively 函式，就需要多部虛擬機器。 可以使用 hello Azure Resource Manager 範本複製功能來部署多個 Vm。 使用 hello 複製函式，不需要 toodefine 有限數目的虛擬機器，而不是此值可以為部署的 hello 次動態提供。 hello 複製函式會消耗 hello toocreated 執行個體和部署 hello 適當數目的虛擬機器和相關聯的資源控制代碼數目。

在 hello 音樂存放區範例範本，參數會定義在執行個體計數會採用。 建立虛擬機器和相關的資源時，此編號用整個 hello 範本。

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

在 hello 虛擬機器資源，hello 複製迴圈會給予的名稱，hello 的執行個體參數用產生複本 toocontrol hello 數目。

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬機器複製函式](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300)。 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

hello hello 複製函式的 目前反覆項目可以存取以 hello`copyIndex()`函式。 hello hello 複製索引函式值可以是使用的 tooname 虛擬機器和其他資源。 例如，如果部署兩個虛擬機器執行個體，它們將需要不同的名稱。 hello`copyIndex()`函式可以做為屬於 hello 虛擬機器名稱 toocreate 唯一的名稱。 舉例來說，hello `copyindex()` hello 虛擬機器資源中可以看到用來命名之用的函式。 此處 hello 電腦名稱是串連的 hello`vmName`參數和 hello`copyIndex()`函式。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[複製索引功能](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319)。 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

hello`copyIndex`函式 hello Music Store 範例範本中使用多次。 資源和函式，利用`copyIndex`包含任何項目特定 tooa hello 虛擬機器網路介面，負載平衡器規則，例如單一執行個體和任何相依於函式。 

如需有關 hello 複製功能的詳細資訊，請參閱[Azure 資源管理員中建立資源的多個執行個體](../../resource-group-create-multiple.md)。

## <a name="next-step"></a>後續步驟
<hr>

[步驟 4 - 使用 Azure Resource Manager 範本進行應用程式部署](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

