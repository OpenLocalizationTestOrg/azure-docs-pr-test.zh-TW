---
title: "在 Azure 中 Linux 虛擬機器上的燈 aaaDeploy |Microsoft 文件"
description: "了解 Azure 中的 Linux VM 上 tooinstall hello LAMP 堆疊的方式"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a>在 Azure 上部署 LAMP 堆疊
本文將告訴您如何 toodeploy Apache web 伺服器、 MySQL 和 Azure 上的 PHP （hello LAMP 堆疊）。 您需要 Azure 帳戶 ([取得免費試用](https://azure.microsoft.com/pricing/free-trial/)) 和 hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。 您也可以執行下列步驟以 hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="quick-command-summary"></a>快速命令摘要

1. 儲存並編輯 hello [azuredeploy.parameters.json 檔案](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json)tooyour 喜好設定，在本機電腦上的。
2. 執行下列兩個命令 toocreate hello 資源群組，然後再部署您的範本：

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>在現有 VM 上部署 LAMP
hello 下列安裝 Apache、 MySQL 和 PHP，接著更新封裝的命令：

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>逐步解說在新的 VM 上部署 LAMP

1. 建立資源群組與[az 群組建立](/cli/azure/group#create)toocontain hello 新的 VM:

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate hello VM 本身，您可以使用已撰寫的 Azure Resource Manager 範本，找到[這裡 GitHub 上](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app)。

2. 儲存 hello [azuredeploy.parameters.json 檔案](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json)tooyour 本機電腦。
3. 編輯 hello **azuredeploy.parameters.json**檔案 tooyour 慣用的輸入。
4. 部署與 hello 範本 [az 群組部署建立] 參考 hello 下載 json 檔案：

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

hello 輸出是 toohello 類似下列範例程式碼：

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

您現在已建立安裝了 LAMP 的 Linux VM。 如果您希望，您可以確認 hello 安裝太跳躍向[確認燈安裝成功](#verify-lamp-successfully-installed)。

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>逐步解說在現有 VM 上部署 LAMP
如果您需要協助建立 Linux VM，您可以向[這裡 toolearn 如何 toocreate Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli)。 接下來，您需要 tooSSH 到 hello Linux VM。 如果您需要協助建立 SSH 金鑰，您可以向[這裡 toolearn 如何 toocreate Linux/Mac 上的 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
如果您已經有 SSH 金鑰，請繼續進行，並從您的命令列透過 SSH 使用 `ssh azureuser@mypublicdns.westus.cloudapp.azure.com` 登入 Linux VM。

現在，您使用 Linux VM 內，我們可以逐步完成安裝 hello LAMP 堆疊 Debian 為基礎的發佈。 hello 確實命令可能會與針對其他 Linux 散發版本不同。

#### <a name="installing-on-debianubuntu"></a>安裝在 Debian/Ubuntu 上
您需要下列安裝套件的 hello: `apache2`， `mysql-server`， `php5`，和`php5-mysql`。 直接擷取這些封裝或使用 Tasksel，即可安裝這些封裝。
安裝之前，您需要 toodownload 並更新封裝清單。

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>個別封裝
使用 apt-get：

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>使用 Tasksel
或者，您也可以下載 Tasksel，這是一個 Debian/Ubuntu 工具，以協調工作的方式安裝多個相關套件到您的系統上。

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

後執行的其中一個 hello 上述選項，您將會被提示的 tooinstall，這些封裝和各種其他相依性。 按 'y' 'Enter' toocontinue tooset MySQL 的系統管理密碼，並依照任何其他提示。 此程序會 hello 最小必要的 PHP 延伸模組需要 toouse PHP 安裝 MySQL。 

![][1]

執行下列命令 toosee hello 封裝其他 PHP 延伸模組：

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>建立 info.php 文件
您現在應該能夠 toocheck Apache、 MySQL 和 PHP 您擁有版本透過 hello 命令列輸入`apache2 -v`， `mysql -v`，或`php -v`。

如果您將像是 tootest 此外，您可以建立快速的 PHP 資訊頁面 tooview 瀏覽器中。 透過以下命令，使用 Nano 文字編輯器建立檔案：

```bash
sudo nano /var/www/html/info.php
```

在 hello GNU Nano 文字編輯器 中，加入下列行 hello:

```php
<?php
phpinfo();
?>
```

然後，儲存並結束 hello 文字編輯器。

使用這個命令重新啟動 Apache，讓所有新的安裝生效。

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>確認 LAMP 安裝成功
現在您可以檢查您建立開啟瀏覽器並移 toohttp://youruniqueDNS/info.php hello PHP 資訊頁面。 它看起來應該類似 toothis 映像。

![][2]

您可以檢查您的 Apache 安裝移 tooyou http://youruniqueDNS/ 檢視 hello Apache2 Ubuntu 預設頁面。 hello 輸出是 toohello 類似下列範例程式碼：

![][3]

恭喜，您剛已在 Azure VM 上安裝 LAMP 堆疊！

## <a name="next-steps"></a>後續步驟
簽出 hello hello LAMP 堆疊上的 Ubuntu 文件：

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
