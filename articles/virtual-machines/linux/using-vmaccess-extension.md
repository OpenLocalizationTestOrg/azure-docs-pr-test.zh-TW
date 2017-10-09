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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="207f7-103">管理使用者、 SSH 和核取或修復磁碟上使用 Linux Vm 以 hello Azure CLI 2.0 hello VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="207f7-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="207f7-104">hello Linux VM 上的磁碟會顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="207f7-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="207f7-105">由於某種原因而 hello 根密碼重設 Linux VM，或不慎刪除您的 SSH 私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="207f7-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="207f7-106">如果，是發生在 hello 天數 hello 資料中心，您會需要那里 toodrive，然後開啟 hello KVM tooget hello 伺服器主控台。</span><span class="sxs-lookup"><span data-stu-id="207f7-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="207f7-107">將視為該 KVM 切換器，可讓您 tooaccess hello 主控台 tooreset 存取 tooLinux 或執行磁碟層級維護 hello Azure VMAccess 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="207f7-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="207f7-108">本文章將示範如何 toouse hello Azure VMAccess 擴充功能 toocheck 或修復磁碟、 重設使用者的存取權、 管理使用者帳戶，或重設 hello Linux 上的 SSH 組態。</span><span class="sxs-lookup"><span data-stu-id="207f7-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="207f7-109">您也可以執行下列步驟以 hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="207f7-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="207f7-110">方式 toouse hello VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="207f7-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="207f7-111">有兩種方式，您可以在 Linux Vm 上使用 hello VMAccess 擴充功能：</span><span class="sxs-lookup"><span data-stu-id="207f7-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="207f7-112">使用 Azure CLI 2.0 hello 和所需的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="207f7-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="207f7-113">[使用未經處理的 JSON 檔案的 hello VMAccess 擴充功能的程序](#use-json-files-and-the-vmaccess-extension)，接著處理。</span><span class="sxs-lookup"><span data-stu-id="207f7-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="207f7-114">下列範例使用的 hello [az vm 使用者](/cli/azure/vm/user)命令。</span><span class="sxs-lookup"><span data-stu-id="207f7-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="207f7-115">tooperform 這些步驟，您需要 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="207f7-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="207f7-116">重設 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="207f7-116">Reset SSH key</span></span>
<span data-ttu-id="207f7-117">hello 下列範例會重設 hello 使用者 hello SSH 金鑰`azureuser`hello 名為 VM 上`myVM`:</span><span class="sxs-lookup"><span data-stu-id="207f7-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="207f7-118">重設密碼</span><span class="sxs-lookup"><span data-stu-id="207f7-118">Reset password</span></span>
<span data-ttu-id="207f7-119">hello 下列範例會重設 hello hello 使用者密碼`azureuser`hello 名為 VM 上`myVM`:</span><span class="sxs-lookup"><span data-stu-id="207f7-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="207f7-120">重新啟動 SSH</span><span class="sxs-lookup"><span data-stu-id="207f7-120">Restart SSH</span></span>
<span data-ttu-id="207f7-121">hello 下列範例會重新啟動 hello SSH 服務精靈和重設 hello 名為的 VM 上的 SSH 組態 toodefault 值`myVM`:</span><span class="sxs-lookup"><span data-stu-id="207f7-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="207f7-122">建立使用者</span><span class="sxs-lookup"><span data-stu-id="207f7-122">Create a user</span></span>
<span data-ttu-id="207f7-123">hello 下列範例會建立名為使用者`myNewUser`hello 名為 VM 上的驗證使用 SSH 金鑰`myVM`:</span><span class="sxs-lookup"><span data-stu-id="207f7-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="207f7-124">刪除使用者</span><span class="sxs-lookup"><span data-stu-id="207f7-124">Delete a user</span></span>
<span data-ttu-id="207f7-125">hello 下列範例會刪除名為使用者`myNewUser`hello 名為 VM 上`myVM`:</span><span class="sxs-lookup"><span data-stu-id="207f7-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="207f7-126">使用 JSON 檔案並 hello VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="207f7-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="207f7-127">下列範例中的 hello 使用未經處理的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="207f7-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="207f7-128">使用[az vm 延伸模組集](/cli/azure/vm/extension#set)toothen 呼叫您的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="207f7-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="207f7-129">您也可以從 Azure 範本呼叫這些 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="207f7-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="207f7-130">重設使用者存取</span><span class="sxs-lookup"><span data-stu-id="207f7-130">Reset user access</span></span>
<span data-ttu-id="207f7-131">如果您遺失存取 tooroot Linux VM 上，您可以啟動 VMAccess 指令碼 tooreset 使用者的 SSH 金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="207f7-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="207f7-132">tooreset hello SSH 公開金鑰的使用者，建立名為`reset_ssh_key.json`和加入的 hello 遵循格式設定。</span><span class="sxs-lookup"><span data-stu-id="207f7-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="207f7-133">取代您自己的值為 hello`username`和`ssh_key`參數：</span><span class="sxs-lookup"><span data-stu-id="207f7-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="207f7-134">執行與 hello VMAccess 指令碼：</span><span class="sxs-lookup"><span data-stu-id="207f7-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="207f7-135">tooreset 使用者密碼，建立名為`reset_user_password.json`和加入的 hello 遵循格式設定。</span><span class="sxs-lookup"><span data-stu-id="207f7-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="207f7-136">取代您自己的值為 hello`username`和`password`參數：</span><span class="sxs-lookup"><span data-stu-id="207f7-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="207f7-137">執行與 hello VMAccess 指令碼：</span><span class="sxs-lookup"><span data-stu-id="207f7-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="207f7-138">重新啟動 SSH</span><span class="sxs-lookup"><span data-stu-id="207f7-138">Restart SSH</span></span>
<span data-ttu-id="207f7-139">toorestart hello SSH 服務精靈和重設 hello SSH 組態 toodefault 值，請建立名為`reset_sshd.json`。</span><span class="sxs-lookup"><span data-stu-id="207f7-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="207f7-140">新增下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="207f7-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="207f7-141">執行與 hello VMAccess 指令碼：</span><span class="sxs-lookup"><span data-stu-id="207f7-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="207f7-142">管理使用者</span><span class="sxs-lookup"><span data-stu-id="207f7-142">Manage users</span></span>

<span data-ttu-id="207f7-143">toocreate 進行驗證，使用 SSH 金鑰的使用者建立名為`create_new_user.json`和加入的 hello 遵循格式設定。</span><span class="sxs-lookup"><span data-stu-id="207f7-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="207f7-144">取代您自己的值為 hello`username`和`ssh_key`參數：</span><span class="sxs-lookup"><span data-stu-id="207f7-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="207f7-145">執行與 hello VMAccess 指令碼：</span><span class="sxs-lookup"><span data-stu-id="207f7-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="207f7-146">toodelete 使用者時，建立名為`delete_user.json`並加入下列內容的 hello。</span><span class="sxs-lookup"><span data-stu-id="207f7-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="207f7-147">取代您自己的值為 hello`remove_user`參數：</span><span class="sxs-lookup"><span data-stu-id="207f7-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="207f7-148">執行與 hello VMAccess 指令碼：</span><span class="sxs-lookup"><span data-stu-id="207f7-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="207f7-149">檢查或修復 hello 磁碟</span><span class="sxs-lookup"><span data-stu-id="207f7-149">Check or repair hello disk</span></span>
<span data-ttu-id="207f7-150">您也可以使用 VMAccess 檢查並修復您加入 toohello Linux VM 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="207f7-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="207f7-151">toocheck，然後修復 hello 磁碟，建立名為`disk_check_repair.json`和加入的 hello 遵循格式設定。</span><span class="sxs-lookup"><span data-stu-id="207f7-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="207f7-152">取代您自己的值為 hello 名稱`repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="207f7-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="207f7-153">執行與 hello VMAccess 指令碼：</span><span class="sxs-lookup"><span data-stu-id="207f7-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="207f7-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="207f7-154">Next steps</span></span>
<span data-ttu-id="207f7-155">更新 Linux 使用 hello Azure VMAccess 擴充功能是在執行中的 Linux VM 上的一個方法 toomake 變更。</span><span class="sxs-lookup"><span data-stu-id="207f7-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="207f7-156">您也可以使用工具像是雲端 init 和 Azure 資源管理員範本 toomodify Linux VM 上開機。</span><span class="sxs-lookup"><span data-stu-id="207f7-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="207f7-157">適用於 Linux 的虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="207f7-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="207f7-158">使用 Linux VM 擴充功能編寫 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="207f7-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="207f7-159">在建立期間使用雲端 init toocustomize Linux VM</span><span class="sxs-lookup"><span data-stu-id="207f7-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

