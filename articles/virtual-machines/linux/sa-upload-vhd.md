---
title: "使用 Azure CLI 2.0 上傳自訂 Linux 磁碟 | Microsoft Docs"
description: "使用 Resource Manager 部署模型和 Azure CLI 2.0 來建立虛擬硬碟 (VHD) 並上傳至 Azure"
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
ms.openlocfilehash: 9159960af396e89f373da711e0cc46fdd996ab83
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="2e004-103">使用 Azure CLI 2.0 從自訂磁碟上傳並建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="2e004-103">Upload and create a Linux VM from custom disk with the Azure CLI 2.0</span></span>
<span data-ttu-id="2e004-104">本文說明如何使用 Azure CLI 2.0，將虛擬硬碟 (VHD) 上傳至 Azure 儲存體帳戶，並從這個自訂磁碟建立 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="2e004-104">This article shows you how to upload a virtual hard disk (VHD) to an Azure storage account with the Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="2e004-105">您也可以使用 [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="2e004-105">You can also perform these steps with the [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2e004-106">這項功能可讓您安裝和設定 Linux 散發版本以符合您的需求，然後使用該 VHD 快速建立 Azure 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="2e004-106">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="2e004-107">本主題會將儲存體帳戶用於最終的 VHD，但您也可以使用[受控磁碟](upload-vhd.md)來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="2e004-107">This topic uses storage accounts for the final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="2e004-108">快速命令</span><span class="sxs-lookup"><span data-stu-id="2e004-108">Quick commands</span></span>
<span data-ttu-id="2e004-109">如果您需要快速完成作業，下列章節詳細說明將 VHD 上傳至 Azure 的基本命令。</span><span class="sxs-lookup"><span data-stu-id="2e004-109">If you need to quickly accomplish the task, the following section details the base commands to upload a VHD to Azure.</span></span> <span data-ttu-id="2e004-110">每個步驟的詳細資訊和內容可在文件其他地方找到，[從這裡開始](#requirements)。</span><span class="sxs-lookup"><span data-stu-id="2e004-110">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="2e004-111">請確定您已安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) 並使用 [az login](/cli/azure/#login) 登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e004-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="2e004-112">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="2e004-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2e004-113">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `mydisks`。</span><span class="sxs-lookup"><span data-stu-id="2e004-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="2e004-114">首先，使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="2e004-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2e004-115">下列範例會在 `WestUs` 位置建立名為 `myResourceGroup` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="2e004-115">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="2e004-116">使用 [az storage account create](/cli/azure/storage/account#create) 建立儲存體帳戶以存放您的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="2e004-116">Create a storage account to hold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="2e004-117">下列範例會建立名為 `mystorageaccount` 的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="2e004-117">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="2e004-118">使用 [az storage account keys list](/cli/azure/storage/account/keys#list) 列出您的儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2e004-118">List the access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="2e004-119">記下 `key1`：</span><span class="sxs-lookup"><span data-stu-id="2e004-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="2e004-120">使用透過 [az storage container create](/cli/azure/storage/container#create) 取得的儲存體金鑰在您的儲存體帳戶內建立容器。</span><span class="sxs-lookup"><span data-stu-id="2e004-120">Create a container within your storage account using the storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="2e004-121">下列範例會使用來自 `key1` 的儲存體金鑰值，建立名為 `mydisks` 的容器：</span><span class="sxs-lookup"><span data-stu-id="2e004-121">The following example creates a container named `mydisks` using the storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="2e004-122">最後，使用 [az storage blob upload](/cli/azure/storage/blob#upload) 將您的 VHD 上傳至您所建立的容器。</span><span class="sxs-lookup"><span data-stu-id="2e004-122">Finally, upload your VHD to the container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="2e004-123">在 `/path/to/disk/mydisk.vhd` 下方為您的 VHD 指定本機路徑：</span><span class="sxs-lookup"><span data-stu-id="2e004-123">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="2e004-124">使用 [az vm create](/cli/azure/vm#create)，為您的磁碟指定 URI (`--image`)。</span><span class="sxs-lookup"><span data-stu-id="2e004-124">Specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2e004-125">下列範例會使用先前上傳的虛擬磁碟來建立名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="2e004-125">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="2e004-126">目的地儲存體帳戶必須與您上傳虛擬磁碟的目的地帳戶相同。</span><span class="sxs-lookup"><span data-stu-id="2e004-126">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="2e004-127">您也需要指定或依據提示回答 **az vm create** 命令所需的所有其他參數，例如虛擬網路、公用 IP 位址、使用者名稱及 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2e004-127">You also need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="2e004-128">您可以深入了解[可用的 CLI Resource Manager 參數](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)。</span><span class="sxs-lookup"><span data-stu-id="2e004-128">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="2e004-129">需求</span><span class="sxs-lookup"><span data-stu-id="2e004-129">Requirements</span></span>
<span data-ttu-id="2e004-130">若要完成下列步驟，您需要：</span><span class="sxs-lookup"><span data-stu-id="2e004-130">To complete the following steps, you need:</span></span>

* <span data-ttu-id="2e004-131">**以 .vhd 檔案安裝的 Linux 作業系統** - 以 VHD 格式將 [Azure 背書的 Linux 散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (或參閱[非背書散發套件的資訊](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) 安裝到虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="2e004-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="2e004-132">有多項工具可用來建立 VM 和 VHD：</span><span class="sxs-lookup"><span data-stu-id="2e004-132">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="2e004-133">安裝和設定 [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 或 [KVM](http://www.linux-kvm.org/page/RunningKVM)，並小心使用 VHD 做為您的映像格式。</span><span class="sxs-lookup"><span data-stu-id="2e004-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="2e004-134">如有需要，您可以使用 `qemu-img convert` 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)。</span><span class="sxs-lookup"><span data-stu-id="2e004-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="2e004-135">您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="2e004-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="2e004-136">Azure 不支援較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="2e004-136">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="2e004-137">當您建立 VM 時，請指定 VHD 做為格式。</span><span class="sxs-lookup"><span data-stu-id="2e004-137">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="2e004-138">如有需要，您可以使用 [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 或 [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell Cmdlet 將 VHDX 磁碟轉換為 VHD。</span><span class="sxs-lookup"><span data-stu-id="2e004-138">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="2e004-139">此外，Azure 不支援上傳動態 VHD，因此您必須將此類磁碟轉換成靜態 VHD 再上傳。</span><span class="sxs-lookup"><span data-stu-id="2e004-139">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="2e004-140">您可以在上傳至 Azure 的期間使用 [適用於 GO 的 Azure VHD 公用程式](https://github.com/Microsoft/azure-vhd-utils-for-go) 之類的工具來轉換動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="2e004-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="2e004-141">從自訂磁碟建立的 VM 必須位於與磁碟本身相同的儲存體帳戶中</span><span class="sxs-lookup"><span data-stu-id="2e004-141">VMs created from your custom disk must reside in the same storage account as the disk itself</span></span>
  * <span data-ttu-id="2e004-142">建立儲存體帳戶和容器來存放您的自訂磁碟和所建立的 VM</span><span class="sxs-lookup"><span data-stu-id="2e004-142">Create a storage account and container to hold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="2e004-143">建立所有 VM 之後，您即可放心地刪除您的磁碟</span><span class="sxs-lookup"><span data-stu-id="2e004-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="2e004-144">請確定您已安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) 並使用 [az login](/cli/azure/#login) 登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e004-144">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="2e004-145">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="2e004-145">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2e004-146">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `mydisks`。</span><span class="sxs-lookup"><span data-stu-id="2e004-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="2e004-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="2e004-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-disk-to-be-uploaded"></a><span data-ttu-id="2e004-148">準備要上傳的磁碟</span><span class="sxs-lookup"><span data-stu-id="2e004-148">Prepare the disk to be uploaded</span></span>
<span data-ttu-id="2e004-149">Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="2e004-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="2e004-150">下列文章會逐步引導您了解如何準備 Azure 上支援的各種 Linux 散發套件：</span><span class="sxs-lookup"><span data-stu-id="2e004-150">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="2e004-151">**[CentOS 型散發套件](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2e004-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2e004-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2e004-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2e004-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2e004-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2e004-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2e004-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2e004-155">**[SLES 和 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2e004-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2e004-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2e004-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="2e004-157">**[其他：非背書散發套件](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="2e004-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="2e004-158">如需有關為 Azure 準備 Linux 映像的更多一般秘訣，另請參閱 **[Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)**。</span><span class="sxs-lookup"><span data-stu-id="2e004-158">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="2e004-159">只有在搭配[經 Azure 背書之 Linux 散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中＜支援的版本＞下指定的組態詳細資料來使用其中一個經背書的散發套件時，[Azure 平台 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) 才適用於執行 Linux 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2e004-159">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="2e004-160">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="2e004-160">Create a resource group</span></span>
<span data-ttu-id="2e004-161">資源群組會以邏輯方式將所有 Azure 資源 (例如虛擬網路和儲存體) 結合在一起以支援您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2e004-161">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="2e004-162">如需有關資源群組的詳細資訊，請參閱[資源群組概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2e004-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="2e004-163">在上傳您的自訂磁碟並建立 VM 之前，您必須先使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="2e004-163">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="2e004-164">下列範例會在 `westus` 位置建立名為 `myResourceGroup` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="2e004-164">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="2e004-165">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="2e004-165">Create a storage account</span></span>

<span data-ttu-id="2e004-166">使用 [az storage account create](/cli/azure/storage/account#create) 為自訂磁碟和 VM 建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2e004-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="2e004-167">您從自訂磁碟建立、具有非受控磁碟的任何 VM 都必須位於與該磁碟相同的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="2e004-167">Any VMs with unmanaged disks that you create from your custom disk need to be in the same storage account as that disk.</span></span> 

<span data-ttu-id="2e004-168">下列範例會在先前建立的資源群組中建立名為 `mystorageaccount` 的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="2e004-168">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="2e004-169">列出儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="2e004-169">List storage account keys</span></span>
<span data-ttu-id="2e004-170">Azure 會為每個儲存體帳戶產生兩個 512 位元的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2e004-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="2e004-171">對儲存體帳戶進行驗證時 (例如為了執行寫入作業)，就會使用這些存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2e004-171">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="2e004-172">從 [這裡](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)深入了解如何管理對儲存體的存取。</span><span class="sxs-lookup"><span data-stu-id="2e004-172">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="2e004-173">您使用 [az storage account keys list](/cli/azure/storage/account/keys#list) 來檢視存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="2e004-173">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="2e004-174">檢視您所建立儲存體帳戶的存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="2e004-174">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="2e004-175">輸出如下：</span><span class="sxs-lookup"><span data-stu-id="2e004-175">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="2e004-176">請記下 `key1` ，因為在接下來的步驟中，您將使用它來與您的儲存體帳戶互動。</span><span class="sxs-lookup"><span data-stu-id="2e004-176">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="2e004-177">建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="2e004-177">Create a storage container</span></span>
<span data-ttu-id="2e004-178">您可以在儲存體帳戶內建立容器來組織您的磁碟，方法與您建立不同目錄來以邏輯方式組織本機檔案系統相同。</span><span class="sxs-lookup"><span data-stu-id="2e004-178">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="2e004-179">儲存體帳戶可以包含任意數目的容器。</span><span class="sxs-lookup"><span data-stu-id="2e004-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="2e004-180">使用 [az storage container create](/cli/azure/storage/container#create) 來建立容器。</span><span class="sxs-lookup"><span data-stu-id="2e004-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="2e004-181">下列範例會建立名為 `mydisks` 的容器：</span><span class="sxs-lookup"><span data-stu-id="2e004-181">The following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="2e004-182">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="2e004-182">Upload VHD</span></span>
<span data-ttu-id="2e004-183">現在您可以使用 [az storage blob upload](/cli/azure/storage/blob#upload) 上傳您的自訂磁碟。</span><span class="sxs-lookup"><span data-stu-id="2e004-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="2e004-184">您上傳並將您的自訂磁碟儲存為分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="2e004-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="2e004-185">指定您的存取金鑰、您在上一個步驟中建立的容器，然後指定您本機電腦上自訂磁碟的路徑：</span><span class="sxs-lookup"><span data-stu-id="2e004-185">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-the-vm"></a><span data-ttu-id="2e004-186">建立 VM</span><span class="sxs-lookup"><span data-stu-id="2e004-186">Create the VM</span></span>
<span data-ttu-id="2e004-187">若要使用未受控磁碟來建立 VM，請使用 [az vm create](/cli/azure/vm#create) 指定磁碟的 URI (`--image`)。</span><span class="sxs-lookup"><span data-stu-id="2e004-187">To create a VM with unmanaged disks, specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2e004-188">下列範例會使用先前上傳的虛擬磁碟來建立名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="2e004-188">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

<span data-ttu-id="2e004-189">您需搭配 [az vm create](/cli/azure/vm#create) 指定 `--image` 參數，以指向您的自訂磁碟。</span><span class="sxs-lookup"><span data-stu-id="2e004-189">You specify the `--image` parameter with [az vm create](/cli/azure/vm#create) to point to your custom disk.</span></span> <span data-ttu-id="2e004-190">請確保 `--storage-account` 與儲存您自訂磁碟的儲存體帳戶相符。</span><span class="sxs-lookup"><span data-stu-id="2e004-190">Ensure that `--storage-account` matches the storage account where your custom disk is stored.</span></span> <span data-ttu-id="2e004-191">您不需使用與自訂磁碟相同的容器來儲存您的 VM。</span><span class="sxs-lookup"><span data-stu-id="2e004-191">You do not have to use the same container as the custom disk to store your VMs.</span></span> <span data-ttu-id="2e004-192">上傳您的自訂磁碟之前，請確定會使用與先前步驟中相同的方式來建立任何額外的容器。</span><span class="sxs-lookup"><span data-stu-id="2e004-192">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="2e004-193">下列範例會從您的自訂磁碟建立名為 `myVM` 的 VM：</span><span class="sxs-lookup"><span data-stu-id="2e004-193">The following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="2e004-194">您仍需指定或依據提示回答 **az vm create** 命令所需的所有其他參數，例如使用者名稱及 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="2e004-194">You still need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="2e004-195">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="2e004-195">Resource Manager template</span></span>
<span data-ttu-id="2e004-196">Azure Resource Manager 範本是「JavaScript 物件標記法」(JSON) 檔案，定義了您想要建置的環境。</span><span class="sxs-lookup"><span data-stu-id="2e004-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="2e004-197">範本會細分成不同的資源提供者，例如計算或網路。</span><span class="sxs-lookup"><span data-stu-id="2e004-197">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="2e004-198">您可以使用現有的範本或自行撰寫範本。</span><span class="sxs-lookup"><span data-stu-id="2e004-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="2e004-199">深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2e004-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="2e004-200">在範本的 `Microsoft.Compute/virtualMachines` 提供者內，您會有一個包含 VM 組態詳細資料的 `storageProfile` 節點。</span><span class="sxs-lookup"><span data-stu-id="2e004-200">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="2e004-201">兩個要編輯的主要參數為 `image` 和 `vhd` URI，分別指向您的自訂磁碟和新 VM 的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="2e004-201">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="2e004-202">以下顯示使用自訂磁碟的 JSON 範例：</span><span class="sxs-lookup"><span data-stu-id="2e004-202">The following shows an example of the JSON for using a custom disk:</span></span>

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

<span data-ttu-id="2e004-203">您可以使用[這個現有的範本以從自訂映像建立 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) 或閱讀[建立您自己的 Azure Resource Manager 範本](../../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="2e004-203">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="2e004-204">設定範本之後，請使用 [az group deployment create](/cli/azure/group/deployment#create) 來建立您的 VM。</span><span class="sxs-lookup"><span data-stu-id="2e004-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) to create your VMs.</span></span> <span data-ttu-id="2e004-205">請使用 `--template-uri` 參數來指定您 JSON 範本的 URI︰</span><span class="sxs-lookup"><span data-stu-id="2e004-205">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="2e004-206">如果您已在電腦本機儲存 JSON 檔案，則可以改用 `--template-file` 參數︰</span><span class="sxs-lookup"><span data-stu-id="2e004-206">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="2e004-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e004-207">Next steps</span></span>
<span data-ttu-id="2e004-208">在您備妥並上傳自訂虛擬磁碟之後，您可以深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2e004-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="2e004-209">您也可以 [將資料磁碟新增](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 至您的新 VM。</span><span class="sxs-lookup"><span data-stu-id="2e004-209">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="2e004-210">如果您需要存取在您的 VM 上執行的應用程式，請務必 [開啟連接埠和端點](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2e004-210">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

