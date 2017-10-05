---
title: "使用 VMAccess 擴充功能重設 Azure Linux VM 的存取 | Microsoft Docs"
description: "使用 VMAccess 擴充功能重設 Azure Linux VM 的存取。"
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
ms.openlocfilehash: 278bf1785aac71068ab94cf9916af69a204c44be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-10"></a><span data-ttu-id="a9b94-103">使用 VMAccess 擴充功能搭配 Azure CLI 1.0 在 Azure Linux VM 上管理使用者、SSH 及檢查或修復磁碟</span><span class="sxs-lookup"><span data-stu-id="a9b94-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension with the Azure CLI 1.0</span></span>
<span data-ttu-id="a9b94-104">本文將說明如何使用 Azure VMAcesss 延伸模組來檢查或修復磁碟、重設使用者存取、管理使用者帳戶或重設 Linux 上的 SSHD 組態。</span><span class="sxs-lookup"><span data-stu-id="a9b94-104">This article shows you how to use the Azure VMAcesss Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSHD configuration on Linux.</span></span> <span data-ttu-id="a9b94-105">本文需要：</span><span class="sxs-lookup"><span data-stu-id="a9b94-105">The article requires:</span></span>

* <span data-ttu-id="a9b94-106">一個 Azure 帳戶 ([取得免費試用帳戶](https://azure.microsoft.com/pricing/free-trial/))。</span><span class="sxs-lookup"><span data-stu-id="a9b94-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="a9b94-107">使用 `azure login` 登入的 [Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="a9b94-107">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="a9b94-108">Azure CLI *必須處於* Azure Resource Manager 模式 `azure config mode arm`。</span><span class="sxs-lookup"><span data-stu-id="a9b94-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="a9b94-109">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="a9b94-109">CLI versions to complete the task</span></span>
<span data-ttu-id="a9b94-110">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="a9b94-111">[Azure CLI 1.0](#quick-commands) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="a9b94-111">[Azure CLI 1.0](#quick-commands)– our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a9b94-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="a9b94-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="a9b94-113">快速命令</span><span class="sxs-lookup"><span data-stu-id="a9b94-113">Quick commands</span></span>
<span data-ttu-id="a9b94-114">有兩種方式可在 Linux VM 上使用 VMAccess：</span><span class="sxs-lookup"><span data-stu-id="a9b94-114">There are two ways to use VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="a9b94-115">使用 Azure CLI 1.0 和必要的參數。</span><span class="sxs-lookup"><span data-stu-id="a9b94-115">Using the Azure CLI 1.0 and the required parameters.</span></span>
* <span data-ttu-id="a9b94-116">使用 VMAccess 處理的原始 JSON 檔案並採取行動。</span><span class="sxs-lookup"><span data-stu-id="a9b94-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="a9b94-117">針對快速命令區段，我們將使用 Azure CLI 1.0 `azure vm reset-access` 方法。</span><span class="sxs-lookup"><span data-stu-id="a9b94-117">For the quick command section, we are going to use the Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="a9b94-118">在下列命令範例中，將包含 "example" 的值取代為您環境中的值。</span><span class="sxs-lookup"><span data-stu-id="a9b94-118">In the following command examples, replace the values that contain "example" with the values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="a9b94-119">建立資源群組和 Linux VM</span><span class="sxs-lookup"><span data-stu-id="a9b94-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="a9b94-120">建立 Debian VM</span><span class="sxs-lookup"><span data-stu-id="a9b94-120">Create a Debian VM</span></span>
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

## <a name="reset-root-password"></a><span data-ttu-id="a9b94-121">重設根密碼</span><span class="sxs-lookup"><span data-stu-id="a9b94-121">Reset root password</span></span>
<span data-ttu-id="a9b94-122">重設根密碼：</span><span class="sxs-lookup"><span data-stu-id="a9b94-122">To reset the root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="a9b94-123">SSH 金鑰重設</span><span class="sxs-lookup"><span data-stu-id="a9b94-123">SSH key reset</span></span>
<span data-ttu-id="a9b94-124">若要重設非根使用者的 SSH 金鑰︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-124">To reset the SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="a9b94-125">建立使用者</span><span class="sxs-lookup"><span data-stu-id="a9b94-125">Create a user</span></span>
<span data-ttu-id="a9b94-126">若要建立使用者：</span><span class="sxs-lookup"><span data-stu-id="a9b94-126">To create a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="a9b94-127">移除使用者</span><span class="sxs-lookup"><span data-stu-id="a9b94-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="a9b94-128">重設 SSHD</span><span class="sxs-lookup"><span data-stu-id="a9b94-128">Reset SSHD</span></span>
<span data-ttu-id="a9b94-129">重設 SSHD 組態：</span><span class="sxs-lookup"><span data-stu-id="a9b94-129">To reset the SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="a9b94-130">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="a9b94-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="a9b94-131">VMAccess 已定義︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-131">VMAccess defined:</span></span>
<span data-ttu-id="a9b94-132">Linux VM 的磁碟顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="a9b94-132">The disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="a9b94-133">您不知怎麼重設 Linux VM的根密碼，或不小心刪除了 SSH 私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="a9b94-133">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="a9b94-134">如果是過去資料中心的時代發生此狀況，您必須親赴現場，然後再開啟 KVM 才能存取伺服器主控台。</span><span class="sxs-lookup"><span data-stu-id="a9b94-134">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span></span> <span data-ttu-id="a9b94-135">請將 Azure VMAccess 擴充功能想成 KVM 交換器，在此可以存取主控台重設 Linux 存取或執行磁碟等級維護。</span><span class="sxs-lookup"><span data-stu-id="a9b94-135">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span></span>

<span data-ttu-id="a9b94-136">在詳細的逐步解說中，我們會使用利用原始 JSON 檔案的完整格式 VMAccess。</span><span class="sxs-lookup"><span data-stu-id="a9b94-136">For the detailed walkthrough, we are going to use the long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="a9b94-137">從 Azure 範本也可以呼叫這些 VMAccess JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="a9b94-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-to-check-or-repair-the-disk-of-a-linux-vm"></a><span data-ttu-id="a9b94-138">使用 VMAccess 檢查或修復 Linux VM 的磁碟</span><span class="sxs-lookup"><span data-stu-id="a9b94-138">Using VMAccess to check or repair the disk of a Linux VM</span></span>
<span data-ttu-id="a9b94-139">使用 VMAccess 可以執行在 Linux VM 磁碟上執行的 fsck。</span><span class="sxs-lookup"><span data-stu-id="a9b94-139">Using VMAccess you can do a fsck run on the disk under your Linux VM.</span></span>  <span data-ttu-id="a9b94-140">您也可以使用 VMAccess 執行磁碟檢查和磁碟修復。</span><span class="sxs-lookup"><span data-stu-id="a9b94-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="a9b94-141">若要檢查並修復磁碟，請使用這個 VMAccess 指令碼︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-141">To check, and then repair the disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="a9b94-142">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-142">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-to-reset-user-access-to-linux"></a><span data-ttu-id="a9b94-143">使用 VMAccess 重設 Linux 的使用者存取</span><span class="sxs-lookup"><span data-stu-id="a9b94-143">Using VMAccess to reset user access to Linux</span></span>
<span data-ttu-id="a9b94-144">如已無法存取 Linux VM 的根，您可以啟動 VMAccess 指令碼來重設根密碼。</span><span class="sxs-lookup"><span data-stu-id="a9b94-144">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset the root password.</span></span>

<span data-ttu-id="a9b94-145">若要重設根密碼，請使用這個 VMAccess 指令碼︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-145">To reset the root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="a9b94-146">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-146">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="a9b94-147">若要重設非根使用者的 SSH 金鑰，請使用這個 VMAccess 指令碼︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-147">To reset the SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="a9b94-148">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-148">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-to-manage-user-accounts-on-linux"></a><span data-ttu-id="a9b94-149">使用 VMAccess 管理 Linux 的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="a9b94-149">Using VMAccess to manage user accounts on Linux</span></span>
<span data-ttu-id="a9b94-150">VMAccess 是一種 Python 指令碼，可用來管理 Linux VM 上的使用者，但不需要登入及使用 sudo 或根帳戶。</span><span class="sxs-lookup"><span data-stu-id="a9b94-150">VMAccess is a Python script that can be used to manage users on your Linux VM without logging in and using sudo or the root account.</span></span>

<span data-ttu-id="a9b94-151">若要建立使用者，請使用這個 VMAccess 指令碼︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-151">To create a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="a9b94-152">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-152">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="a9b94-153">若要刪除使用者，請使用這個 VMAccess 指令碼︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-153">To delete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="a9b94-154">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-154">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-to-reset-the-sshd-configuration"></a><span data-ttu-id="a9b94-155">使用 VMAccess 重設 SSHD 組態</span><span class="sxs-lookup"><span data-stu-id="a9b94-155">Using VMAccess to reset the SSHD configuration</span></span>
<span data-ttu-id="a9b94-156">如果您變更了 Linux VM SSHD 組態，並在驗證變更之前關閉 SSH 連線，您可能無法回到 SSH 作業。</span><span class="sxs-lookup"><span data-stu-id="a9b94-156">If you make changes to the Linux VMs SSHD configuration and close the SSH connection before verifying the changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="a9b94-157">VMAccess 可用來將 SSHD 組態重設回到已知的良好組態，而不需透過 SSH 登入。</span><span class="sxs-lookup"><span data-stu-id="a9b94-157">VMAccess can be used to reset the SSHD configuration back to a known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="a9b94-158">使用這個 VMAccess 指令碼重設 SSHD 組態：</span><span class="sxs-lookup"><span data-stu-id="a9b94-158">To reset the SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="a9b94-159">執行 VMAccess 指令碼搭配︰</span><span class="sxs-lookup"><span data-stu-id="a9b94-159">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="a9b94-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9b94-160">Next steps</span></span>
<span data-ttu-id="a9b94-161">使用 Azure VMAccess 延伸模組更新 Linux 是變更執行中的 Linux VM 的一種方法。</span><span class="sxs-lookup"><span data-stu-id="a9b94-161">Updating Linux using Azure VMAccess Extensions is one method to make changes on a running Linux VM.</span></span>  <span data-ttu-id="a9b94-162">您也可以使用類似 cloud-init 和 Azure 範本等工具，以在開機時修改您的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="a9b94-162">You can also use tools like cloud-init and Azure Templates to modify your Linux VM on boot.</span></span>

[<span data-ttu-id="a9b94-163">有關虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="a9b94-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="a9b94-164">使用 Linux VM 擴充功能編寫 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="a9b94-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="a9b94-165">在建立期間使用 cloud-init 自訂 Linux VM</span><span class="sxs-lookup"><span data-stu-id="a9b94-165">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

