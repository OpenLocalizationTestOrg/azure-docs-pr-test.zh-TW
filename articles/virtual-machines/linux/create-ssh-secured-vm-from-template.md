---
title: "從範本 aaaCreate Azure 中的 Linux VM |Microsoft 文件"
description: "如何 toouse 會 hello Azure CLI 2.0 toocreate Resource Manager 範本從 Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>如何 toocreate Linux 虛擬機器與 Azure 資源管理員範本
本文示範 tooquickly 部署 Linux 虛擬機器 (VM) 與 Azure 資源管理員範本 hello Azure CLI 2.0 的方式。 您也可以執行下列步驟以 hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md)。


## <a name="templates-overview"></a>範本概觀
Azure 資源管理員範本是 hello 基礎結構和 Azure 方案的組態中定義的 JSON 檔案。 透過範本，您可以在整個生命週期中重複部署方案，並確信您的資源會以一致的狀態部署。 toolearn 進一步了解 hello 格式 hello 範本和建構它，請參閱[建立第一個 Azure Resource Manager 範本](../../azure-resource-manager/resource-manager-create-first-template.md)。 tooview hello JSON 語法資源類型，請參閱[Azure Resource Manager 範本中定義的資源](/azure/templates/)。


## <a name="create-resource-group"></a>建立資源群組
Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 資源群組必須在虛擬機器之前建立。 hello 下列範例會建立名為的資源群組*myResourceGroupVM*在 hello *eastus*區域：

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine
hello 下列範例會建立將 VM 從[此 Azure Resource Manager 範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)與[az 群組部署建立](/cli/azure/group/deployment#create)。 提供您自己 SSH 公開金鑰，例如 hello 內容 hello 值*~/.ssh/id_rsa.pub*。 如果您需要 toocreate 的 SSH 金鑰組，請參閱[如何 toocreate 及使用 SSH 金鑰組適用於在 Azure 中的 Linux Vm](mac-create-ssh-keys.md)。

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

在此範例中，會指定存放在 GitHub 中的範本。 您也可以下載或建立範本及指定 hello 本機路徑以 hello 相同`--template-file`參數。

tooSSH tooyour VM，取得與 hello 公用 IP 位址[az 網路公用 ip 顯示](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

然後，您可以像平常一樣 SSH tooyour VM:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>後續步驟
在此範例中，您建立基本的 Linux VM。 對於多個資源管理員範本包含應用程式架構，或建立更複雜的環境，瀏覽 hello [Azure 快速入門範本圖庫](https://azure.microsoft.com/documentation/templates/)。
