---
title: "使用 Azure CLI 1.0 上傳自訂 Linux 映像 | Microsoft Docs"
description: "使用 Resource Manager 部署模型與 Azure CLI 1.0 搭配自訂 Linux 映像，來建立虛擬硬碟 (VHD) 並上傳至 Azure。"
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
ms.openlocfilehash: ca4c6cb9296028275b2b032af0c94baabeec1223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-the-azure-cli-10"></a><span data-ttu-id="5d15c-103">使用 Azure CLI 1.0 從自訂磁碟映像上傳並建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="5d15c-103">Upload and create a Linux VM from custom disk image by using the Azure CLI 1.0</span></span>
<span data-ttu-id="5d15c-104">本文說明如何使用 Resource Manager 部署模型，將虛擬硬碟 (VHD) 上傳至 Azure，並從這個自訂映像建立 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="5d15c-104">This article shows you how to upload a virtual hard disk (VHD) to Azure using the Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="5d15c-105">這項功能可讓您安裝和設定 Linux 散發版本以符合您的需求，然後使用該 VHD 快速建立 Azure 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="5d15c-105">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="5d15c-106">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="5d15c-106">CLI versions to complete the task</span></span>
<span data-ttu-id="5d15c-107">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="5d15c-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="5d15c-108">[Azure CLI 1.0](#quick-commands) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="5d15c-108">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="5d15c-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="5d15c-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="5d15c-110">快速命令</span><span class="sxs-lookup"><span data-stu-id="5d15c-110">Quick commands</span></span>
<span data-ttu-id="5d15c-111">如果您需要快速完成工作，下列章節詳細說明上傳 VM 至 Azure 的基本命令。</span><span class="sxs-lookup"><span data-stu-id="5d15c-111">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="5d15c-112">每個步驟的詳細資訊和內容可在文件其他地方找到，[從這裡開始](#requirements)。</span><span class="sxs-lookup"><span data-stu-id="5d15c-112">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="5d15c-113">確定您已登入 [Azure CLI 1.0](../../cli-install-nodejs.md)，並且使用的是 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="5d15c-113">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="5d15c-114">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="5d15c-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5d15c-115">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myimages`。</span><span class="sxs-lookup"><span data-stu-id="5d15c-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="5d15c-116">首先，建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d15c-116">First, create a resource group.</span></span> <span data-ttu-id="5d15c-117">下列範例會在 `WestUs` 位置建立名為 `myResourceGroup` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="5d15c-117">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="5d15c-118">建立的儲存體帳戶以放置虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="5d15c-118">Create a storage account to hold your virtual disks.</span></span> <span data-ttu-id="5d15c-119">下列範例會建立名為 `mystorageaccount` 的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="5d15c-119">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="5d15c-120">列出儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d15c-120">List the access keys for your storage account.</span></span> <span data-ttu-id="5d15c-121">記下 `key1`：</span><span class="sxs-lookup"><span data-stu-id="5d15c-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="5d15c-122">使用取得的儲存體金鑰在您的儲存體帳戶內建立容器。</span><span class="sxs-lookup"><span data-stu-id="5d15c-122">Create a container within your storage account using the storage key you obtained.</span></span> <span data-ttu-id="5d15c-123">下列範例會使用來自 `key1` 的儲存體金鑰值，建立名為 `myimages` 的容器：</span><span class="sxs-lookup"><span data-stu-id="5d15c-123">The following example creates a container named `myimages` using the storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="5d15c-124">最後，將您的 VHD 上傳至您所建立的容器。</span><span class="sxs-lookup"><span data-stu-id="5d15c-124">Finally, upload your VHD to the container you created.</span></span> <span data-ttu-id="5d15c-125">在 `/path/to/disk/mydisk.vhd` 下方為您的 VHD 指定本機路徑：</span><span class="sxs-lookup"><span data-stu-id="5d15c-125">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="5d15c-126">您現在可以 [使用 Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd)，從上傳的虛擬磁碟建立 VM。</span><span class="sxs-lookup"><span data-stu-id="5d15c-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="5d15c-127">您也可以藉由指定磁碟 (`--image-urn`) 的 URI 來使用 CLI。</span><span class="sxs-lookup"><span data-stu-id="5d15c-127">You can also use the CLI by specifying the URI to your disk (`--image-urn`).</span></span> <span data-ttu-id="5d15c-128">下列範例會使用先前上傳的虛擬磁碟來建立名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="5d15c-128">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="5d15c-129">目的地儲存體帳戶必須與您上傳虛擬磁碟的目的地帳戶相同。</span><span class="sxs-lookup"><span data-stu-id="5d15c-129">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="5d15c-130">您也需要指定或依據提示回答 `azure vm create` 命令所需的所有其他參數，例如虛擬網路、公用 IP 位址、使用者名稱及 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d15c-130">You also need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="5d15c-131">您可以深入了解[可用的 CLI Resource Manager 參數](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="5d15c-131">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="5d15c-132">需求</span><span class="sxs-lookup"><span data-stu-id="5d15c-132">Requirements</span></span>
<span data-ttu-id="5d15c-133">若要完成下列步驟，您需要：</span><span class="sxs-lookup"><span data-stu-id="5d15c-133">To complete the following steps, you need:</span></span>

* <span data-ttu-id="5d15c-134">**以 .vhd 檔案安裝的 Linux 作業系統** - 以 VHD 格式將 [Azure 背書的 Linux 散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (或參閱[非背書散發套件的資訊](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) 安裝到虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="5d15c-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="5d15c-135">有多項工具可用來建立 VM 和 VHD：</span><span class="sxs-lookup"><span data-stu-id="5d15c-135">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="5d15c-136">安裝和設定 [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 或 [KVM](http://www.linux-kvm.org/page/RunningKVM)，並小心使用 VHD 做為您的映像格式。</span><span class="sxs-lookup"><span data-stu-id="5d15c-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="5d15c-137">如有需要，您可以使用 `qemu-img convert` 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)。</span><span class="sxs-lookup"><span data-stu-id="5d15c-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="5d15c-138">您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="5d15c-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="5d15c-139">Azure 不支援較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="5d15c-139">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="5d15c-140">當您建立 VM 時，請指定 VHD 做為格式。</span><span class="sxs-lookup"><span data-stu-id="5d15c-140">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="5d15c-141">如有需要，您可以使用 [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 或 [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell Cmdlet 將 VHDX 磁碟轉換為 VHD。</span><span class="sxs-lookup"><span data-stu-id="5d15c-141">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="5d15c-142">此外，Azure 不支援上傳動態 VHD，因此您必須將此類磁碟轉換成靜態 VHD 再上傳。</span><span class="sxs-lookup"><span data-stu-id="5d15c-142">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="5d15c-143">您可以在上傳至 Azure 的期間使用 [適用於 GO 的 Azure VHD 公用程式](https://github.com/Microsoft/azure-vhd-utils-for-go) 之類的工具來轉換動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="5d15c-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="5d15c-144">從自訂映像建立的 VM 必須位於與映像本身相同的儲存體帳戶中</span><span class="sxs-lookup"><span data-stu-id="5d15c-144">VMs created from your custom image must reside in the same storage account as the image itself</span></span>
  * <span data-ttu-id="5d15c-145">建立儲存體帳戶和容器來存放您的自訂映像和所建立的 VM</span><span class="sxs-lookup"><span data-stu-id="5d15c-145">Create a storage account and container to hold both your custom image and created VMs</span></span>
  * <span data-ttu-id="5d15c-146">建立所有 VM 之後，您即可放心地刪除您的映像</span><span class="sxs-lookup"><span data-stu-id="5d15c-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="5d15c-147">確定您已登入 [Azure CLI 1.0](../../cli-install-nodejs.md)，並且使用的是 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="5d15c-147">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="5d15c-148">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="5d15c-148">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5d15c-149">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myimages`。</span><span class="sxs-lookup"><span data-stu-id="5d15c-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="5d15c-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="5d15c-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-image-to-be-uploaded"></a><span data-ttu-id="5d15c-151">備妥要上傳的映像</span><span class="sxs-lookup"><span data-stu-id="5d15c-151">Prepare the image to be uploaded</span></span>
<span data-ttu-id="5d15c-152">Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="5d15c-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="5d15c-153">下列文章會逐步引導您了解如何準備 Azure 上支援的各種 Linux 散發套件：</span><span class="sxs-lookup"><span data-stu-id="5d15c-153">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="5d15c-154">**[CentOS 型散發套件](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5d15c-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5d15c-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5d15c-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5d15c-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5d15c-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5d15c-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5d15c-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5d15c-158">**[SLES 和 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5d15c-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5d15c-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5d15c-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5d15c-160">**[其他：非背書散發套件](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5d15c-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="5d15c-161">如需有關為 Azure 準備 Linux 映像的更多一般秘訣，另請參閱 **[Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)**。</span><span class="sxs-lookup"><span data-stu-id="5d15c-161">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="5d15c-162">只有在搭配[經 Azure 背書之 Linux 散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中＜支援的版本＞下指定的組態詳細資料來使用其中一個經背書的散發套件時，[Azure 平台 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) 才適用於執行 Linux 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d15c-162">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="5d15c-163">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="5d15c-163">Create a resource group</span></span>
<span data-ttu-id="5d15c-164">資源群組會以邏輯方式將所有 Azure 資源 (例如虛擬網路和儲存體) 結合在一起以支援您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d15c-164">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="5d15c-165">從 [這裡](../../azure-resource-manager/resource-group-overview.md)深入了解 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d15c-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="5d15c-166">在上傳您的自訂磁碟映像並建立 VM 之前，您必須先建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d15c-166">Before uploading your custom disk image and creating VMs, you first need to create a resource group.</span></span> 

<span data-ttu-id="5d15c-167">下列範例會在 `WestUS` 位置建立名為 `myResourceGroup` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="5d15c-167">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="5d15c-168">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5d15c-168">Create a storage account</span></span>
<span data-ttu-id="5d15c-169">VM 會以分頁 Blob 的形式儲存在儲存體帳戶內。</span><span class="sxs-lookup"><span data-stu-id="5d15c-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="5d15c-170">從[這裡](../../storage/common/storage-introduction.md#blob-storage)深入了解 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5d15c-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="5d15c-171">您要為自訂磁碟映像和 VM 建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d15c-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="5d15c-172">您從自訂磁碟映像建立的所有 VM 都必須位於與該映像相同的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5d15c-172">Any VMs that you create from your custom disk image need to be in the same storage account as that image.</span></span>

<span data-ttu-id="5d15c-173">下列範例會在先前建立的資源群組中建立名為 `mystorageaccount` 的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="5d15c-173">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="5d15c-174">列出儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="5d15c-174">List storage account keys</span></span>
<span data-ttu-id="5d15c-175">Azure 會為每個儲存體帳戶產生兩個 512 位元的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d15c-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="5d15c-176">對儲存體帳戶進行驗證時 (例如為了執行寫入作業)，就會使用這些存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d15c-176">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="5d15c-177">從 [這裡](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)深入了解如何管理對儲存體的存取。</span><span class="sxs-lookup"><span data-stu-id="5d15c-177">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="5d15c-178">您可以使用 `azure storage account keys list` 命令來檢視存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d15c-178">You can view access keys with the `azure storage account keys list` command.</span></span>

<span data-ttu-id="5d15c-179">檢視您所建立儲存體帳戶的存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="5d15c-179">View the access keys for the storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="5d15c-180">輸出如下：</span><span class="sxs-lookup"><span data-stu-id="5d15c-180">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="5d15c-181">請記下 `key1` ，因為在接下來的步驟中，您將使用它來與您的儲存體帳戶互動。</span><span class="sxs-lookup"><span data-stu-id="5d15c-181">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="5d15c-182">建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="5d15c-182">Create a storage container</span></span>
<span data-ttu-id="5d15c-183">您可以在儲存體帳戶內建立容器來組織您的虛擬磁碟和映像，方法與您建立不同目錄來以邏輯方式組織本機檔案系統相同。</span><span class="sxs-lookup"><span data-stu-id="5d15c-183">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your virtual disks and images.</span></span> <span data-ttu-id="5d15c-184">儲存體帳戶可以包含任意數目的容器。</span><span class="sxs-lookup"><span data-stu-id="5d15c-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="5d15c-185">下列範例會建立一個名為 `myimages` 的容器，其中指定前一個步驟中取得的存取金鑰 (`key1`)：</span><span class="sxs-lookup"><span data-stu-id="5d15c-185">The following example creates a container named `myimages`, specifying the access key obtained in the previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="5d15c-186">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="5d15c-186">Upload VHD</span></span>
<span data-ttu-id="5d15c-187">現在您可以實際上傳您的自訂磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="5d15c-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="5d15c-188">與 VM 使用的所有虛擬磁碟相同，您會以分頁 Blob 的形式上傳及儲存您的自訂磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="5d15c-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="5d15c-189">指定您的存取金鑰、您在上一個步驟中建立的容器，然後指定您本機電腦上自訂磁碟映像的路徑：</span><span class="sxs-lookup"><span data-stu-id="5d15c-189">Specify your access key, the container you created in the previous step, and then the path to the custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="5d15c-190">從自訂映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="5d15c-190">Create VM from custom image</span></span>
<span data-ttu-id="5d15c-191">當您從自訂磁碟映像建立 VM 時，請指定磁碟映像的 URI。</span><span class="sxs-lookup"><span data-stu-id="5d15c-191">When you create VMs from your custom disk image, specify the URI to the disk image.</span></span> <span data-ttu-id="5d15c-192">請確保目的地儲存體帳戶與儲存您自訂磁碟映像的儲存體帳戶相符。</span><span class="sxs-lookup"><span data-stu-id="5d15c-192">Ensure that the destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="5d15c-193">您可以使用 Azure CLI 或 Resource Manager JSON 範本來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="5d15c-193">You can create your VM using the Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-the-azure-cli"></a><span data-ttu-id="5d15c-194">使用 Azure CLI 來建立 VM</span><span class="sxs-lookup"><span data-stu-id="5d15c-194">Create a VM using the Azure CLI</span></span>
<span data-ttu-id="5d15c-195">您需搭配 `azure vm create` 命令指定 `--image-urn` 參數，以指向您的自訂磁碟映像。</span><span class="sxs-lookup"><span data-stu-id="5d15c-195">You specify the `--image-urn` parameter with the `azure vm create` command to point to your custom disk image.</span></span> <span data-ttu-id="5d15c-196">請確保 `--storage-account-name` 與儲存您自訂磁碟映像的儲存體帳戶相符。</span><span class="sxs-lookup"><span data-stu-id="5d15c-196">Ensure that `--storage-account-name` matches the storage account where your custom disk image is stored.</span></span> <span data-ttu-id="5d15c-197">您不需使用與自訂磁碟映像相同的容器來儲存您的 VM。</span><span class="sxs-lookup"><span data-stu-id="5d15c-197">You do not have to use the same container as the custom disk image to store your VMs.</span></span> <span data-ttu-id="5d15c-198">上傳您的自訂磁碟映像之前，請確定會使用與先前步驟中相同的方式來建立任何額外的容器。</span><span class="sxs-lookup"><span data-stu-id="5d15c-198">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="5d15c-199">下列範例會從您的自訂磁碟映像建立名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="5d15c-199">The following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="5d15c-200">您仍需指定或依據提示回答 `azure vm create` 命令所需的所有其他參數，例如虛擬網路、公用 IP 位址、使用者名稱及 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="5d15c-200">You still need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="5d15c-201">深入了解 [可用的 CLI Resource Manager 參數](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="5d15c-201">Read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="5d15c-202">使用 JSON 範本來建立 VM</span><span class="sxs-lookup"><span data-stu-id="5d15c-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="5d15c-203">Azure Resource Manager 範本是「JavaScript 物件標記法」(JSON) 檔案，定義了您想要建置的環境。</span><span class="sxs-lookup"><span data-stu-id="5d15c-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="5d15c-204">範本會細分成不同的資源提供者，例如計算或網路。</span><span class="sxs-lookup"><span data-stu-id="5d15c-204">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="5d15c-205">您可以使用現有的範本或自行撰寫範本。</span><span class="sxs-lookup"><span data-stu-id="5d15c-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="5d15c-206">深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5d15c-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="5d15c-207">在範本的 `Microsoft.Compute/virtualMachines` 提供者內，您會有一個包含 VM 組態詳細資料的 `storageProfile` 節點。</span><span class="sxs-lookup"><span data-stu-id="5d15c-207">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="5d15c-208">兩個要編輯的主要參數為 `image` 和 `vhd` URI，分別指向您的自訂磁碟映像和新 VM 的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="5d15c-208">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="5d15c-209">以下顯示使用自訂磁碟映像的 JSON 範例：</span><span class="sxs-lookup"><span data-stu-id="5d15c-209">The following shows an example of the JSON for using a custom disk image:</span></span>

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

<span data-ttu-id="5d15c-210">您可以使用[這個現有的範本以從自訂映像建立 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) 或閱讀[建立您自己的 Azure Resource Manager 範本](../../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="5d15c-210">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="5d15c-211">設定完範本之後，您需使用 `azure group deployment create` 命令來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="5d15c-211">Once you have a template configured, you create your VMs using the `azure group deployment create` command.</span></span> <span data-ttu-id="5d15c-212">請使用 `--template-uri` 參數來指定您 JSON 範本的 URI︰</span><span class="sxs-lookup"><span data-stu-id="5d15c-212">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="5d15c-213">如果您已在電腦本機儲存 JSON 檔案，則可以改用 `--template-file` 參數︰</span><span class="sxs-lookup"><span data-stu-id="5d15c-213">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="5d15c-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d15c-214">Next steps</span></span>
<span data-ttu-id="5d15c-215">在您備妥並上傳自訂虛擬磁碟之後，您可以深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5d15c-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="5d15c-216">您也可以 [將資料磁碟新增](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 至您的新 VM。</span><span class="sxs-lookup"><span data-stu-id="5d15c-216">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="5d15c-217">如果您需要存取在您的 VM 上執行的應用程式，請務必 [開啟連接埠和端點](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5d15c-217">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

