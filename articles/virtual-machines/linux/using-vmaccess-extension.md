---
title: "將存取重設為 Azure Linux VM | Microsoft Docs"
description: "如何使用 VMAccess 擴充功能和 Azure CLI 2.0 在 Linux VM 上管理使用者及重設存取"
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
ms.openlocfilehash: 587c73278a9a92776276a811c5c4c8d3db773de3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-20"></a><span data-ttu-id="6602d-103">使用 VMAccess 擴充功能搭配 Azure CLI 2.0 在 Linux VM 上管理使用者、SSH 及檢查或修復磁碟</span><span class="sxs-lookup"><span data-stu-id="6602d-103">Manage users, SSH, and check or repair disks on Linux VMs using the VMAccess Extension with the Azure CLI 2.0</span></span>
<span data-ttu-id="6602d-104">Linux VM 的磁碟顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="6602d-104">The disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="6602d-105">您不知怎麼重設 Linux VM的根密碼，或不小心刪除了 SSH 私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6602d-105">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="6602d-106">如果是過去資料中心的時代發生此狀況，您必須親赴現場，然後再開啟 KVM 才能存取伺服器主控台。</span><span class="sxs-lookup"><span data-stu-id="6602d-106">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span></span> <span data-ttu-id="6602d-107">請將 Azure VMAccess 擴充功能想成 KVM 交換器，在此可以存取主控台重設 Linux 存取或執行磁碟等級維護。</span><span class="sxs-lookup"><span data-stu-id="6602d-107">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span></span>

<span data-ttu-id="6602d-108">本文將說明如何使用 Azure VMAccess 擴充功能來檢查或修復磁碟、重設使用者存取、管理使用者帳戶或重設 Linux 上的 SSH 組態。</span><span class="sxs-lookup"><span data-stu-id="6602d-108">This article shows you how to use the Azure VMAccess Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSH configuration on Linux.</span></span> <span data-ttu-id="6602d-109">您也可以使用 [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6602d-109">You can also perform these steps with the [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-to-use-the-vmaccess-extension"></a><span data-ttu-id="6602d-110">使用 VMAccess 擴充功能的方式</span><span class="sxs-lookup"><span data-stu-id="6602d-110">Ways to use the VMAccess Extension</span></span>
<span data-ttu-id="6602d-111">您可以透過兩種方式在 Linux VM 上使用「VMAccess 擴充功能」：</span><span class="sxs-lookup"><span data-stu-id="6602d-111">There are two ways that you can use the VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="6602d-112">使用 Azure CLI 2.0 和必要的參數。</span><span class="sxs-lookup"><span data-stu-id="6602d-112">Use the Azure CLI 2.0 and the required parameters.</span></span>
* <span data-ttu-id="6602d-113">[使用 VMAccess 擴充功能會處理然後作為行動依據的原始 JSON 檔案](#use-json-files-and-the-vmaccess-extension)。</span><span class="sxs-lookup"><span data-stu-id="6602d-113">[Use raw JSON files that the VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="6602d-114">下列範例會使用 [az vm user](/cli/azure/vm/user) 命令。</span><span class="sxs-lookup"><span data-stu-id="6602d-114">The following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="6602d-115">若要執行這些步驟，您需要安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並且使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6602d-115">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="6602d-116">重設 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="6602d-116">Reset SSH key</span></span>
<span data-ttu-id="6602d-117">下列範例會重設名為 `myVM` 的 VM 上使用者 `azureuser` 的 SSH 金鑰：</span><span class="sxs-lookup"><span data-stu-id="6602d-117">The following example resets the SSH key for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="6602d-118">重設密碼</span><span class="sxs-lookup"><span data-stu-id="6602d-118">Reset password</span></span>
<span data-ttu-id="6602d-119">下列範例會重設名為 `myVM` 的 VM 上使用者 `azureuser` 的密碼：</span><span class="sxs-lookup"><span data-stu-id="6602d-119">The following example resets the password for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="6602d-120">重新啟動 SSH</span><span class="sxs-lookup"><span data-stu-id="6602d-120">Restart SSH</span></span>
<span data-ttu-id="6602d-121">下列範例會重新啟動 SSH 精靈，並將 SSH 組態重設成名為 `myVM` 的 VM 上之預設值：</span><span class="sxs-lookup"><span data-stu-id="6602d-121">The following example restarts the SSH daemon and resets the SSH configuration to default values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="6602d-122">建立使用者</span><span class="sxs-lookup"><span data-stu-id="6602d-122">Create a user</span></span>
<span data-ttu-id="6602d-123">下列範例會在名為 `myVM` 的 VM 上，建立一個使用 SSH 金鑰進行驗證、名為 `myNewUser` 的使用者：</span><span class="sxs-lookup"><span data-stu-id="6602d-123">The following example creates a user named `myNewUser` using an SSH key for authentication on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="6602d-124">刪除使用者</span><span class="sxs-lookup"><span data-stu-id="6602d-124">Delete a user</span></span>
<span data-ttu-id="6602d-125">下列範例會刪除名為 `myVM` 之 VM 上名為 `myNewUser` 的使用者：</span><span class="sxs-lookup"><span data-stu-id="6602d-125">The following example deletes a user named `myNewUser` on the VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-the-vmaccess-extension"></a><span data-ttu-id="6602d-126">使用 JSON 檔案和 VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="6602d-126">Use JSON files and the VMAccess Extension</span></span>
<span data-ttu-id="6602d-127">下列範例會使用原始 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="6602d-127">The following examples use raw JSON files.</span></span> <span data-ttu-id="6602d-128">請使用 [az vm extension set](/cli/azure/vm/extension#set) 來接著呼叫您的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="6602d-128">Use [az vm extension set](/cli/azure/vm/extension#set) to then call your JSON files.</span></span> <span data-ttu-id="6602d-129">您也可以從 Azure 範本呼叫這些 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="6602d-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="6602d-130">重設使用者存取</span><span class="sxs-lookup"><span data-stu-id="6602d-130">Reset user access</span></span>
<span data-ttu-id="6602d-131">如果您已無法存取 Linux VM 上的根，可以啟動 VMAccess 指令碼來重設使用者的 SSH 金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="6602d-131">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset a user's SSH key or password.</span></span>

<span data-ttu-id="6602d-132">若要重設使用者的 SSH 公開金鑰，請建立名為 `reset_ssh_key.json` 的檔案，並以下列格式新增設定。</span><span class="sxs-lookup"><span data-stu-id="6602d-132">To reset the SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in the following format.</span></span> <span data-ttu-id="6602d-133">將您自己的值取代為 `username` 和 `ssh_key` 參數：</span><span class="sxs-lookup"><span data-stu-id="6602d-133">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="6602d-134">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="6602d-134">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="6602d-135">若要重設使用者密碼，請建立名為 `reset_user_password.json` 的檔案，並以下列格式新增設定。</span><span class="sxs-lookup"><span data-stu-id="6602d-135">To reset a user password, create a file named `reset_user_password.json` and add settings in the following format.</span></span> <span data-ttu-id="6602d-136">將您自己的值取代為 `username` 和 `password` 參數：</span><span class="sxs-lookup"><span data-stu-id="6602d-136">Substitute your own values for the `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="6602d-137">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="6602d-137">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="6602d-138">重新啟動 SSH</span><span class="sxs-lookup"><span data-stu-id="6602d-138">Restart SSH</span></span>
<span data-ttu-id="6602d-139">若要重新啟動 SSH 精靈並將 SSH 組態重設為預設值，請建立名為 `reset_sshd.json` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="6602d-139">To restart the SSH daemon and reset the SSH configuration to default values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="6602d-140">新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="6602d-140">Add the following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="6602d-141">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="6602d-141">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="6602d-142">管理使用者</span><span class="sxs-lookup"><span data-stu-id="6602d-142">Manage users</span></span>

<span data-ttu-id="6602d-143">若要建立使用 SSH 金鑰進行驗證的使用者，請建立名為 `create_new_user.json` 的檔案，並以下列格式新增設定。</span><span class="sxs-lookup"><span data-stu-id="6602d-143">To create a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in the following format.</span></span> <span data-ttu-id="6602d-144">將您自己的值取代為 `username` 和 `ssh_key` 參數：</span><span class="sxs-lookup"><span data-stu-id="6602d-144">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="6602d-145">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="6602d-145">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="6602d-146">若要刪除使用者，請建立名為 `delete_user.json` 的檔案並新增下列內容。</span><span class="sxs-lookup"><span data-stu-id="6602d-146">To delete a user, create a file named `delete_user.json` and add the following content.</span></span> <span data-ttu-id="6602d-147">將您自己的值取代為 `remove_user` 參數：</span><span class="sxs-lookup"><span data-stu-id="6602d-147">Substitute your own value for the `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="6602d-148">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="6602d-148">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-the-disk"></a><span data-ttu-id="6602d-149">檢查或修復磁碟</span><span class="sxs-lookup"><span data-stu-id="6602d-149">Check or repair the disk</span></span>
<span data-ttu-id="6602d-150">您也可以使用 VMAccess 來檢查並修復您新增至 Linux VM 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="6602d-150">Using VMAccess you can also check and repair a disk that you added to the Linux VM.</span></span>

<span data-ttu-id="6602d-151">若要檢查然後修復磁碟，請建立名為 `disk_check_repair.json` 的檔案，並以下列格式新增設定。</span><span class="sxs-lookup"><span data-stu-id="6602d-151">To check and then repair the disk, create a file named `disk_check_repair.json` and add settings in the following format.</span></span> <span data-ttu-id="6602d-152">將您自己的值取代為 `repair_disk` 的名稱：</span><span class="sxs-lookup"><span data-stu-id="6602d-152">Substitute your own value for the name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="6602d-153">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="6602d-153">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="6602d-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6602d-154">Next steps</span></span>
<span data-ttu-id="6602d-155">使用 Azure VMAccess 擴充功能來更新 Linux，是一種對執行中 Linux VM 進行變更的方法。</span><span class="sxs-lookup"><span data-stu-id="6602d-155">Updating Linux using the Azure VMAccess Extension is one method to make changes on a running Linux VM.</span></span> <span data-ttu-id="6602d-156">您也可以使用 cloud-init 和 Azure Resource Manager 範本之類的工具，在開機時修改您的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="6602d-156">You can also use tools like cloud-init and Azure Resource Manager templates to modify your Linux VM on boot.</span></span>

[<span data-ttu-id="6602d-157">適用於 Linux 的虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="6602d-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="6602d-158">使用 Linux VM 擴充功能編寫 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="6602d-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="6602d-159">在建立期間使用 cloud-init 自訂 Linux VM</span><span class="sxs-lookup"><span data-stu-id="6602d-159">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md)

