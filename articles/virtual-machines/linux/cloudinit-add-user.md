---
title: "使用 cloud-init 將使用者新增至 Azure 上的 Linux 虛擬機器 | Microsoft Docs"
description: "如何透過 Azure CLI 2.0 在建立期間使用 cloud-init 將使用者新增至 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 11/29/2017
ms.author: rclaus
ms.openlocfilehash: 728ffed27747cb298d5da312014a3c9e98b44f1e
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2017
---
# <a name="use-cloud-init-to-add-a-user-to-a-linux-vm-in-azure"></a>使用 cloud-init 將使用者新增至 Azure 上的 Linux 虛擬機器
本文會示範如何在 Azure 佈建期間，使用 [cloud-init](https://cloudinit.readthedocs.io) 在虛擬機器 (VM) 上或虛擬機器擴展集 (VMSS) 上新增使用者。 一旦 Azure 佈建資源，此 cloud-init 指令碼就會在初次開機時執行。 如需深入了解 cloud-init 如何以原生方式在 Azure 和支援的 Linux 散發版本中運作，請參閱 [cloud-init 概觀](using-cloud-init.md)。

## <a name="add-a-user-to-a-vm-with-cloud-init"></a>使用 cloud-init 將使用者新增至 VM
針對任何新的 Linux 虛擬機器，首要工作之一就是為您自己新增其他使用者，以避免使用「根」。 SSH 金鑰是提供安全性和可用性的最佳做法。 此 cloud-init 指令碼會將金鑰新增至 *~/.ssh/authorized_keys* 檔案。

若要將使用者新增至 Linux 虛擬機器，請在目前的殼層中建立名為 cloud_init_add_user.txt 的檔案，然後貼上下列設定。 針對此範例，請在 Cloud Shell 中 (而不是本機電腦上) 建立該檔案。 您可以使用任何您想要的編輯器。 輸入 `sensible-editor cloud_init_add_user.txt` 可建立檔案，並查看可用的編輯器清單。 建議首先選擇使用 **nano** 編輯器。 請確定已正確複製整個 cloud-init 檔案，特別是第一行。  您需要提供您自己的公開金鑰 (例如 ~/.ssh/id_rsa.pub 的內容)，以作為 `ssh-authorized-keys:` 的值 - 這裡已將其縮減以簡化範例。

```yaml
#cloud-config
users:
  - default
  - name: myadminuser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>
```
> [!NOTE] 
> #cloud-config 檔包含 `- default` 參數。 這會將使用者附加至佈建期間建立的現有管理使用者。 如果您建立的使用者不含 `- default` 參數 - 由 Azure 平台建立的自動產生管理使用者就會遭到覆寫。 

部署此映像前，您必須使用 [az group create](/cli/azure/group#create) 命令建立資源群組。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組。

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

現在，請使用 [az vm create](/cli/azure/vm#create) 建立 VM 並以 `--custom-data cloud_init_add_user.txt` 指定 cloud-init 檔案，如下所示：

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroup \
  --name centos74 \
  --image OpenLogic:CentOS:7-CI:latest \
  --custom-data cloud_init_add_user.txt \
  --generate-ssh-keys 
```

以 SSH 連線到顯示於由上述命令所產生之輸出中的 VM 公用 IP 位址。 輸入您自己的 **publicIpAddress**，如下所示︰

```bash
ssh <publicIpAddress>
```

若要確認已將您的使用者新增至 VM 與指定的群組，請檢視 */etc/group* 檔案的內容，如下所示：

```bash
cat /etc/group
```

下列範例輸出顯示來自 *cloud_init_add_user.txt* 檔案的使用者已新增至 VM 與適當的群組：

```bash
root:x:0:
<snip />
sudo:x:27:myadminuser
<snip />
myadminuser:x:1000:
```

## <a name="next-steps"></a>後續步驟
如需其他設定變更的 cloud-init 範例，請參閱下列文件：
 
- [將其他 Linux 使用者新增至虛擬機器](cloudinit-add-user.md)
- [執行封裝管理員以便在初次開機時更新現有的封裝](cloudinit-update-vm.md)
- [變更虛擬機器本機的主機名稱](cloudinit-update-vm-hostname.md) 
- [安裝應用程式封裝、更新設定檔及插入金鑰](tutorial-automate-vm-deployment.md)