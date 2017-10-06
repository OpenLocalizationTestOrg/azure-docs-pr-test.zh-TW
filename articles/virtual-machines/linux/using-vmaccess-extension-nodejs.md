---
title: "使用 Azure Linux Vm aaaReset 存取 hello VMAccess 擴充功能 |Microsoft 文件"
description: "重設使用 hello VMAccess 擴充功能的 Azure Linux Vm 上的存取。"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>管理使用者、 SSH 和核取，或使用 Azure Linux Vm 上的修復磁片以 hello Azure CLI 1.0 hello VMAccess 擴充功能
本文章將示範如何 toouse hello Azure VMAcesss Extension toocheck 或修復磁碟、 重設使用者的存取權、 管理使用者帳戶，或重設 Linux 上的 hello SSHD 設定。 hello 文章需要：

* 一個 Azure 帳戶 ([取得免費試用帳戶](https://azure.microsoft.com/pricing/free-trial/))。
* hello [Azure CLI](../../cli-install-nodejs.md)登入的`azure login`。
* hello Azure CLI*必須在*Azure Resource Manager 模式`azure config mode arm`。


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#quick-commands)– 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="quick-commands"></a>快速命令
有兩種方式 toouse VMAccess Linux Vm 上：

* 使用 Azure CLI 1.0 hello 和 hello 必要參數。
* 使用 VMAccess 處理的原始 JSON 檔案並採取行動。

Hello 快速命令區段，我們 toouse hello Azure CLI 1.0`azure vm reset-access`方法。 在 hello 下列命令範例中，會包含 「 範例 」 使用 hello 值從您自己的環境的 hello 值取代。

## <a name="create-a-resource-group-and-linux-vm"></a>建立資源群組和 Linux VM
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>建立 Debian VM
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a>重設根密碼
tooreset hello 根密碼：

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>SSH 金鑰重設
tooreset hello SSH 金鑰的非根使用者：

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>建立使用者
toocreate 使用者：

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>移除使用者
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>重設 SSHD
tooreset hello SSHD 組態：

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>詳細的逐步解說
### <a name="vmaccess-defined"></a>VMAccess 已定義︰
hello Linux VM 上的磁碟會顯示錯誤。 由於某種原因而 hello 根密碼重設 Linux VM，或不慎刪除您的 SSH 私密金鑰。 如果，是發生在 hello 天數 hello 資料中心，您會需要那里 toodrive，然後開啟 hello KVM tooget hello 伺服器主控台。 將視為該 KVM 切換器，可讓您 tooaccess hello 主控台 tooreset 存取 tooLinux 或執行磁碟層級維護 hello Azure VMAccess 擴充功能。

Hello 詳細的逐步解說中，我們 toouse hello 完整格式 VMAccess，會使用原始的 JSON 檔案。  從 Azure 範本也可以呼叫這些 VMAccess JSON 檔案。

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>使用 VMAccess toocheck 或修復 hello 磁碟上的 Linux VM
使用 VMAccess 可以執行、 fsck hello 磁碟，在 Linux VM 上執行。  您也可以使用 VMAccess 執行磁碟檢查和磁碟修復。

toocheck，然後按一下 修復 hello 磁碟使用這個 VMAccess 指令碼：

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

執行與 hello VMAccess 指令碼：

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>使用 VMAccess tooreset 使用者存取 tooLinux
如果您遺失存取 tooroot Linux VM 上，您可以啟動 VMAccess 指令碼 tooreset hello 根密碼。

tooreset hello 根密碼，使用此 VMAccess 指令碼：

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

執行與 hello VMAccess 指令碼：

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

tooreset hello SSH 金鑰的非根使用者，使用此 VMAccess 指令碼：

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

執行與 hello VMAccess 指令碼：

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>在 Linux 上使用 VMAccess toomanage 使用者帳戶
VMAccess 是可以是您沒有登入，並使用 sudo 或 hello 根帳號的 Linux VM 上使用的 toomanage 使用者的 Python 指令碼。

toocreate 使用者時，會使用此 VMAccess 指令碼：

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

執行與 hello VMAccess 指令碼：

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete 使用者時，會使用此 VMAccess 指令碼：

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

執行與 hello VMAccess 指令碼：

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>使用 VMAccess tooreset hello SSHD 組態
若要變更 toohello Linux Vm SSHD 設定及驗證 hello 變更之前關閉 hello SSH 連線，您可能會導致無法 SSH'ing 回。  VMAccess 可以是使用的 tooreset hello SSHD 組態後 tooa 已知的正確設定而不透過 SSH 登入。

tooreset hello SSHD 組態，請使用此 VMAccess 指令碼：

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

執行與 hello VMAccess 指令碼：

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>後續步驟
更新 Linux 使用 Azure VMAccess 擴充功能是在執行中的 Linux VM 上的一個方法 toomake 變更。  您也可以使用工具像是雲端 init 和 Azure 範本 toomodify Linux VM 上開機。

[有關虛擬機器擴充功能和功能](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[使用 Linux VM 擴充功能編寫 Azure Resource Manager 範本](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[在建立期間使用雲端 init toocustomize Linux VM](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

