---
title: "aaaDifferent 方式 toocreate Azure 中的 Linux VM |Microsoft Azure"
description: "了解 hello 不同的方式 toocreate Azure，包括連結 tootools 和教學課程，每個方法上的 Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>不同的方式 toocreate Linux VM
您擁有 hello 彈性 Azure toocreate 中使用工具和工作流程的舒適 tooyou 在 Linux 虛擬機器 (VM)。 本文摘要說明這些差異和建立 Linux Vm，包括 hello Azure CLI 2.0 的範例。 您也可以檢視建立選項包括 hello [Azure CLI 1.0](creation-choices-nodejs.md)。

hello [Azure CLI 2.0](/cli/azure/install-az-cli2)可跨平台透過 npm 封裝、 distro 提供的封裝或 Docker 容器。 安裝您的環境的 hello 最適合組建並 tooan Azure 帳戶使用登入[az 登入](/cli/azure/#login)

* [建立 Linux VM 以 hello Azure CLI 2.0](quick-create-cli.md)
  
  * 使用名為 myResourceGroup 的 [az group create](/cli/azure/group#create) 來建立資源群組： 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * 建立與 VM [az vm 建立](/cli/azure/vm#create)名為*myVM*使用最新 hello *UbuntuLTS*映像，如果它們尚不存在中產生 SSH 金鑰*~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [使用 Azure 範本建立 Linux VM](create-ssh-secured-vm-from-template.md)
  
  * hello 下列範例會使用[az 群組部署建立](/cli/azure/group/deployment#create)toocreate 將 VM 從 GitHub 上存放的範本：
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [建立 Linux VM，並使用 cloud-init 進行自訂](tutorial-automate-vm-deployment.md)

* [在多個 Linux VM 上建立負載平衡和高可用性的應用程式](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Azure 入口網站
hello [Azure 入口網站](https://portal.azure.com)可讓您 tooquickly 建立 VM，因為沒有任何 tooinstall 您系統上的。 使用 hello Azure 入口網站 toocreate hello VM:

* [建立 Linux VM 使用 hello Azure 入口網站](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>作業系統和映像選項
在建立 VM 時，您可以選擇根據 hello 想 toorun 作業系統映像。 Azure 與其合作夥伴提供許多映像，其中有些包括已預先安裝的應用程式和工具。 或者，您也可以上傳自己的映像的其中一個 (請參閱[hello 下列區段](#use-your-own-image))。

### <a name="azure-images"></a>Azure 映像
使用 hello [az vm 映像](/cli/azure/vm/image)命令 toosee 可用的發行者、 distro 版本和組建。

列出可用的發佈者：

```azurecli
az vm image list-publishers --location eastus
```

列出特定發佈者的可用產品 (提供項目)︰

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

清單特定提供項目的可用 SKU (散發版本)︰

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

列出特定版本的所有可用映像︰

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

瀏覽和使用可用的映像的詳細範例，請參閱[瀏覽並選取 Azure 虛擬機器映像以 hello Azure CLI](cli-ps-findimage.md)。

hello [az vm 建立](/cli/azure/vm#create)命令有別名，您可以使用 tooquickly 存取 hello 較常見的散發版本，其最新版本。 使用別名，通常會快於每次當您建立的 VM 指定 hello 發行者、 方案、 SKU 和版本：

| Alias | 發佈者 | 提供項目 | SKU | 版本 |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |最新 |
| CoreOS |CoreOS |CoreOS |Stable |最新 |
| Debian |credativ |Debian |8 |最新 |
| openSUSE |SUSE |openSUSE |13.2 |最新 |
| RHEL |Redhat |RHEL |7.2 |最新 |
| SLES |SLES |SLES |12-SP1 |最新 |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |最新 |

### <a name="use-your-own-image"></a>使用您自己的映像
如果您需要特定的自訂，可以擷取該 VM，根據現有的 Azure VM 使用映像。 也可以上傳在內部部署建立的映像。 如需有關支援的散發版本以及如何 toouse 自己的映像，請參閱下列文章 hello:

* [Azure 背書的散發套件](endorsed-distros.md)
* [非背書散發套件的資訊](create-upload-generic.md)
* [如何從現有的 Azure VM 映像 toocreate](tutorial-custom-images.md)。
  
  * 快速入門範例命令 toocreate 從現有的 Azure VM 映像：
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>後續步驟
* 建立 Linux VM 以 hello [CLI](quick-create-cli.md)，從 hello[入口網站](quick-create-portal.md)，或使用[Azure Resource Manager 範本](../windows/cli-deploy-templates.md)。
* 建立 Linux VM 之後，[深入了解 Azure 磁碟與儲存體](tutorial-manage-disks.md)。
* 快速步驟太[重設密碼或 SSH 金鑰，以及管理使用者](using-vmaccess-extension.md)。
