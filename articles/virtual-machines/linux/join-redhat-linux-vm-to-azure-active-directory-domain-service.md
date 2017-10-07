---
title: "aaaJoin RedHat Linux VM tooan Azure Active Directory DS |Microsoft 文件"
description: "如何 toojoin 現有 RedHat Enterprise Linux 7 VM tooan Azure Active Directory 網域服務。"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>加入 RedHat Linux VM tooan Azure Active Directory 網域服務

本文章將示範如何 toojoin Red Hat Enterprise Linux (RHEL) 7 虛擬機器 tooan Azure Active Directory 網域服務 (AADDS) 管理網域。  hello 需求如下：

- [一個 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)

- [SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md)

- [Azure Active Directory Domain Services DC](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>快速命令

_將任何範例換成您自己的設定。_

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>切換 hello azure cli tooclassic 部署模式

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>搜尋 RHEL 版本和映像

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>建立 Redhat Linux VM

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a>SSH toohello VM

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>更新 YUM 套件

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>安裝需要的套件

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

現在，hello Linux 虛擬機器上安裝所需的 hello 封裝，hello 下一項工作就會是 toojoin hello 虛擬機器 toohello 受管理的網域。

### <a name="discover-hello-aad-domain-services-managed-domain"></a>探索 hello AAD 網域服務受管理的網域

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>初始化 kerberos

請確認您指定隸屬 toohello ' AAD DC Administrators' 群組的使用者身分。 只有這些使用者可以加入電腦 toohello 受管理的網域。

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>加入 hello 機器 toohello 網域

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>請確認 hello 電腦聯結的 toohello 網域

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>後續步驟

* [適用於 Azure 中隨選 Red Hat Enterprise Linux VM 的 Red Hat Update Infrastructure (RHUI)](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [為 Azure Resource Manager 中的虛擬機器設定金鑰保存庫](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [部署及管理虛擬機器使用的 Azure 資源管理員範本和 hello Azure CLI](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
