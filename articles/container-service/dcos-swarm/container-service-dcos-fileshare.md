---
title: "aaaFile 共用 Azure DC/OS 叢集 |Microsoft 文件"
description: "建立並掛接檔案共用 tooa DC/OS 中的叢集 Azure 容器服務"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: "Docker, Containers, Micro-services, Mesos, Azure, FileShare, cifs, 容器, 微服務"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>建立並掛接檔案共用 tooa DC/OS 叢集
本教學課程會詳細說明如何 toocreate 檔案共用在 Azure 中，並將其裝載每個代理程式與主機 hello DC/OS 叢集。 設定檔案共用可讓您更輕鬆 tooshare 檔案跨例如設定、 存取、 記錄檔，以及多個叢集。 在此教學課程中，會完成下列工作的 hello:

> [!div class="checklist"]
> * 建立 Azure 儲存體帳戶
> * 建立檔案共用
> * 掛接 hello hello DC/OS 叢集中的共用

您必須在本教學課程步驟的叢集 toocomplete hello ACS DC/OS。 如有需要，[此指令碼範例](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)可為您建立一個叢集。

本教學課程需要 hello Azure CLI 版本 2.0.4 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>在 Microsoft Azure 上建立檔案共用

之前使用 Azure 檔案共用與 DC/OS ACS 叢集，您必須建立 hello 儲存體帳戶和檔案共用。 執行下列指令碼 toocreate hello 存放區和檔案共用的 hello。 更新從您的環境 thoes hello 參數。

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a>裝載在叢集中的 hello 共用

接下來，hello 檔案共用需要 toobe 裝載在叢集內每個虛擬機器上。 這項工作已完成使用 hello cifs 工具/通訊協定。 hello 掛上操作可以手動方式完成，或針對 hello 叢集中的每個節點執行的指令碼的 hello 叢集中，每個節點上。

在此範例中，執行兩個指令碼、 一 toomount hello Azure 檔案共用，以及第二個 toorun 此指令碼 hello DC/OS 叢集的每個節點上。

首先，需要 hello Azure 儲存體帳戶名稱和存取金鑰。 執行下列命令 tooget hello 這項資訊。 請將每一個記下，稍後步驟中將會使用這些值。

儲存體帳戶名稱︰

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

儲存體帳戶存取金鑰︰

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

接下來，取得 hello hello 主要 DC/OS，並將它儲存在變數中的 FQDN。

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

複製您的私用金鑰 toohello 主要節點。 此索引鍵是所需的 toocreate ssh 連線與 hello 叢集中的所有節點。 如果建立 hello 叢集時使用非預設值，請更新 hello 使用者名稱。 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

建立 SSH 連線與 hello 主要 （或 hello 第一個主要） 的 DC/作業系統為基礎的叢集。 如果建立 hello 叢集時使用非預設值，請更新 hello 使用者名稱。

```azurecli-interactive
ssh azureuser@$FQDN
```

建立名為**cifsMount.sh**，並複製 hello 遵循到其中的內容。 

此指令碼是使用的 toomount hello Azure 檔案共用。 更新 hello`STORAGE_ACCT_NAME`和`ACCESS_KEY`稍早收集到的 hello 資訊的變數。

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
建立第二個名為**getNodesRunScript.sh**並複製 hello 遵循到 hello 檔案的內容。 

此指令碼會探索所有叢集節點，然後再執行 hello **cifsMount.sh**上每個指令碼 toomount hello 檔案共用。

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

Hello 叢集的所有節點上執行 hello 指令碼 toomount hello Azure 檔案共用。

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

hello 檔案共用現在是可存取`/mnt/share/dcosshare`hello 叢集的每個節點上。

## <a name="next-steps"></a>後續步驟

在本教學課程 Azure 檔案共用已提出可用 tooa DC/OS 叢集使用 hello 步驟：

> [!div class="checklist"]
> * 建立 Azure 儲存體帳戶
> * 建立檔案共用
> * 掛接 hello hello DC/OS 叢集中的共用

前進 toohello 下一個教學課程的 toolearn 有關在 Azure 中的 DC/OS 與整合 Azure 容器登錄中。  

> [!div class="nextstepaction"]
> [負載平衡應用程式](container-service-dcos-acr.md)