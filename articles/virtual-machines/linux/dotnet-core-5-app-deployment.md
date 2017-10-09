---
title: "aaaAutomating 虛擬機器擴充功能的應用程式部署 |Microsoft 文件"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>使用適用於 Linux VM 的 Azure Resource Manager 範本進行應用程式部署

一旦所有 Azure 基礎結構需求有已找出並轉譯成部署範本，hello 實際的應用程式部署將需要 toobe 定址。 此應用程式部署指 tooinstalling hello 實際的應用程式二進位檔拖曳至 Azure 資源。 Hello 音樂商店範例中，.Net Core、 NGINX 和監督員需要 toobe 每部虛擬機器上安裝和設定。 預先建立 hello Music Store 二進位檔需要 toobe hello 的虛擬機器，安裝和 hello 音樂存放區資料庫。

這份文件詳細說明虛擬機器擴充功能可以自動化應用程式部署和設定 tooAzure 虛擬機器的方式。 所有相依項目和獨特的設定都會以醒目提示的方式標示。 Hello 獲得最佳經驗，針對預先部署 hello 方案 tooyour Azure 訂用帳戶和與 hello Azure Resource Manager 範本一起工作的執行個體。 hello 完成範本可以在這裡 – 找到[音樂存放部署在 Ubuntu 上](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)。

## <a name="configuration-script"></a>組態指令碼
虛擬機器擴充功能是針對虛擬機器 tooprovide 組態自動化來執行的特定的程式。 針對許多特定用途 (防毒、記錄組態及 Docker 組態) 都有擴充功能可供使用。 自訂指令碼延伸可以是使用的 toorun 任何指令碼的虛擬機器。 Hello 音樂商店範例中，用於 toohello 自訂指令碼延伸 tooconfigure hello Ubuntu 虛擬機器及安裝 hello Music Store 應用程式。 

然後再詳細說明如何將虛擬機器擴充功能宣告 Azure Resource Manager 範本中，檢查 hello 指令碼執行。 此指令碼會設定 hello Ubuntu 虛擬機器 toohost hello Music Store 應用程式。 Hello 指令碼執行時，安裝所需的所有軟體，請安裝從原始檔控制的 hello 音樂市集應用程式並準備 hello 資料庫。 

深入了解裝載.Net toolearn 核心應用程式 on Linux，請參閱[發行 tooa Linux 實際執行環境](https://docs.asp.net/en/latest/publishing/linuxproduction.html)。

> 此範例僅供示範之用。
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a>VM 指令碼擴充功能
VM 擴充功能可以執行的虛擬機器在建立時期 hello 延伸模組資源併入 hello Azure Resource Manager 範本。 hello Visual Studio 新增資源精靈，或藉由將有效的 JSON 插入 hello 範本可以加入 hello 延伸模組。 hello 虛擬機器資源; 巢狀 hello 指令碼擴充功能資源這可以在下列範例中的 hello 看到。

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 – [VM 指令碼延伸](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359)。 

請注意，在 hello 下方 hello 指令碼的 JSON 儲存在 GitHub 中。 此指令碼也可以儲存在 Azure Blob 儲存體中。 此外，Azure 資源管理員範本可讓 hello 指令碼執行字串 tooconstructed 範本參數的值可以使用做為參數執行指令碼。 部署 hello 範本時，在此情況下提供資料並執行 hello 指令碼時，可以接著使用這些值。

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

如需有關使用 hello 自訂指令碼延伸模組的詳細資訊，請參閱[自訂指令碼延伸模組與資源管理員範本](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="next-step"></a>後續步驟
<hr>

[探索其他 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates)

