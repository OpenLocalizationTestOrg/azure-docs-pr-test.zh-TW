---
title: "aaaReset 存取 tooan Azure Linux VM |Microsoft 文件"
description: "如何 toomanage 使用者及重設 Linux Vm 使用的存取 hello VMAccess 擴充功能和 hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>管理使用者、 SSH 和核取或修復磁碟上使用 Linux Vm 以 hello Azure CLI 2.0 hello VMAccess 擴充功能
hello Linux VM 上的磁碟會顯示錯誤。 由於某種原因而 hello 根密碼重設 Linux VM，或不慎刪除您的 SSH 私密金鑰。 如果，是發生在 hello 天數 hello 資料中心，您會需要那里 toodrive，然後開啟 hello KVM tooget hello 伺服器主控台。 將視為該 KVM 切換器，可讓您 tooaccess hello 主控台 tooreset 存取 tooLinux 或執行磁碟層級維護 hello Azure VMAccess 擴充功能。

本文章將示範如何 toouse hello Azure VMAccess 擴充功能 toocheck 或修復磁碟、 重設使用者的存取權、 管理使用者帳戶，或重設 hello Linux 上的 SSH 組態。 您也可以執行下列步驟以 hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。


## <a name="ways-toouse-hello-vmaccess-extension"></a>方式 toouse hello VMAccess 擴充功能
有兩種方式，您可以在 Linux Vm 上使用 hello VMAccess 擴充功能：

* 使用 Azure CLI 2.0 hello 和所需的 hello 參數。
* [使用未經處理的 JSON 檔案的 hello VMAccess 擴充功能的程序](#use-json-files-and-the-vmaccess-extension)，接著處理。

下列範例使用的 hello [az vm 使用者](/cli/azure/vm/user)命令。 tooperform 這些步驟，您需要 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

## <a name="reset-ssh-key"></a>重設 SSH 金鑰
hello 下列範例會重設 hello 使用者 hello SSH 金鑰`azureuser`hello 名為 VM 上`myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>重設密碼
hello 下列範例會重設 hello hello 使用者密碼`azureuser`hello 名為 VM 上`myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>重新啟動 SSH
hello 下列範例會重新啟動 hello SSH 服務精靈和重設 hello 名為的 VM 上的 SSH 組態 toodefault 值`myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>建立使用者
hello 下列範例會建立名為使用者`myNewUser`hello 名為 VM 上的驗證使用 SSH 金鑰`myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>刪除使用者
hello 下列範例會刪除名為使用者`myNewUser`hello 名為 VM 上`myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>使用 JSON 檔案並 hello VMAccess 擴充功能
下列範例中的 hello 使用未經處理的 JSON 檔案。 使用[az vm 延伸模組集](/cli/azure/vm/extension#set)toothen 呼叫您的 JSON 檔案。 您也可以從 Azure 範本呼叫這些 JSON 檔案。 

### <a name="reset-user-access"></a>重設使用者存取
如果您遺失存取 tooroot Linux VM 上，您可以啟動 VMAccess 指令碼 tooreset 使用者的 SSH 金鑰或密碼。

tooreset hello SSH 公開金鑰的使用者，建立名為`reset_ssh_key.json`和加入的 hello 遵循格式設定。 取代您自己的值為 hello`username`和`ssh_key`參數：

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

執行與 hello VMAccess 指令碼：

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

tooreset 使用者密碼，建立名為`reset_user_password.json`和加入的 hello 遵循格式設定。 取代您自己的值為 hello`username`和`password`參數：

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

執行與 hello VMAccess 指令碼：

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>重新啟動 SSH
toorestart hello SSH 服務精靈和重設 hello SSH 組態 toodefault 值，請建立名為`reset_sshd.json`。 新增下列內容的 hello:

```json
{
  "reset_ssh": true
}
```

執行與 hello VMAccess 指令碼：

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>管理使用者

toocreate 進行驗證，使用 SSH 金鑰的使用者建立名為`create_new_user.json`和加入的 hello 遵循格式設定。 取代您自己的值為 hello`username`和`ssh_key`參數：

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

執行與 hello VMAccess 指令碼：

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

toodelete 使用者時，建立名為`delete_user.json`並加入下列內容的 hello。 取代您自己的值為 hello`remove_user`參數：

```json
{
  "remove_user":"myNewUser"
}
```

執行與 hello VMAccess 指令碼：

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>檢查或修復 hello 磁碟
您也可以使用 VMAccess 檢查並修復您加入 toohello Linux VM 的磁碟。

toocheck，然後修復 hello 磁碟，建立名為`disk_check_repair.json`和加入的 hello 遵循格式設定。 取代您自己的值為 hello 名稱`repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

執行與 hello VMAccess 指令碼：

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>後續步驟
更新 Linux 使用 hello Azure VMAccess 擴充功能是在執行中的 Linux VM 上的一個方法 toomake 變更。 您也可以使用工具像是雲端 init 和 Azure 資源管理員範本 toomodify Linux VM 上開機。

[適用於 Linux 的虛擬機器擴充功能和功能](extensions-features.md)

[使用 Linux VM 擴充功能編寫 Azure Resource Manager 範本](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[在建立期間使用雲端 init toocustomize Linux VM](using-cloud-init.md)

