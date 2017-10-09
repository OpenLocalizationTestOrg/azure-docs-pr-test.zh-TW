---
title: "aaaUpload Azure CLI 2.0 自訂 Linux 磁碟 |Microsoft 文件"
description: "建立及上傳的虛擬硬碟 (VHD) tooAzure 使用 hello Resource Manager 部署模型和 hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="48c75-103">上傳並從自訂的磁碟以 hello Azure CLI 2.0 建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="48c75-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="48c75-104">本文示範如何 tooupload 虛擬硬碟 (VHD) tooan Azure 儲存體帳戶與 hello Azure CLI 2.0，並從這個自訂的磁碟建立 Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="48c75-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="48c75-105">您也可以執行下列步驟以 hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="48c75-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="48c75-106">這項功能可讓您 tooinstall 和設定 Linux distro tooyour 需求，然後使用該 VHD tooquickly 建立 Azure 虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="48c75-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="48c75-107">本主題會使用儲存體帳戶的 hello 最終的 Vhd，但您也可以執行這些步驟使用[管理磁碟](upload-vhd.md)。</span><span class="sxs-lookup"><span data-stu-id="48c75-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="48c75-108">快速命令</span><span class="sxs-lookup"><span data-stu-id="48c75-108">Quick commands</span></span>
<span data-ttu-id="48c75-109">如果您需要 tooquickly 完成 hello 工作，請在下列章節詳細資料 hello hello 基底命令 tooupload VHD tooAzure。</span><span class="sxs-lookup"><span data-stu-id="48c75-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="48c75-110">詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#requirements)。</span><span class="sxs-lookup"><span data-stu-id="48c75-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="48c75-111">請確定您擁有 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="48c75-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="48c75-112">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="48c75-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="48c75-113">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `mydisks`。</span><span class="sxs-lookup"><span data-stu-id="48c75-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="48c75-114">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="48c75-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="48c75-115">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`WestUs`位置：</span><span class="sxs-lookup"><span data-stu-id="48c75-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="48c75-116">建立虛擬磁碟與儲存體帳戶 toohold [az 儲存體帳戶建立](/cli/azure/storage/account#create)。</span><span class="sxs-lookup"><span data-stu-id="48c75-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="48c75-117">hello 下列範例會建立名為的儲存體帳戶`mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="48c75-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="48c75-118">列出您的儲存體帳戶的 hello 便捷鍵[az 儲存體帳戶金鑰清單](/cli/azure/storage/account/keys#list)。</span><span class="sxs-lookup"><span data-stu-id="48c75-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="48c75-119">記下 `key1`：</span><span class="sxs-lookup"><span data-stu-id="48c75-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="48c75-120">建立使用 hello 儲存體金鑰與您取得儲存體帳戶內的容器[az 儲存體容器建立](/cli/azure/storage/container#create)。</span><span class="sxs-lookup"><span data-stu-id="48c75-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="48c75-121">hello 下列範例會建立名為的容器`mydisks`使用 hello 從儲存體金鑰值`key1`:</span><span class="sxs-lookup"><span data-stu-id="48c75-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="48c75-122">最後上, 傳您使用您建立的 VHD toohello 容器[az 儲存體 blob 上傳](/cli/azure/storage/blob#upload)。</span><span class="sxs-lookup"><span data-stu-id="48c75-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="48c75-123">指定 hello 本機路徑 tooyour VHD 下`/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="48c75-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="48c75-124">指定 hello URI tooyour 磁碟 (`--image`) 與[az vm 建立](/cli/azure/vm#create)。</span><span class="sxs-lookup"><span data-stu-id="48c75-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="48c75-125">hello 下列範例會建立名為的 VM`myVM`使用 hello 先前上傳的虛擬磁碟：</span><span class="sxs-lookup"><span data-stu-id="48c75-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="48c75-126">hello 目的地儲存體帳戶有 toobe 相同 hello 做為您上傳至您的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="48c75-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="48c75-127">您也需要 toospecify，或回答會提示您輸入時，所有 hello hello 所需的其他參數**az vm 建立**命令，例如虛擬網路、 公用 IP 位址、 使用者名稱和 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="48c75-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="48c75-128">閱讀更多有關 hello[可用 CLI 資源管理員參數](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="48c75-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="48c75-129">需求</span><span class="sxs-lookup"><span data-stu-id="48c75-129">Requirements</span></span>
<span data-ttu-id="48c75-130">toocomplete hello 下列步驟，您需要：</span><span class="sxs-lookup"><span data-stu-id="48c75-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="48c75-131">**安裝.vhd 檔案中的 Linux 作業系統**-安裝[支援 Azure 的 linux Linux 發佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(或參閱[非背書發佈資訊](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD 中的虛擬磁碟格式。</span><span class="sxs-lookup"><span data-stu-id="48c75-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="48c75-132">VM 和 VHD toocreate 有多個工具：</span><span class="sxs-lookup"><span data-stu-id="48c75-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="48c75-133">安裝和設定[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU)或[KVM](http://www.linux-kvm.org/page/RunningKVM)，小心 toouse VHD 作為映像格式。</span><span class="sxs-lookup"><span data-stu-id="48c75-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="48c75-134">如有需要，您可以使用 `qemu-img convert` 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)。</span><span class="sxs-lookup"><span data-stu-id="48c75-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="48c75-135">您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="48c75-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="48c75-136">在 Azure 中不支援 hello 較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="48c75-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="48c75-137">當您建立 VM 時，指定 hello 格式 VHD。</span><span class="sxs-lookup"><span data-stu-id="48c75-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="48c75-138">如有需要您可以將轉換使用的 VHDX 磁碟 tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)或 hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="48c75-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="48c75-139">此外，Azure 不支援將動態 Vhd 上, 傳，以便您需要 tooconvert 這類磁碟 toostatic Vhd 上傳之前。</span><span class="sxs-lookup"><span data-stu-id="48c75-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="48c75-140">您可以使用工具，例如[Azure VHD 公用程式 GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert 動態磁碟上傳 tooAzure hello 程序期間。</span><span class="sxs-lookup"><span data-stu-id="48c75-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="48c75-141">建立從自訂磁碟的 Vm 必須位在 hello 相同本身 hello 磁碟儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48c75-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="48c75-142">建立儲存體帳戶和容器 toohold 您自訂的磁碟和建立的 Vm</span><span class="sxs-lookup"><span data-stu-id="48c75-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="48c75-143">建立所有 VM 之後，您即可放心地刪除您的磁碟</span><span class="sxs-lookup"><span data-stu-id="48c75-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="48c75-144">請確定您擁有 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="48c75-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="48c75-145">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="48c75-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="48c75-146">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `mydisks`。</span><span class="sxs-lookup"><span data-stu-id="48c75-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="48c75-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="48c75-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="48c75-148">準備上傳的 hello 磁碟 toobe</span><span class="sxs-lookup"><span data-stu-id="48c75-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="48c75-149">Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="48c75-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="48c75-150">hello 下列文章會引導您完成 tooprepare hello Azure 所支援各種 Linux 散發套件的方式：</span><span class="sxs-lookup"><span data-stu-id="48c75-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="48c75-151">**[CentOS 型散發套件](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="48c75-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="48c75-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="48c75-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="48c75-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="48c75-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="48c75-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="48c75-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="48c75-155">**[SLES 和 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="48c75-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="48c75-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="48c75-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="48c75-157">**[其他：非背書散發套件](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="48c75-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="48c75-158">另請參閱 hello  **[Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)**如需有關準備 Azure Linux 映像的多個一般秘訣。</span><span class="sxs-lookup"><span data-stu-id="48c75-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="48c75-159">hello [Azure 平台 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)適用於僅當其中一個 hello 背書分佈會搭配 hello 設定詳細資料，指定在支援版本底下執行 Linux 的 tooVMs [Linux 上支援 Azure 的 Linux分佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="48c75-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="48c75-160">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="48c75-160">Create a resource group</span></span>
<span data-ttu-id="48c75-161">資源群組以邏輯方式結合所有 hello Azure 資源 toosupport 您的虛擬機器，例如 hello 虛擬網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="48c75-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="48c75-162">如需有關資源群組的詳細資訊，請參閱[資源群組概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="48c75-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="48c75-163">上傳您自訂的磁碟和之前建立的 Vm，您必須先 toocreate 的資源群組與[az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="48c75-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="48c75-164">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westus`位置：</span><span class="sxs-lookup"><span data-stu-id="48c75-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="48c75-165">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="48c75-165">Create a storage account</span></span>

<span data-ttu-id="48c75-166">使用 [az storage account create](/cli/azure/storage/account#create) 為自訂磁碟和 VM 建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48c75-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="48c75-167">在您自訂的磁碟需要 toobe 從您建立的未受管理磁碟的任何 Vm hello 相同的磁碟儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48c75-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="48c75-168">hello 下列範例會建立名為的儲存體帳戶`mystorageaccount`hello 先前建立的資源群組中：</span><span class="sxs-lookup"><span data-stu-id="48c75-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="48c75-169">列出儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="48c75-169">List storage account keys</span></span>
<span data-ttu-id="48c75-170">Azure 會為每個儲存體帳戶產生兩個 512 位元的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="48c75-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="48c75-171">驗證 toohello 儲存體帳戶，例如 toocarry 寫入作業時，會使用這些存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="48c75-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="48c75-172">深入了解[管理存取 toostorage 這裡](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="48c75-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="48c75-173">檢視與 hello 便捷鍵[az 儲存體帳戶金鑰清單](/cli/azure/storage/account/keys#list)。</span><span class="sxs-lookup"><span data-stu-id="48c75-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="48c75-174">檢視 hello hello 您所建立的儲存體帳戶的存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="48c75-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="48c75-175">hello 輸出如下：</span><span class="sxs-lookup"><span data-stu-id="48c75-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="48c75-176">請記下`key1`因為您可以將 toointeract hello 後續步驟中儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48c75-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="48c75-177">建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="48c75-177">Create a storage container</span></span>
<span data-ttu-id="48c75-178">在 hello 中建立不同的目錄 toologically 相同方式，組織您的本機檔案系統，您建立儲存體帳戶 tooorganize 內的容器，您的磁碟。</span><span class="sxs-lookup"><span data-stu-id="48c75-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="48c75-179">儲存體帳戶可以包含任意數目的容器。</span><span class="sxs-lookup"><span data-stu-id="48c75-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="48c75-180">使用 [az storage container create](/cli/azure/storage/container#create) 來建立容器。</span><span class="sxs-lookup"><span data-stu-id="48c75-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="48c75-181">hello 下列範例會建立名為的容器`mydisks`:</span><span class="sxs-lookup"><span data-stu-id="48c75-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="48c75-182">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="48c75-182">Upload VHD</span></span>
<span data-ttu-id="48c75-183">現在您可以使用 [az storage blob upload](/cli/azure/storage/blob#upload) 上傳您的自訂磁碟。</span><span class="sxs-lookup"><span data-stu-id="48c75-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="48c75-184">您上傳並將您的自訂磁碟儲存為分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="48c75-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="48c75-185">指定您的存取金鑰，您在 hello 前一個步驟中建立的 hello 容器，然後 hello 路徑 toohello 自訂磁碟在本機電腦上：</span><span class="sxs-lookup"><span data-stu-id="48c75-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="48c75-186">建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="48c75-186">Create hello VM</span></span>
<span data-ttu-id="48c75-187">使用 unmanaged 磁碟時，VM toocreate 指定 hello URI tooyour 磁碟 (`--image`) 與[az vm 建立](/cli/azure/vm#create)。</span><span class="sxs-lookup"><span data-stu-id="48c75-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="48c75-188">hello 下列範例會建立名為的 VM`myVM`使用 hello 先前上傳的虛擬磁碟：</span><span class="sxs-lookup"><span data-stu-id="48c75-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="48c75-189">您指定 hello`--image`參數[az vm 建立](/cli/azure/vm#create)toopoint tooyour 自訂磁碟。</span><span class="sxs-lookup"><span data-stu-id="48c75-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="48c75-190">請確認`--storage-account`相符項目 hello 儲存您的自訂磁碟的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="48c75-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="48c75-191">您沒有 toouse hello 相同容器 hello 自訂磁碟 toostore 為您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="48c75-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="48c75-192">請確定 toocreate hello 中任何其他容器相同方式與上傳您的自訂磁碟之前 hello 先前的步驟。</span><span class="sxs-lookup"><span data-stu-id="48c75-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="48c75-193">hello 下列範例會建立名為的 VM`myVM`從自訂磁碟：</span><span class="sxs-lookup"><span data-stu-id="48c75-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="48c75-194">您仍然需要 toospecify，或回答會提示您輸入時，所有 hello hello 所需的其他參數**az vm 建立**命令，例如使用者名稱和 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="48c75-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="48c75-195">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="48c75-195">Resource Manager template</span></span>
<span data-ttu-id="48c75-196">Azure 資源管理員範本會定義您想 toobuild hello 環境的 JavaScript Object Notation (JSON) 檔案。</span><span class="sxs-lookup"><span data-stu-id="48c75-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="48c75-197">hello 範本會細分 toodifferent 資源提供者，例如計算或網路中。</span><span class="sxs-lookup"><span data-stu-id="48c75-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="48c75-198">您可以使用現有的範本或自行撰寫範本。</span><span class="sxs-lookup"><span data-stu-id="48c75-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="48c75-199">深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="48c75-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="48c75-200">Hello 內`Microsoft.Compute/virtualMachines`範本的提供者，您有`storageProfile`節點，包含您的 VM hello 設定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="48c75-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="48c75-201">hello 兩個主要的參數 tooedit 是 hello`image`和`vhd`點 tooyour 自訂磁碟和新 VM 的虛擬磁碟的 Uri。</span><span class="sxs-lookup"><span data-stu-id="48c75-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="48c75-202">hello 下列顯示 hello JSON 的範例使用自訂磁碟：</span><span class="sxs-lookup"><span data-stu-id="48c75-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="48c75-203">您可以使用[這個現有的範本 toocreate 從自訂映像的 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)或閱讀有關[建立您自己的 Azure Resource Manager 範本](../../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="48c75-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="48c75-204">設定範本之後，使用[az 群組部署建立](/cli/azure/group/deployment#create)toocreate Vm。</span><span class="sxs-lookup"><span data-stu-id="48c75-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="48c75-205">指定 hello JSON 範本的 URI 與 hello`--template-uri`參數：</span><span class="sxs-lookup"><span data-stu-id="48c75-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="48c75-206">如果您有 JSON 檔案儲存在本機電腦上，您可以使用 hello`--template-file`參數改為：</span><span class="sxs-lookup"><span data-stu-id="48c75-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="48c75-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48c75-207">Next steps</span></span>
<span data-ttu-id="48c75-208">在您備妥並上傳自訂虛擬磁碟之後，您可以深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="48c75-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="48c75-209">您也可以太[新增資料磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)tooyour 新 Vm。</span><span class="sxs-lookup"><span data-stu-id="48c75-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="48c75-210">如果您有 Vm 上執行，您需要 tooaccess 應用程式，請務必太[開啟連接埠和端點](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="48c75-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

