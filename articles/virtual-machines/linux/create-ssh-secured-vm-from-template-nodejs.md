---
title: "aaaCreate Linux VM，使用 Azure 的範本與 Azure CLI 1.0 |Microsoft 文件"
description: "使用 Azure CLI 1.0 hello 和 Azure Resource Manager 範本的 Azure 上建立 Linux VM。"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>如何使用 Linux VM 的 toocreate hello Azure CLI 1.0 Azure Resource Manager 範本
本文章將示範如何 tooquickly 部署 Linux 虛擬機器使用 Azure CLI 1.0 hello 和 Azure Resource Manager 範本。 hello 文章需要：

* 一個 Azure 帳戶 ([取得免費試用帳戶](https://azure.microsoft.com/pricing/free-trial/))。
* hello [Azure CLI 1.0](../../cli-install-nodejs.md)登入的`azure login`。
* hello Azure CLI*必須在*Azure Resource Manager 模式`azure config mode arm`。

您可以使用 hello，以快速部署 Linux VM 範本[Azure 入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#quick-command-summary) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -hello 資源管理部署模型我們下一個層代 CLI

## <a name="quick-command-summary"></a>快速命令摘要
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說
範本可讓您 toocreate Vm 在 Azure 上設定的 toocustomize 期間 hello 啟動、 設定，例如使用者名稱和主機名稱。 在本文中，我們推出的 Azure 範本會利用 Ubuntu VM 以及連接埠 22 對 SSH 開放的網路安全性群組 (NSG)。

Azure Resource Manager 範本是 JSON 檔案，可用於進行簡單的一次性工作 (如本文中的啟動 Ubuntu VM)。  Azure 範本也可以使用的 tooconstruct 複雜 Azure 的組態的整個環境，例如測試、 開發、 或實際執行部署堆疊。

## <a name="create-hello-linux-vm"></a>建立 hello Linux VM
hello 下列程式碼範例顯示如何 toocall `azure group create` toocreate 資源群組和 SSH 保護 Linux VM，在 hello 部署相同的時間使用[此 Azure Resource Manager 範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json)。 請記住，您必須是唯一的 tooyour 環境的 toouse 名稱的範例中。 這個範例會使用*myResourceGroup*與 hello 資源群組名稱，和*myVM*做為 hello VM 名稱。

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

hello 輸出應該看起來像下列輸出區塊的 hello:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

該範例部署 VM，使用 hello`--template-uri`參數。  您也可以下載或建立在本機的範本及傳送嗨範本使用 hello`--template-file`使用路徑 toohello 範本檔做為引數的參數。 hello Azure CLI 會提示您輸入 hello 範本所需的 hello 參數。

## <a name="next-steps"></a>後續步驟
搜尋 hello[範本組件庫](https://azure.microsoft.com/documentation/templates/)toodiscover 哪些應用程式架構 toodeploy 下一步。

