---
title: "aaaDeploying Linux 計算資源與 Azure 資源管理員範本 |Microsoft 文件"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a>使用適用於 Linux VM 之 Azure Resource Manager 範本的應用程式架構

在開發 Azure Resource Manager 部署時，計算需求需要對應的 toobe tooAzure 資源和服務。 如果應用程式是由數個 http 端點、 資料庫和資料快取服務所組成，hello 裝載每個元件的 Azure 資源需要 toobe 合理化。 比方說，hello 範例 Music Store 應用程式包含虛擬機器裝載的 web 應用程式和 SQL 資料庫中，裝載於 Azure SQL database。 

本文件詳述 hello Music Store 計算資源 hello 範例 Azure Resource Manager 範本中設定的方式。 所有相依項目和獨特的設定都會以醒目提示的方式標示。 Hello 獲得最佳經驗，針對預先部署 hello 方案 tooyour Azure 訂用帳戶和與 hello Azure Resource Manager 範本一起工作的執行個體。 hello 完成範本可以在這裡 – 找到[音樂存放部署在 Ubuntu 上](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。 

## <a name="virtual-machine"></a>虛擬機器
hello Music Store 應用程式包含 web 應用程式，其中客戶可以瀏覽及購買音樂。 雖然有好幾個 Azure 服務可以裝載 Web 應用程式，但是這個範例是使用「虛擬機器」。 使用 hello 範例 Music Store 範本，在部署虛擬機器、 web 伺服器安裝及 hello Music Store 網站安裝及設定。 為了本文章的 hello 起見，hello 虛擬機器部署會詳細說明。 hello 設定 hello web 伺服器與 hello 應用程式的更新版本的文件會詳細說明。

虛擬機器可以加入 tooa 範本使用 hello Visual Studio 加入新資源精靈，或有效的 JSON 插入 hello 部署範本。 部署虛擬機器時，也需要數個相關的資源。 如果使用 Visual Studio toocreate hello 範本，則會為您建立這些資源。 若以手動方式建構 hello 範本，這些資源需要 toobe 插入並設定。

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬機器 JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295)。

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
      ........<truncated>  
    }
```

一旦部署之後，hello Azure 入口網站中可以看到 hello 虛擬機器內容。

![虛擬機器](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a>儲存體帳戶
儲存體帳戶有許多儲存體選項和功能。 Hello 的 Azure 虛擬機器的內容，儲存體帳戶會保留 hello 虛擬硬碟的 hello 虛擬機器與其他所有資料磁碟。 hello Music Store 範例 hello 部署中包含一個儲存體帳戶 toohold hello 虛擬硬碟的每個虛擬機器。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[儲存體帳戶](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109)。

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

儲存體帳戶是內 hello 資源管理員範本宣告 hello 虛擬機器的虛擬機器相關聯。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬機器與儲存體帳戶的關聯](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341)。

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

部署之後，可以在 hello Azure 入口網站中檢視 hello 儲存體帳戶。

![儲存體帳戶](./media/dotnet-core-2-architecture/storacct.png)

按一下至 hello 儲存體帳戶 blob 容器中，可以看到每個虛擬機器使用 hello 範本部署的 hello 虛擬硬碟檔案。

![虛擬硬碟](./media/dotnet-core-2-architecture/vhd.png)

如需有關「Azure 儲存體」的資訊，請參閱 [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)。

## <a name="virtual-network"></a>虛擬網路
如果虛擬機器需要內部網路，例如 hello 能力 toocommunicate 與其他虛擬機器和 Azure 資源，Azure 虛擬網路是必要的。  虛擬網路不會進行 hello 虛擬機器可以透過 hello 網際網路。 公用連線能力需要公用 IP 位址，本系列稍後會詳細說明。

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬網路和子網路](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136)。

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

Hello Azure 入口網站，從 hello 虛擬網路看起來像下列映像的 hello。 請注意，使用 hello 範本部署的所有虛擬機器附加的 toohello 虛擬網路。

![虛擬網路](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a>網路介面
 網路介面正在連線的虛擬機器 tooa 虛擬網路、 更明確地說 hello 虛擬網路中已定義 tooa 子網路。 

 請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[網路介面](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166)。

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

每個虛擬機器資源都包含一個網路設定檔。 hello 網路介面是 hello 這個設定檔中的虛擬機器相關聯。  

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 –[虛擬機器的網路設定檔](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350)。

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

Hello Azure 入口網站，從 hello 網路介面看起來像下列映像的 hello。 hello 內部 IP 位址和 hello 虛擬機器關聯可以看見 hello 網路介面資源上。

![網路介面](./media/dotnet-core-2-architecture/nic.png)

如需有關「Azure 虛擬網路」的詳細資訊，請參閱 [Azure 虛擬網路文件](https://azure.microsoft.com/documentation/services/virtual-network/)。

## <a name="azure-sql-database"></a>Azure SQL Database
此外 tooa 裝載 hello 音樂商店的網站，Azure SQL Database 的虛擬機器是部署的 toohost hello Music Store 資料庫。 這裡使用 Azure SQL Database 的 hello 優點是不是必要項目，第二組的虛擬機器，hello 服務內建延展性和可用性。

可以使用 Visual Studio 加入新資源精靈，或藉由插入範本中的有效的 JSON hello 加入 Azure SQL database。 hello SQL Server 資源包含使用者名稱和密碼會授與 hello SQL 執行個體上的系統管理權限。 此外，也會新增 SQL 防火牆資源。 根據預設，在 Azure 中裝載的應用程式會無法 tooconnect 與 hello SQL 執行個體。 tooallow 外部應用程式這類的 SQL Server Management studio tooconnect toohello SQL 執行個體，需要設定 toobe hello 防火牆。 Hello Music Store 示範的 hello 起見，hello 預設組態是正常的。 

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401)。

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Hello SQL server 和 MusicStore 資料庫 hello Azure 入口網站中所見的檢視。

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

如需有關部署 Azure SQL Database 的詳細資訊，請參閱 [Azure SQL Database 文件](https://azure.microsoft.com/documentation/services/sql-database/)。

## <a name="next-step"></a>後續步驟
<hr>

[步驟 2 - Azure Resource Manager 範本中的存取和安全性](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

