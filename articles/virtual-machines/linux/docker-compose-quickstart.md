---
title: "在 Azure 中的 Linux VM 上的 Docker Compose aaaUse |Microsoft 文件"
description: "Toouse Docker 和 Linux 的虛擬機器上撰寫 hello Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>取得開始使用 Docker 和撰寫 toodefine 並在 Azure 中執行多個容器應用程式
與[撰寫](http://github.com/docker/compose)，您可以使用簡單的文字檔案 toodefine 組成的多個 Docker 容器應用程式。 然後加速您的應用程式中的單一命令的一切 toodeploy 您定義的環境。 例如，本文章將示範如何 tooquickly WordPress 部落格與後端 MariaDB SQL 資料庫上設定 Ubuntu VM。 您也可以使用撰寫 tooset 組成更複雜的應用程式。


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>設定 Linux VM 做為 Docker 主機
您可以在 hello Azure Marketplace toocreate Linux VM 中使用各種 Azure 的程序和可用的映像或資源管理員範本，並將它設定為 Docker 主機。 例如，請參閱[使用您環境的 hello Docker VM 擴充功能 toodeploy](dockerextension.md) tooquickly Ubuntu VM 以 hello Azure Docker VM 延伸模組建立使用[快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)。 

當您使用 hello Docker VM 擴充功能時，您的 VM 會自動設定為 Docker 主機，且已安裝撰寫。


### <a name="create-docker-host-with-azure-cli-20"></a>使用 Azure CLI 2.0 建立 Docker 主機
最新安裝 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。

首先，使用 [az group create](/cli/azure/group#create) 建立 Docker 環境的資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *uswest*位置：

```azurecli
az group create --name myResourceGroup --location westus
```

接下來，部署具有 VM [az 群組部署建立](/cli/azure/group/deployment#create)包含 hello Azure Docker VM 擴充功能，從[GitHub 上的此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)。 針對 newStorageAccountName、adminUsername、adminPassword 和 dnsNameForPublicIP 提供您自己的值：

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

花幾分鐘，讓 hello 部署 toofinish。 在 hello 部署完成時，[移動 toonext 步驟](#verify-that-compose-is-installed)tooSSH tooyour VM。 

（選擇性） tooinstead 傳回控制 toohello 提示與 hello 可讓的部署於 hello 背景繼續執行新增 hello `--no-wait` toohello 命令的前面加上旗標。 此程序可讓您 tooperform hello CLI 時在幾分鐘後會繼續進行 hello 部署中的其他工作。 然後，您可以檢視與 hello Docker 主機狀態的詳細[az vm 顯示](/cli/azure/vm#show)。 hello 下列範例會檢查 hello 狀態 hello 名為 VM *myDockerVM* （hello hello 範本中的預設名稱-不要變更這個名稱） 在 hello 資源群組中名為*myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

此命令會傳回當*Succeeded*hello 部署已完成，您可以在 hello 步驟之後的 SSH toohello VM。


## <a name="verify-that-compose-is-installed"></a>確認已安裝 Compose
在 hello 部署完成時，SSH tooyour 新 Docker 主機使用 hello DNS 名稱提供您在部署期間。 您可以使用`az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`tooview 詳細資料，您的 VM，包括 hello DNS 名稱。

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

撰寫的 toocheck 被安裝在 hello VM，執行下列命令的 hello:

```bash
docker-compose --version
```

您會看到類似的輸出太*docker 撰寫 1.6.2、 組建 4d 72027*。

> [!TIP]
> 如果您使用另一個方法 toocreate Docker 主機，而需要的 tooinstall 撰寫您自己，請參閱 hello[撰寫文件](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md)。


## <a name="create-a-docker-composeyml-configuration-file"></a>建立 docker-compose.yml 組態檔
接下來您建立`docker-compose.yml`不只是文字組態檔，toodefine hello Docker 容器 toorun hello VM 上的檔案。 hello 檔案指定 hello 映像 toorun 上每個容器 （或可能是來自 Dockerfile），必要的環境變數和相依性、 連接埠和 hello 容器之間的連結。 如需有關 yml 檔案語法的詳細資料，請參閱 [Compose file reference (Compose 檔案參考)](https://docs.docker.com/compose/compose-file/)。

建立 hello *docker compose.yml*檔案，如下所示：

```bash
touch docker-compose.yml
```

使用您慣用的文字編輯器 tooadd toohello 的一些資料檔案。 hello 下列範例會使用 hello *vi*編輯器：

```bash
vi docker-compose.yml
```

下列範例文字檔案到貼上 hello。 這種設定使用映像從 hello [DockerHub 登錄](https://registry.hub.docker.com/_/wordpress/)tooinstall WordPress （hello 開放原始碼部落格和內容管理系統） 和連結的後端 MariaDB SQL 資料庫。 輸入您自已的 MYSQL_ROOT_PASSWORD，如下所示：

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a>Hello 容器開頭撰寫
在 hello 相同目錄做為您*docker compose.yml*檔案中，執行下列命令的 hello (根據您的環境，您可能需要 toorun`docker-compose`使用`sudo`):

```bash
docker-compose up -d
```

此命令會啟動 hello Docker 容器中指定*docker compose.yml*。 花一分鐘，或兩個進行此步驟 toocomplete。 您會看到下列範例的輸出類似 toohello:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> 要確定 toouse hello **-d**啟動選項，使 hello 容器連續執行 hello 背景。


hello 容器已啟動的 tooverify 類型`docker-compose ps`。 您應該會看到如下的內容：

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

您現在可以連接 tooWordPress 直接在 hello 連接埠 80 上的 VM 上。 開啟網頁瀏覽器並輸入您 VM hello DNS 名稱 (例如`http://mypublicdns.westus.cloudapp.azure.com`)。 您現在應該會看到的 hello WordPress 開始畫面上，您會完成 hello 安裝，並開始使用 hello 應用程式。

![WordPress 起始畫面][wordpress_start]

## <a name="next-steps"></a>後續步驟
* 移 toohello [Docker VM 延伸模組使用者指南](https://github.com/Azure/azure-docker-extension/blob/master/README.md)更多選項 tooconfigure Docker 和 Docker VM 中的撰寫。 例如，其中一個選項是 tooput hello 撰寫 yml 檔案 (轉換後 tooJSON) 直接在 hello hello Docker VM 擴充功能組態。
* 簽出 hello[撰寫命令列參照](http://docs.docker.com/compose/reference/)和[使用者指南](http://docs.docker.com/compose/)建置及部署多個容器應用程式的相關範例。
* 使用 Azure 資源管理員範本，或是您自己或其中一個由 hello[社群](https://azure.microsoft.com/documentation/templates/)，toodeploy Docker 和應用程式與 Azure VM 與撰寫設定。 例如，hello[部署使用 Docker WordPress 部落格](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql)範本使用 Docker，並撰寫 tooquickly 使用 MySQL 後端 Ubuntu 虛擬機器上部署 WordPress。
* 嘗試整合 Docker Compose 與 Docker Swarm 叢集。 如需案例，請參閱[搭配使用 Compose 與 Swarm (英文)](https://docs.docker.com/compose/swarm/)。

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
