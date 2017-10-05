---
title: "使用 cloud-init 自訂 Linux VM | Microsoft Docs"
description: "如何透過 Azure CLI 2.0 在建立期間使用 cloud-init 自訂 Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a>在建立期間使用 cloud-init 自訂 Linux VM
本文會示範如何透過 Azure CLI 2.0 製作 cloud-init 指令碼來設定主機名稱、更新已安裝的封裝及管理使用者帳戶。 當您從 Azure CLI 建立虛擬機器 (VM) 時，會呼叫 cloud-init 指令碼。 如需更深入的安裝應用程式、撰寫組態檔，以及插入 Key Vault 金鑰的概觀，請參閱[本教學課程 (英文)](tutorial-automate-vm-deployment.md)。 您也可以使用 [Azure CLI 1.0](using-cloud-init-nodejs.md) 來執行這些步驟。

## <a name="quick-commands"></a>快速命令
建立一個設定主機名稱、更新所有封裝、並將 sudo 使用者新增至 Linux 的 cloud-init.txt 指令碼。

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

使用 [az group create](/cli/azure/group#create) 來建立資源群組以在其中啟動 VM。 下列範例會建立名為 myResourceGroup 的資源群組：

```azurecli
az group create --name myResourceGroup --location eastus
```

透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM，並使用 cloud-init 在以 `--custom-data` 參數開機期間進行設定。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說
啟動新的 Linux VM 時，Linux VM 會是標準模式，沒有自訂或符合您需求的選項。 [Cloud-init](https://cloudinit.readthedocs.org) 第一次啟動時，會是在 Linux VM 中插入指令碼或組態設定的標準方法。

Azure 有許多不同的方法可在 Linux VM 部署或開機時進行變更。

* 使用 cloud-init 插入指令碼。
* 使用 Azure [VMAccess 延伸模組](using-vmaccess-extension.md)插入指令碼。
* 使用 cloud-init 的 Azure 範本。
* 使用 [CustomScriptExtention](extensions-customscript.md)的 Azure 範本。

若開機後隨時要插入指令碼︰

* 直接執行命令的 SSH
* 使用 Azure [VMAccess 延伸模組](using-vmaccess-extension.md)，以命令方式或在 Azure 範本中插入指令碼
* 組態管理工具，例如 Ansible、Salt、Chef 及 Puppet。

> [!NOTE]
> VMAccess 延伸模組會採用根身分，以及與使用 SSH 時的相同方式執行指令碼。 不過，使用 VM 延伸模組可視您的案例啟用數個 Azure 提供的實用功能。

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Cloud-init 在 Azure VM quick-create 映像別名上的可用性︰
| Alias | 發佈者 | 提供項目 | SKU | 版本 | Cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |最新 |no |
| CoreOS |CoreOS |CoreOS |Stable |最新 |yes |
| Debian |credativ |Debian |8 |最新 |no |
| openSUSE |SUSE |openSUSE |13.2 |最新 |no |
| RHEL |Redhat |RHEL |7.2 |最新 |no |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |最新 |yes |

我們正在與合作夥伴合作，以期在他們提供給 Azure 的映像中包含和使用 cloud-init。

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a>將 cloud-init 指令碼新增至使用 Azure CLI 建立 VM 的作業中
在 Azure 中建立 VM 時，若要啟動 cloud-init 指令碼，請使用 Azure CLI `--custom-data` 參數來指定 cloud-init 檔案。

使用 [az group create](/cli/azure/group#create) 來建立資源群組以在其中啟動 VM。 下列範例會建立名為 myResourceGroup 的資源群組：

```azurecli
az group create --name myResourceGroup --location eastus
```

透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM 並使用 cloud-init 在開機期間進行設定。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a>建立 cloud-init 指令碼以設定 Linux VM 的主機名稱
對任何 Linux VM 而言，其中一個最簡單且最重要的設定就是主機名稱。 使用 cloud-init 和這個指令碼就可以輕鬆地設定這個項目。  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>名為 `cloud_config_hostname.txt`的範例 cloud-init 指令碼。
```yaml
#cloud-config
hostname: myservername
```

在 VM 首次啟動期間，這個 cloud-init 指令碼會將主機名稱設定為 myservername。 透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM 並使用 cloud-init 在開機期間進行設定。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

登入並驗證新 VM 的主機名稱。

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>建立 cloud-init 指令碼
基於安全性，您希望您的 Ubuntu VM 能在第一次開機時進行更新。 我們可以使用 cloud-init 和下列指令碼執行這個作業，視您使用的 Linux 散發套件而定。

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a>適用於 Debian 系列的範例 cloud-init 指令碼 `cloud_config_apt_upgrade.txt`
```yaml
#cloud-config
apt_upgrade: true
```

在 Linux 開機後，所有已安裝的封裝都會透過 apt-get 更新。 透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM 並使用 cloud-init 在開機期間進行設定。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

登入並驗證所有封裝是否皆已更新。

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a>建立 cloud-init 指令碼以將使用者新增至 Linux 中
針對任何新的 Linux VM，首要工作之一就是為您自己新增一位使用者，或是避免使用根身分。 SSH 金鑰是基於安全性和可用性的最佳作法，它們會隨此 cloud-init 指令碼新增至 ~/.ssh/authorized_keys 檔案。

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>適用於 Debian 系列的範例 cloud-init 指令碼 `cloud_config_add_users.txt`
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Linux 開機之後，所有列出的使用者就會建立並加入 sudo 群組。 透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM 並使用 cloud-init 在開機期間進行設定。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

登入並驗證新建立的使用者。

```bash
ssh myVM
cat /etc/group
```

輸出

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>後續步驟
Cloud-init 已成為在開機時修改 Linux VM 的一種標準方式。 Azure 也有 VM 延伸模組，可讓您在開機或執行時修改您的 LinuxVM。 例如，當 VM 執行時，您可以使用 Azure VMAccessExtension 來重設 SSH 或使用者資訊。 使用 cloud-init，您必須重新開機才能重設密碼。

[有關虛擬機器擴充功能和功能](extensions-features.md)

[管理使用者、SSH，並使用 VMAccess 擴充功能檢查或修復 Azure Linux VM 上的磁碟](using-vmaccess-extension.md)