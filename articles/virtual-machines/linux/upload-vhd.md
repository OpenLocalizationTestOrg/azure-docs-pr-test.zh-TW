---
title: "aaaUpload 或複製自訂的 Linux VM，使用 Azure CLI 2.0 |Microsoft 文件"
description: "上傳或複製自訂的虛擬機器使用 hello Resource Manager 部署模型和 hello Azure CLI 2.0"
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
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="f97e4-103">從自訂的磁碟以 hello Azure CLI 2.0 建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="f97e4-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="f97e4-104">本文章將示範如何 tooupload 自訂虛擬硬碟 (VHD) 或複製在 Azure 中現有的 VHD，並從 hello 自訂磁碟建立新的 Linux 虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="f97e4-105">您可以安裝和設定 Linux distro tooyour 需求，然後使用該 VHD tooquickly 建立新的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f97e4-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="f97e4-106">如果您想 toocreate 多個 Vm 從自訂磁碟，您應該從您的 VM 或 VHD 建立映像。</span><span class="sxs-lookup"><span data-stu-id="f97e4-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="f97e4-107">如需詳細資訊，請參閱[建立自訂映像的 Azure VM 使用 hello CLI](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="f97e4-108">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="f97e4-108">You have two options:</span></span>
* [<span data-ttu-id="f97e4-109">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="f97e4-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="f97e4-110">複製現有的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="f97e4-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="f97e4-111">快速命令</span><span class="sxs-lookup"><span data-stu-id="f97e4-111">Quick commands</span></span>

<span data-ttu-id="f97e4-112">當建立新的 VM 使用[az vm 建立](/cli/azure/vm#create)從自訂或特定磁碟您**附加**hello 磁碟 (-附加 os 磁碟) 而不是指定的自訂或 marketplace 映像 (-映像)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="f97e4-113">hello 下列範例會建立名為的 VM *myVM*使用 hello 受管理的名為磁碟*myManagedDisk*建立從自訂的 VHD:</span><span class="sxs-lookup"><span data-stu-id="f97e4-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="f97e4-114">需求</span><span class="sxs-lookup"><span data-stu-id="f97e4-114">Requirements</span></span>
<span data-ttu-id="f97e4-115">toocomplete hello 下列步驟，您需要：</span><span class="sxs-lookup"><span data-stu-id="f97e4-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="f97e4-116">一部已準備好用於 Azure 中的 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f97e4-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="f97e4-117">hello[準備 hello VM](#prepare-the-vm)這篇文章的章節將涵蓋如何 toofind distro 特定安裝資訊 hello Azure Linux 代理程式 (waagent) 才能正確地在 Azure 中的 hello VM toowork 以及您 toobe 無法 tooconnect使用 SSH tooit。</span><span class="sxs-lookup"><span data-stu-id="f97e4-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="f97e4-118">hello VHD 檔案從現有[支援 Azure 的 linux Linux 發佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(或參閱[非背書發佈資訊](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD 格式的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="f97e4-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="f97e4-119">VM 和 VHD toocreate 有多個工具：</span><span class="sxs-lookup"><span data-stu-id="f97e4-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="f97e4-120">安裝和設定[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU)或[KVM](http://www.linux-kvm.org/page/RunningKVM)，小心 toouse VHD 作為映像格式。</span><span class="sxs-lookup"><span data-stu-id="f97e4-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="f97e4-121">如有需要，您可以使用 **qemu-img convert** 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="f97e4-122">您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="f97e4-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f97e4-123">在 Azure 中不支援 hello 較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="f97e4-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="f97e4-124">當您建立 VM 時，指定 hello 格式 VHD。</span><span class="sxs-lookup"><span data-stu-id="f97e4-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="f97e4-125">如有需要您可以將轉換使用的 VHDX 磁碟 tooVHD [qemu img 轉換](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)或 hello [CONVERT-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f97e4-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="f97e4-126">此外，Azure 不支援將動態 Vhd 上, 傳，以便您需要 tooconvert 這類磁碟 toostatic Vhd 上傳之前。</span><span class="sxs-lookup"><span data-stu-id="f97e4-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="f97e4-127">您可以使用工具，例如[Azure VHD 公用程式 GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert 動態磁碟上傳 tooAzure hello 程序期間。</span><span class="sxs-lookup"><span data-stu-id="f97e4-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="f97e4-128">請確定您擁有 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f97e4-129">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="f97e4-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f97e4-130">範例參數名稱包含 myResourceGroup、mystorageaccount 和 mydisks。</span><span class="sxs-lookup"><span data-stu-id="f97e4-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="f97e4-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="f97e4-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="f97e4-132">準備 VM hello</span><span class="sxs-lookup"><span data-stu-id="f97e4-132">Prepare hello VM</span></span>

<span data-ttu-id="f97e4-133">Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="f97e4-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="f97e4-134">hello 下列文章會引導您完成 tooprepare hello Azure 所支援各種 Linux 散發套件的方式：</span><span class="sxs-lookup"><span data-stu-id="f97e4-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="f97e4-135">CentOS 型發行版本</span><span class="sxs-lookup"><span data-stu-id="f97e4-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f97e4-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="f97e4-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f97e4-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="f97e4-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f97e4-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="f97e4-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f97e4-139">SLES 和 openSUSE</span><span class="sxs-lookup"><span data-stu-id="f97e4-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f97e4-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f97e4-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f97e4-141">其他：非背書的發行版本</span><span class="sxs-lookup"><span data-stu-id="f97e4-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="f97e4-142">另請參閱 hello [Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)如需有關準備 Azure Linux 映像的多個一般秘訣。</span><span class="sxs-lookup"><span data-stu-id="f97e4-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f97e4-143">hello [Azure 平台 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)適用於僅當其中一個 hello 背書分佈會搭配 hello 設定詳細資料，指定在支援版本底下執行 Linux 的 tooVMs [Linux 上支援 Azure 的 Linux分佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="f97e4-144">選項 1：上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="f97e4-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="f97e4-145">您可以上傳已在本機電腦上執行或從另一個雲端匯出的自訂 VHD。</span><span class="sxs-lookup"><span data-stu-id="f97e4-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="f97e4-146">toouse hello VHD toocreate 新的 Azure VM，您需要 tooupload hello VHD tooa 儲存體帳戶，並從 hello VHD 建立受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f97e4-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="f97e4-147">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="f97e4-147">Create a resource group</span></span>

<span data-ttu-id="f97e4-148">上傳您自訂的磁碟和之前建立的 Vm，您必須先 toocreate 的資源群組與[az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="f97e4-149">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置： [Azure 受管理磁碟概觀](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f97e4-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="f97e4-150">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f97e4-150">Create a storage account</span></span>

<span data-ttu-id="f97e4-151">使用 [az storage account create](/cli/azure/storage/account#create) 為自訂磁碟和 VM 建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f97e4-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="f97e4-152">hello 下列範例會建立名為的儲存體帳戶*mystorageaccount* hello 先前建立的資源群組中：</span><span class="sxs-lookup"><span data-stu-id="f97e4-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="f97e4-153">列出儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="f97e4-153">List storage account keys</span></span>
<span data-ttu-id="f97e4-154">Azure 會為每個儲存體帳戶產生兩個 512 位元的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="f97e4-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="f97e4-155">驗證 toohello 儲存體帳戶，例如一波波的寫入作業時，會使用這些存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="f97e4-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="f97e4-156">深入了解[管理存取 toostorage 這裡](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="f97e4-157">檢視與 hello 便捷鍵[az 儲存體帳戶金鑰清單](/cli/azure/storage/account/keys#list)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="f97e4-158">檢視 hello hello 您所建立的儲存體帳戶的存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="f97e4-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="f97e4-159">hello 輸出如下：</span><span class="sxs-lookup"><span data-stu-id="f97e4-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="f97e4-160">請記下**key1**因為您可以將 toointeract hello 後續步驟中儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f97e4-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="f97e4-161">建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="f97e4-161">Create a storage container</span></span>
<span data-ttu-id="f97e4-162">在 hello 中建立不同的目錄 toologically 相同方式，組織您的本機檔案系統，您建立儲存體帳戶 tooorganize 內的容器，您的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f97e4-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="f97e4-163">儲存體帳戶可以包含任意數目的容器。</span><span class="sxs-lookup"><span data-stu-id="f97e4-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="f97e4-164">使用 [az storage container create](/cli/azure/storage/container#create) 來建立容器。</span><span class="sxs-lookup"><span data-stu-id="f97e4-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="f97e4-165">hello 下列範例會建立名為的容器*mydisks*:</span><span class="sxs-lookup"><span data-stu-id="f97e4-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="f97e4-166">上傳 VHD hello</span><span class="sxs-lookup"><span data-stu-id="f97e4-166">Upload hello VHD</span></span>
<span data-ttu-id="f97e4-167">現在您可以使用 [az storage blob upload](/cli/azure/storage/blob#upload) 上傳您的自訂磁碟。</span><span class="sxs-lookup"><span data-stu-id="f97e4-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="f97e4-168">您上傳並將您的自訂磁碟儲存為分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="f97e4-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="f97e4-169">指定您的存取金鑰，您在 hello 前一個步驟中建立的 hello 容器，然後 hello 路徑 toohello 自訂磁碟在本機電腦上：</span><span class="sxs-lookup"><span data-stu-id="f97e4-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="f97e4-170">正在上傳 hello VHD，可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="f97e4-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="f97e4-171">建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="f97e4-171">Create a managed disk</span></span>


<span data-ttu-id="f97e4-172">建立受管理的磁碟 hello VHD 使用[az 磁碟建立](/cli/azure/disk#create)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="f97e4-173">hello 下列範例會建立名為受管理的磁碟*myManagedDisk*從 hello VHD 上傳 tooyour 名為儲存體帳戶和容器：</span><span class="sxs-lookup"><span data-stu-id="f97e4-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="f97e4-174">選項 2：複製現有的 VM</span><span class="sxs-lookup"><span data-stu-id="f97e4-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="f97e4-175">您也可以建立 hello 自訂的 Azure，然後複製 hello OS 磁碟 VM，並將它附加新 VM toocreate tooa 另一份複本。</span><span class="sxs-lookup"><span data-stu-id="f97e4-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="f97e4-176">這是正常進行測試，但如果您想要 toouse 現有的 Azure VM hello 模型為多個新的 Vm，您實際上應該建立**映像**改為。</span><span class="sxs-lookup"><span data-stu-id="f97e4-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="f97e4-177">如需有關如何從現有的 Azure VM 建立映像的詳細資訊，請參閱[建立 Azure VM 使用 hello CLI 的自訂映像](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="f97e4-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="f97e4-178">建立快照集</span><span class="sxs-lookup"><span data-stu-id="f97e4-178">Create a snapshot</span></span>

<span data-ttu-id="f97e4-179">這個範例會在名為 myResourceGroup 資源群組中建立名為 myVM 的 VM 快照集，並建立名為 osDiskSnapshot 的快照集。</span><span class="sxs-lookup"><span data-stu-id="f97e4-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="f97e4-180">建立 hello 受管理的磁碟</span><span class="sxs-lookup"><span data-stu-id="f97e4-180">Create hello managed disk</span></span>

<span data-ttu-id="f97e4-181">建立新的受管理的磁碟從 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="f97e4-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="f97e4-182">取得 hello 識別碼 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="f97e4-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="f97e4-183">在此範例中，名為 hello 快照*osDiskSnapshot* hello，且*myResourceGroup*資源群組。</span><span class="sxs-lookup"><span data-stu-id="f97e4-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="f97e4-184">建立 hello 受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f97e4-184">Create hello managed disk.</span></span> <span data-ttu-id="f97e4-185">在此範例中，我們將從快照集中建立名為 myManagedDisk 的受控磁碟，其在標準儲存體中大小為 128 GB。</span><span class="sxs-lookup"><span data-stu-id="f97e4-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="f97e4-186">建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="f97e4-186">Create hello VM</span></span>

<span data-ttu-id="f97e4-187">現在，建立具有您 VM [az vm 建立](/cli/azure/vm#create)與附加 (-附加 os 磁碟) hello 管理 hello OS 磁碟的磁碟。</span><span class="sxs-lookup"><span data-stu-id="f97e4-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="f97e4-188">hello 下列範例會建立名為的 VM *myNewVM*使用 hello 管理從您上傳的 VHD 建立磁碟：</span><span class="sxs-lookup"><span data-stu-id="f97e4-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="f97e4-189">您應該能夠 tooSSH hello VM 到 hello 來源 VM 使用 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="f97e4-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f97e4-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f97e4-190">Next steps</span></span>
<span data-ttu-id="f97e4-191">在您備妥並上傳自訂虛擬磁碟之後，您可以深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f97e4-192">您也可以太[新增資料磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)tooyour 新 Vm。</span><span class="sxs-lookup"><span data-stu-id="f97e4-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="f97e4-193">如果您有 Vm 上執行，您需要 tooaccess 應用程式，請務必太[開啟連接埠和端點](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f97e4-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

