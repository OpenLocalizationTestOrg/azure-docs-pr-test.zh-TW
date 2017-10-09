---
title: "aaaUse Ansible toocreate Azure 中的基本 Linux VM |Microsoft 文件"
description: "深入了解如何 toouse Ansible toocreate 和管理 Azure 中的基本 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>使用 Ansible 在 Azure 中建立基本虛擬機器
Ansible 可讓您 tooautomate hello 部署和設定資源在您的環境中。 您可以在 Azure 中虛擬機器 (Vm) 使用 Ansible toomanage、 hello 相同，如同任何其他資源。 本文章將示範如何 toocreate 具有 Ansible 的基本 VM。 您也可以了解如何太[建立完成在 VM 環境使用 Ansible](ansible-create-complete-vm.md)。


## <a name="prerequisites"></a>必要條件
toomanage Azure Ansible 資源，您需要遵循的 hello:

- Ansible 和 hello Azure Python SDK 模組安裝在主機系統上。
    - 在 [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts)、[CentOS 7.3](ansible-install-configure.md#centos-73) 和 [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2) 上安裝 Ansible
- Azure 認證和設定 Ansible toouse 它們。
    - [建立 Azure 認證和設定 Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI 2.0.4 版或更新版本。 執行`az --version`toofind hello 版本。 
    - 如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 您也可以在瀏覽器中使用 [Cloud Shell](/azure/cloud-shell/quickstart)。


## <a name="create-supporting-azure-resources"></a>建立支援的 Azure 資源
在此範例中，我們會建立一個 Runbook 來將 VM 部署到現有的基礎結構中。 首先，使用 [az group create](/cli/azure/vm#create) 建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置：

```azurecli
az group create --name myResourceGroup --location eastus
```

使用 [az network vnet create](/cli/azure/network/vnet#create) 為您的 VM 建立虛擬網路。 hello 下列範例會建立虛擬網路，名為*myVnet*和名為的子網路*mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>建立及執行 Ansible 腳本
建立名為 Ansible 腳本**azure_create_vm.yml**和 hello 貼上下列內容。 此範例會建立單一 VM 並設定 SSH 認證。 輸入您自己的公開金鑰資料在 hello *key_data*配對，如下所示：

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

toocreate hello VM 與 Ansible，執行 hello 腳本，如下所示：

```bash
ansible-playbook azure_create_vm.yml
```

hello 輸出看起來類似下列範例會顯示 hello 已成功建立 VM 的 toohello:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>後續步驟
此範例會在現有的資源群組中建立 VM，並已部署虛擬網路。 如需更詳細範例 toouse Ansible toocreate 支援資源，例如虛擬網路和網路安全性群組規則，請參閱[建立完成在 VM 環境使用 Ansible](ansible-create-complete-vm.md)。
