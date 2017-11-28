---
title: "aaaUpload 自訂 Linux 映像與 Azure CLI 1.0 |Microsoft 文件"
description: "建立並上載虛擬硬碟 (VHD) tooAzure 與自訂 Linux 映像使用 hello Resource Manager 部署模型和 hello Azure CLI 1.0。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="386f3-103">上傳和自訂的磁碟映像建立 Linux VM，請使用 Azure CLI 1.0 hello</span><span class="sxs-lookup"><span data-stu-id="386f3-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="386f3-104">本文章將示範如何使用虛擬硬碟 (VHD) tooAzure tooupload hello Resource Manager 部署模型並從這個自訂映像建立 Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="386f3-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="386f3-105">這項功能可讓您 tooinstall 和設定 Linux distro tooyour 需求，然後使用該 VHD tooquickly 建立 Azure 虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="386f3-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="386f3-106">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="386f3-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="386f3-107">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="386f3-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="386f3-108">[Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="386f3-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="386f3-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="386f3-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="386f3-110">快速命令</span><span class="sxs-lookup"><span data-stu-id="386f3-110">Quick commands</span></span>
<span data-ttu-id="386f3-111">如果您需要 tooquickly 完成 hello 工作，請在下列章節詳細資料 hello hello 基底命令 tooupload VM tooAzure。</span><span class="sxs-lookup"><span data-stu-id="386f3-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="386f3-112">詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#requirements)。</span><span class="sxs-lookup"><span data-stu-id="386f3-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="386f3-113">請確定您有[hello Azure CLI 1.0](../../cli-install-nodejs.md)登入，並使用 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="386f3-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="386f3-114">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="386f3-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="386f3-115">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myimages`。</span><span class="sxs-lookup"><span data-stu-id="386f3-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="386f3-116">首先，建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="386f3-116">First, create a resource group.</span></span> <span data-ttu-id="386f3-117">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`WestUs`位置：</span><span class="sxs-lookup"><span data-stu-id="386f3-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="386f3-118">建立儲存體帳戶 toohold 虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="386f3-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="386f3-119">hello 下列範例會建立名為的儲存體帳戶`mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="386f3-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="386f3-120">清單 hello 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="386f3-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="386f3-121">記下 `key1`：</span><span class="sxs-lookup"><span data-stu-id="386f3-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="386f3-122">建立使用您所取得的 hello 儲存體金鑰的儲存體帳戶內的容器。</span><span class="sxs-lookup"><span data-stu-id="386f3-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="386f3-123">hello 下列範例會建立名為的容器`myimages`使用 hello 從儲存體金鑰值`key1`:</span><span class="sxs-lookup"><span data-stu-id="386f3-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="386f3-124">最後上, 傳您所建立的 VHD toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="386f3-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="386f3-125">指定 hello 本機路徑 tooyour VHD 下`/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="386f3-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="386f3-126">您現在可以 [使用 Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd)，從上傳的虛擬磁碟建立 VM。</span><span class="sxs-lookup"><span data-stu-id="386f3-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="386f3-127">您也可以藉由指定 hello URI tooyour 磁碟使用 hello CLI (`--image-urn`)。</span><span class="sxs-lookup"><span data-stu-id="386f3-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="386f3-128">hello 下列範例會建立名為的 VM`myVM`使用 hello 先前上傳的虛擬磁碟：</span><span class="sxs-lookup"><span data-stu-id="386f3-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="386f3-129">hello 目的地儲存體帳戶有 toobe 相同 hello 做為您上傳至您的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="386f3-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="386f3-130">您也需要 toospecify，或回答會提示您輸入時，所有 hello hello 所需的其他參數`azure vm create`命令，例如虛擬網路、 公用 IP 位址、 使用者名稱和 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="386f3-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="386f3-131">閱讀更多有關 hello[可用 CLI 資源管理員參數](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="386f3-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="386f3-132">需求</span><span class="sxs-lookup"><span data-stu-id="386f3-132">Requirements</span></span>
<span data-ttu-id="386f3-133">toocomplete hello 下列步驟，您需要：</span><span class="sxs-lookup"><span data-stu-id="386f3-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="386f3-134">**安裝.vhd 檔案中的 Linux 作業系統**-安裝[支援 Azure 的 linux Linux 發佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(或參閱[非背書發佈資訊](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD 中的虛擬磁碟格式。</span><span class="sxs-lookup"><span data-stu-id="386f3-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="386f3-135">VM 和 VHD toocreate 有多個工具：</span><span class="sxs-lookup"><span data-stu-id="386f3-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="386f3-136">安裝和設定[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU)或[KVM](http://www.linux-kvm.org/page/RunningKVM)，小心 toouse VHD 作為映像格式。</span><span class="sxs-lookup"><span data-stu-id="386f3-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="386f3-137">如有需要，您可以使用 `qemu-img convert` 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)。</span><span class="sxs-lookup"><span data-stu-id="386f3-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="386f3-138">您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="386f3-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="386f3-139">在 Azure 中不支援 hello 較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="386f3-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="386f3-140">當您建立 VM 時，指定 hello 格式 VHD。</span><span class="sxs-lookup"><span data-stu-id="386f3-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="386f3-141">如有需要您可以將轉換使用的 VHDX 磁碟 tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)或 hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="386f3-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="386f3-142">此外，Azure 不支援將動態 Vhd 上, 傳，以便您需要 tooconvert 這類磁碟 toostatic Vhd 上傳之前。</span><span class="sxs-lookup"><span data-stu-id="386f3-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="386f3-143">您可以使用工具，例如[Azure VHD 公用程式 GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert 動態磁碟上傳 tooAzure hello 程序期間。</span><span class="sxs-lookup"><span data-stu-id="386f3-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="386f3-144">從您的自訂映像建立 Vm 必須位在 hello 相同儲存體帳戶做為本身 hello 映像</span><span class="sxs-lookup"><span data-stu-id="386f3-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="386f3-145">建立儲存體帳戶和容器 toohold，您的自訂映像和建立的 Vm</span><span class="sxs-lookup"><span data-stu-id="386f3-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="386f3-146">建立所有 VM 之後，您即可放心地刪除您的映像</span><span class="sxs-lookup"><span data-stu-id="386f3-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="386f3-147">請確定您有[hello Azure CLI 1.0](../../cli-install-nodejs.md)登入，並使用 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="386f3-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="386f3-148">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="386f3-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="386f3-149">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myimages`。</span><span class="sxs-lookup"><span data-stu-id="386f3-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="386f3-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="386f3-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="386f3-151">準備上傳的 hello 映像 toobe</span><span class="sxs-lookup"><span data-stu-id="386f3-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="386f3-152">Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="386f3-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="386f3-153">hello 下列文章會引導您完成 tooprepare hello Azure 所支援各種 Linux 散發套件的方式：</span><span class="sxs-lookup"><span data-stu-id="386f3-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="386f3-154">**[CentOS 型散發套件](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="386f3-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="386f3-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="386f3-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="386f3-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="386f3-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="386f3-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="386f3-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="386f3-158">**[SLES 和 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="386f3-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="386f3-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="386f3-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="386f3-160">**[其他：非背書散發套件](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="386f3-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="386f3-161">另請參閱 hello  **[Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)**如需有關準備 Azure Linux 映像的多個一般秘訣。</span><span class="sxs-lookup"><span data-stu-id="386f3-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="386f3-162">hello [Azure 平台 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)適用於僅當其中一個 hello 背書分佈會搭配 hello 設定詳細資料，指定在支援版本底下執行 Linux 的 tooVMs [Linux 上支援 Azure 的 Linux分佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="386f3-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="386f3-163">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="386f3-163">Create a resource group</span></span>
<span data-ttu-id="386f3-164">資源群組以邏輯方式結合所有 hello Azure 資源 toosupport 您的虛擬機器，例如 hello 虛擬網路和儲存體。</span><span class="sxs-lookup"><span data-stu-id="386f3-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="386f3-165">從 [這裡](../../azure-resource-manager/resource-group-overview.md)深入了解 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="386f3-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="386f3-166">之前上傳您的自訂磁碟映像建立 Vm，您必須先 toocreate 資源群組。</span><span class="sxs-lookup"><span data-stu-id="386f3-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="386f3-167">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`WestUS`位置：</span><span class="sxs-lookup"><span data-stu-id="386f3-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="386f3-168">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="386f3-168">Create a storage account</span></span>
<span data-ttu-id="386f3-169">VM 會以分頁 Blob 的形式儲存在儲存體帳戶內。</span><span class="sxs-lookup"><span data-stu-id="386f3-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="386f3-170">從[這裡](../../storage/common/storage-introduction.md#blob-storage)深入了解 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="386f3-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="386f3-171">您要為自訂磁碟映像和 VM 建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="386f3-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="386f3-172">在您自訂的磁碟映像需要 toobe 從您建立的所有 Vm 都 hello 做為該映像的相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="386f3-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="386f3-173">hello 下列範例會建立名為的儲存體帳戶`mystorageaccount`hello 先前建立的資源群組中：</span><span class="sxs-lookup"><span data-stu-id="386f3-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="386f3-174">列出儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="386f3-174">List storage account keys</span></span>
<span data-ttu-id="386f3-175">Azure 會為每個儲存體帳戶產生兩個 512 位元的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="386f3-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="386f3-176">驗證 toohello 儲存體帳戶，例如 toocarry 寫入作業時，會使用這些存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="386f3-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="386f3-177">深入了解[管理存取 toostorage 這裡](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="386f3-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="386f3-178">您可以檢視便捷鍵以 hello`azure storage account keys list`命令。</span><span class="sxs-lookup"><span data-stu-id="386f3-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="386f3-179">檢視 hello hello 您所建立的儲存體帳戶的存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="386f3-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="386f3-180">hello 輸出如下：</span><span class="sxs-lookup"><span data-stu-id="386f3-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="386f3-181">請記下`key1`因為您可以將 toointeract hello 後續步驟中儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="386f3-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="386f3-182">建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="386f3-182">Create a storage container</span></span>
<span data-ttu-id="386f3-183">在 hello 中建立不同的目錄 toologically 相同方式，組織您的本機檔案系統，您的虛擬磁碟和映像，建立儲存體帳戶 tooorganize 內的容器。</span><span class="sxs-lookup"><span data-stu-id="386f3-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="386f3-184">儲存體帳戶可以包含任意數目的容器。</span><span class="sxs-lookup"><span data-stu-id="386f3-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="386f3-185">hello 下列範例會建立名為的容器`myimages`，指定 hello 便捷鍵 hello 上一個步驟中取得 (`key1`):</span><span class="sxs-lookup"><span data-stu-id="386f3-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="386f3-186">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="386f3-186">Upload VHD</span></span>
<span data-ttu-id="386f3-187">現在您可以實際上傳您的自訂磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="386f3-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="386f3-188">與 VM 使用的所有虛擬磁碟相同，您會以分頁 Blob 的形式上傳及儲存您的自訂磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="386f3-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="386f3-189">指定您的存取金鑰，您在 hello 前一個步驟中建立的 hello 容器，然後再 hello 路徑 toohello 自訂的磁碟映像，在本機電腦上：</span><span class="sxs-lookup"><span data-stu-id="386f3-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="386f3-190">從自訂映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="386f3-190">Create VM from custom image</span></span>
<span data-ttu-id="386f3-191">當您從您的自訂磁碟映像建立 Vm 時，請指定 hello URI toohello 磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="386f3-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="386f3-192">請確定該 hello 目的地儲存體帳戶儲存您的自訂磁碟映像的相符項目。</span><span class="sxs-lookup"><span data-stu-id="386f3-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="386f3-193">您可以建立您的 VM 使用 hello Azure CLI 或資源管理員 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="386f3-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="386f3-194">使用 Azure CLI hello 建立 VM</span><span class="sxs-lookup"><span data-stu-id="386f3-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="386f3-195">您指定 hello`--image-urn`參數以 hello`azure vm create`命令 toopoint tooyour 自訂的磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="386f3-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="386f3-196">請確認`--storage-account-name`相符項目 hello 儲存您的自訂磁碟映像的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="386f3-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="386f3-197">您沒有 toouse hello 相同容器 hello 自訂的磁碟映像 toostore 為您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="386f3-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="386f3-198">請確定 toocreate hello 中任何其他容器相同方式與上傳您的自訂磁碟映像之前 hello 先前的步驟。</span><span class="sxs-lookup"><span data-stu-id="386f3-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="386f3-199">hello 下列範例會建立名為的 VM`myVM`從您的自訂磁碟映像：</span><span class="sxs-lookup"><span data-stu-id="386f3-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="386f3-200">您仍然需要 toospecify，或回答會提示您輸入時，所有 hello hello 所需的其他參數`azure vm create`命令，例如虛擬網路、 公用 IP 位址、 使用者名稱和 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="386f3-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="386f3-201">深入了解 hello[可用 CLI 資源管理員參數](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="386f3-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="386f3-202">使用 JSON 範本來建立 VM</span><span class="sxs-lookup"><span data-stu-id="386f3-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="386f3-203">Azure 資源管理員範本會定義您想 toobuild hello 環境的 JavaScript Object Notation (JSON) 檔案。</span><span class="sxs-lookup"><span data-stu-id="386f3-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="386f3-204">hello 範本會細分 toodifferent 資源提供者，例如計算或網路中。</span><span class="sxs-lookup"><span data-stu-id="386f3-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="386f3-205">您可以使用現有的範本或自行撰寫範本。</span><span class="sxs-lookup"><span data-stu-id="386f3-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="386f3-206">深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="386f3-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="386f3-207">Hello 內`Microsoft.Compute/virtualMachines`範本的提供者，您有`storageProfile`節點，包含您的 VM hello 設定詳細資料。</span><span class="sxs-lookup"><span data-stu-id="386f3-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="386f3-208">hello 兩個主要的參數 tooedit 是 hello`image`和`vhd`點 tooyour 自訂的磁碟映像，您的新 VM 的虛擬磁碟的 Uri。</span><span class="sxs-lookup"><span data-stu-id="386f3-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="386f3-209">hello 下列顯示 hello JSON 的範例使用自訂的磁碟映像：</span><span class="sxs-lookup"><span data-stu-id="386f3-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="386f3-210">您可以使用[這個現有的範本 toocreate 從自訂映像的 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)或閱讀有關[建立您自己的 Azure Resource Manager 範本](../../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="386f3-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="386f3-211">設定範本之後，您會建立 Vm 使用 hello`azure group deployment create`命令。</span><span class="sxs-lookup"><span data-stu-id="386f3-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="386f3-212">指定 hello JSON 範本的 URI 與 hello`--template-uri`參數：</span><span class="sxs-lookup"><span data-stu-id="386f3-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="386f3-213">如果您有 JSON 檔案儲存在本機電腦上，您可以使用 hello`--template-file`參數改為：</span><span class="sxs-lookup"><span data-stu-id="386f3-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="386f3-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="386f3-214">Next steps</span></span>
<span data-ttu-id="386f3-215">在您備妥並上傳自訂虛擬磁碟之後，您可以深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="386f3-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="386f3-216">您也可以太[新增資料磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)tooyour 新 Vm。</span><span class="sxs-lookup"><span data-stu-id="386f3-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="386f3-217">如果您有 Vm 上執行，您需要 tooaccess 應用程式，請務必太[開啟連接埠和端點](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="386f3-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

