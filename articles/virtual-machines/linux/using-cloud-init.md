---
title: "aaaUse 雲端 init toocustomize Linux VM |Microsoft 文件"
description: "Linux VM 的期間所建立的 toouse 雲端 init toocustomize hello Azure CLI 2.0 的方式"
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
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a>在建立期間使用雲端 init toocustomize Linux VM
本文章將示範 toomake 雲端初始化指令碼 tooset hello 主機名稱、 更新已安裝的套件，及管理使用者帳戶，以 hello Azure CLI 2.0 的方式。 當您從 Azure CLI 建立虛擬機器 (VM) 時，會呼叫 hello 雲端初始化指令碼。 如需更深入的安裝應用程式、撰寫組態檔，以及插入 Key Vault 金鑰的概觀，請參閱[本教學課程 (英文)](tutorial-automate-vm-deployment.md)。 您也可以執行下列步驟以 hello [Azure CLI 1.0](using-cloud-init-nodejs.md)。

## <a name="quick-commands"></a>快速命令
建立雲端 init.txt 指令碼設定 hello 主機名稱，更新所有的封裝，並將 sudo 使用者 tooLinux。

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

建立資源群組 toolaunch Vm 到[az 群組建立](/cli/azure/group#create)。 hello 下列範例會建立名為 「 hello 資源群組*myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它以 hello 開機期間`--custom-data`參數。

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
啟動新的 Linux VM 時，Linux VM 會是標準模式，沒有自訂或符合您需求的選項。 [雲端 init](https://cloudinit.readthedocs.org)開機 hello 註冊第一次該 Linux VM 的指令碼或組態設定是標準方式 tooinject。

在 Azure 上，有幾個不同的方式 toomake 變更到 Linux VM 上的以在部署或啟動。

* 使用 cloud-init 插入指令碼。
* 插入指令碼使用 hello Azure [VMAccess 擴充功能](using-vmaccess-extension.md)。
* 使用 cloud-init 的 Azure 範本。
* 使用 [CustomScriptExtention](extensions-customscript.md)的 Azure 範本。

開機後隨時 tooinject 指令碼：

* 直接 SSH toorun 命令
* 插入指令碼使用 hello Azure [VMAccess 擴充功能](using-vmaccess-extension.md)，以命令方式或在 Azure 範本
* 組態管理工具，例如 Ansible、Salt、Chef 及 Puppet。

> [!NOTE]
> VMAccess 擴充功能執行指令碼為根 hello 中相同方式使用 SSH 可以。 不過，使用 hello VM 延伸模組可讓數個功能非常適合您的案例而定，Azure 優惠。

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Cloud-init 在 Azure VM quick-create 映像別名上的可用性︰
| Alias | 發佈者 | 提供項目 | SKU | 版本 | Cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |最新 |no |
| CoreOS |CoreOS |CoreOS |Stable |最新 |yes |
| Debian |credativ |Debian |8 |最新 |no |
| openSUSE |SUSE |openSUSE |13.2 |最新 |no |
| RHEL |Redhat |RHEL |7.2 |最新 |no |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |最新 |yes |

我們會使用我們合作夥伴 tooget 雲端 for-init 包含以及他們提供 tooAzure hello 映像中的工作。

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>加入雲端初始化指令碼 toohello 建立 VM 以 hello Azure CLI
toolaunch 雲端初始化指令碼在 Azure 中建立 VM 時指定 hello 雲端初始化檔案，使用 Azure CLI hello`--custom-data`切換。

建立資源群組 toolaunch Vm 到[az 群組建立](/cli/azure/group#create)。 hello 下列範例會建立名為 「 hello 資源群組*myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它在開機期間。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>建立 Linux VM 雲端初始化指令碼 tooset hello 主機名稱
其中一個最簡單的 hello 和任何 Linux VM 的最重要的設定是 hello 主機名稱。 使用 cloud-init 和這個指令碼就可以輕鬆地設定這個項目。  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>名為 `cloud_config_hostname.txt`的範例 cloud-init 指令碼。
```yaml
#cloud-config
hostname: myservername
```

在 hello 的 hello VM 的初始啟動，此雲端初始化指令碼設定為 hello 主機名稱太*myservername*。 建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它在開機期間。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

登入，並確認 hello hostname hello 的新 VM。

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>建立 cloud-init 指令碼
為了安全性，您會想 hello 第一次開機程式 Ubuntu VM tooupdate。 使用雲端 init 我們可以執行以 hello 遵循指令碼，根據您使用的 hello Linux 散發套件。

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>範例雲端初始化指令碼`cloud_config_apt_upgrade.txt`hello Debian 系列
```yaml
#cloud-config
apt_upgrade: true
```

Linux 開機之後，所有的 hello 安裝套件會更新透過**apt get**。 建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它在開機期間。

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
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a>建立雲端初始化指令碼 tooadd 使用者 tooLinux
Hello 任何新的 Linux VM 上的首要工作之一是 tooadd 使用者提供您自己或 tooavoid 使用*根*。 SSH 金鑰是針對安全性和可用性的最佳作法，並且會新增 toohello *~/.ssh/authorized_keys*這個雲端初始化指令碼檔案。

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

Linux 開機之後，所有的 hello 列出使用者都是建立和加入 toohello sudo 群組。 建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它在開機期間。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

登入，並確認 hello 新建立的使用者。

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
雲端 init 變得一標準方式 toomodify Linux VM 上開機。 Azure 也有 VM 擴充功能，可讓您 toomodify 您 LinuxVM 開機或執行時。 例如，您可以使用 hello Azure VMAccessExtension tooreset SSH 或使用者資訊 hello VM 正在執行時。 與雲端初始化，您將需要重新開機 tooreset hello 密碼。

[有關虛擬機器擴充功能和功能](extensions-features.md)

[管理使用者、 SSH 和核取，或使用 Azure Linux Vm 上的修復磁片 hello VMAccess 擴充功能](using-vmaccess-extension.md)
