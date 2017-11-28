---
title: "使用 Azure CLI 2.0 上傳或複製自訂的 Linux VM | Microsoft Docs"
description: "使用 Resource Manager 部署模型和 Azure CLI 2.0 來上傳或複製自訂的虛擬機器"
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
ms.openlocfilehash: 7c297725c26ea6c44403a10ecdcc3542f89f10b4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="e2341-103">使用 Azure CLI 2.0 從自訂磁碟建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="e2341-103">Create a Linux VM from custom disk with the Azure CLI 2.0</span></span>

<!-- rename to create-vm-specialized -->

<span data-ttu-id="e2341-104">本文將說明如何在 Azure 中上傳自訂的虛擬硬碟 (VHD) 或複製現有的 VHD，以及從自訂磁碟建立新的 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="e2341-104">This article shows you how to upload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from the custom disk.</span></span> <span data-ttu-id="e2341-105">您可以安裝並設定 Linux 發行版本以符合您的需求，然後使用該 VHD 快速建立新的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e2341-105">You can install and configure a Linux distro to your requirements and then use that VHD to quickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="e2341-106">如果您想要從自訂磁碟建立多個 VM，就應該從您的 VM 或 VHD 建立映像。</span><span class="sxs-lookup"><span data-stu-id="e2341-106">If you want to create multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="e2341-107">如需詳細資訊，請參閱[使用 CLI 建立 Azure VM 的自訂映像](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="e2341-107">For more information, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="e2341-108">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="e2341-108">You have two options:</span></span>
* [<span data-ttu-id="e2341-109">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="e2341-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="e2341-110">複製現有的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="e2341-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="e2341-111">快速命令</span><span class="sxs-lookup"><span data-stu-id="e2341-111">Quick commands</span></span>

<span data-ttu-id="e2341-112">使用 [az vm create](/cli/azure/vm#create) 從自訂或特定磁碟建立新的 VM 時，您需要**連接**磁碟 (--attach-os-disk)，而不是指定自訂或 Marketplace 映像 (--image)。</span><span class="sxs-lookup"><span data-stu-id="e2341-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** the disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="e2341-113">下列範例會使用從您自訂 VHD 建立的受控磁碟 (名為 *myManagedDisk*) 來建立名為 *myVM* 的 VM：</span><span class="sxs-lookup"><span data-stu-id="e2341-113">The following example creates a VM named *myVM* using the managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="e2341-114">需求</span><span class="sxs-lookup"><span data-stu-id="e2341-114">Requirements</span></span>
<span data-ttu-id="e2341-115">若要完成下列步驟，您需要：</span><span class="sxs-lookup"><span data-stu-id="e2341-115">To complete the following steps, you need:</span></span>

* <span data-ttu-id="e2341-116">一部已準備好用於 Azure 中的 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e2341-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="e2341-117">本文的[準備 VM](#prepare-the-vm) 一節將說明如何尋找關於安裝 Azure Linux 代理程式 (waagent) 的發行版本特有資訊，必須有此資訊，VM 才能在 Azure 中正常運作，而您才能使用 SSH 來與它連線。</span><span class="sxs-lookup"><span data-stu-id="e2341-117">The [Prepare the VM](#prepare-the-vm) section of this article covers how to find distro specific information on installing the Azure Linux Agent (waagent) which is required for the VM to work properly in Azure and for you to be able to connect to it using SSH.</span></span>
* <span data-ttu-id="e2341-118">以 VHD 格式從現有[經 Azure 背書的 Linux 發行版本](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (或者，請參閱[非背書發行版本的資訊](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) 到虛擬磁碟的 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="e2341-118">The VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="e2341-119">有多項工具可用來建立 VM 和 VHD：</span><span class="sxs-lookup"><span data-stu-id="e2341-119">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="e2341-120">安裝和設定 [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 或 [KVM](http://www.linux-kvm.org/page/RunningKVM)，並小心使用 VHD 做為您的映像格式。</span><span class="sxs-lookup"><span data-stu-id="e2341-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="e2341-121">如有需要，您可以使用 **qemu-img convert** 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="e2341-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="e2341-122">您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="e2341-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e2341-123">Azure 不支援較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="e2341-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="e2341-124">當您建立 VM 時，請指定 VHD 做為格式。</span><span class="sxs-lookup"><span data-stu-id="e2341-124">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="e2341-125">如有需要，您可以使用 [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 或 [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell Cmdlet，將 VHDX 磁碟轉換為 VHD。</span><span class="sxs-lookup"><span data-stu-id="e2341-125">If needed, you can convert VHDX disks to VHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="e2341-126">此外，Azure 不支援上傳動態 VHD，因此您必須將此類磁碟轉換成靜態 VHD 再上傳。</span><span class="sxs-lookup"><span data-stu-id="e2341-126">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="e2341-127">您可以在上傳至 Azure 的期間使用 [適用於 GO 的 Azure VHD 公用程式](https://github.com/Microsoft/azure-vhd-utils-for-go) 之類的工具來轉換動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="e2341-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 


* <span data-ttu-id="e2341-128">請確定您已安裝最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2) 並使用 [az login](/cli/azure/#login) 登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2341-128">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e2341-129">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="e2341-129">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e2341-130">範例參數名稱包含 myResourceGroup、mystorageaccount 和 mydisks。</span><span class="sxs-lookup"><span data-stu-id="e2341-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="e2341-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="e2341-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="e2341-132">準備 VM</span><span class="sxs-lookup"><span data-stu-id="e2341-132">Prepare the VM</span></span>

<span data-ttu-id="e2341-133">Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="e2341-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="e2341-134">下列文章會逐步引導您了解如何準備 Azure 上支援的各種 Linux 散發套件：</span><span class="sxs-lookup"><span data-stu-id="e2341-134">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="e2341-135">CentOS 型發行版本</span><span class="sxs-lookup"><span data-stu-id="e2341-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e2341-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="e2341-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e2341-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="e2341-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e2341-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="e2341-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e2341-139">SLES 和 openSUSE</span><span class="sxs-lookup"><span data-stu-id="e2341-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e2341-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e2341-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e2341-141">其他：非背書的發行版本</span><span class="sxs-lookup"><span data-stu-id="e2341-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="e2341-142">如需更多為 Azure 準備 Linux 映像的一般秘訣，另請參閱 [Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)。</span><span class="sxs-lookup"><span data-stu-id="e2341-142">Also see the [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e2341-143">只有在搭配[經 Azure 背書之 Linux 散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中＜支援的版本＞下指定的組態詳細資料來使用其中一個經背書的散發套件時，[Azure 平台 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) 才適用於執行 Linux 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e2341-143">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="e2341-144">選項 1：上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="e2341-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="e2341-145">您可以上傳已在本機電腦上執行或從另一個雲端匯出的自訂 VHD。</span><span class="sxs-lookup"><span data-stu-id="e2341-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="e2341-146">若要使用 VHD 來建立新的 Azure VM，您需要將 VHD 上傳至儲存體帳戶，並從 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="e2341-146">To use the VHD to create a new Azure VM, you need to upload the VHD to a storage account and create a managed disk from the VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="e2341-147">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="e2341-147">Create a resource group</span></span>

<span data-ttu-id="e2341-148">在上傳您的自訂磁碟並建立 VM 之前，您必須先使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="e2341-148">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="e2341-149">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組：[Azure 受控磁碟概觀](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e2341-149">The following example creates a resource group named *myResourceGroup* in the *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="e2341-150">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e2341-150">Create a storage account</span></span>

<span data-ttu-id="e2341-151">使用 [az storage account create](/cli/azure/storage/account#create) 為自訂磁碟和 VM 建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2341-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="e2341-152">下列範例會在先前建立的資源群組中建立名為 mystorageaccount 的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="e2341-152">The following example creates a storage account named *mystorageaccount* in the resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="e2341-153">列出儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="e2341-153">List storage account keys</span></span>
<span data-ttu-id="e2341-154">Azure 會為每個儲存體帳戶產生兩個 512 位元的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="e2341-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="e2341-155">對儲存體帳戶進行驗證時 (例如，執行寫入作業)，就會使用這些存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="e2341-155">These access keys are used when authenticating to the storage account, like carrying out write operations.</span></span> <span data-ttu-id="e2341-156">從 [這裡](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)深入了解如何管理對儲存體的存取。</span><span class="sxs-lookup"><span data-stu-id="e2341-156">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="e2341-157">您使用 [az storage account keys list](/cli/azure/storage/account/keys#list) 來檢視存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="e2341-157">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="e2341-158">檢視您所建立儲存體帳戶的存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="e2341-158">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="e2341-159">輸出如下：</span><span class="sxs-lookup"><span data-stu-id="e2341-159">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="e2341-160">請記下 **key1**，因為在接下來的步驟中，您將使用它來與您的儲存體帳戶互動。</span><span class="sxs-lookup"><span data-stu-id="e2341-160">Make a note of **key1** as you will use it to interact with your storage account in the next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="e2341-161">建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="e2341-161">Create a storage container</span></span>
<span data-ttu-id="e2341-162">您可以在儲存體帳戶內建立容器來組織您的磁碟，方法與您建立不同目錄來以邏輯方式組織本機檔案系統相同。</span><span class="sxs-lookup"><span data-stu-id="e2341-162">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="e2341-163">儲存體帳戶可以包含任意數目的容器。</span><span class="sxs-lookup"><span data-stu-id="e2341-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="e2341-164">使用 [az storage container create](/cli/azure/storage/container#create) 來建立容器。</span><span class="sxs-lookup"><span data-stu-id="e2341-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="e2341-165">下列範例會建立名為 mydisks 的容器：</span><span class="sxs-lookup"><span data-stu-id="e2341-165">The following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-the-vhd"></a><span data-ttu-id="e2341-166">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="e2341-166">Upload the VHD</span></span>
<span data-ttu-id="e2341-167">現在您可以使用 [az storage blob upload](/cli/azure/storage/blob#upload) 上傳您的自訂磁碟。</span><span class="sxs-lookup"><span data-stu-id="e2341-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="e2341-168">您上傳並將您的自訂磁碟儲存為分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="e2341-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="e2341-169">指定您的存取金鑰、您在上一個步驟中建立的容器，然後指定您本機電腦上自訂磁碟的路徑：</span><span class="sxs-lookup"><span data-stu-id="e2341-169">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="e2341-170">上傳 VHD，可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="e2341-170">Uploading the VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="e2341-171">建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="e2341-171">Create a managed disk</span></span>


<span data-ttu-id="e2341-172">使用 [az disk create](/cli/azure/disk#create) 從 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="e2341-172">Create a managed disk from the VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="e2341-173">下列範例會從您上傳至具名儲存體帳戶和容器的 VHD 建立名為 myManagedDisk 的受控磁碟：</span><span class="sxs-lookup"><span data-stu-id="e2341-173">The following example creates a managed disk named *myManagedDisk* from the VHD you uploaded to your named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="e2341-174">選項 2：複製現有的 VM</span><span class="sxs-lookup"><span data-stu-id="e2341-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="e2341-175">您可以也在 Azure 中建立自訂的 VM，然後複製 OS 磁碟並將它連接到新的 VM，以建立另一個複本。</span><span class="sxs-lookup"><span data-stu-id="e2341-175">You can also create the customized VM in Azure and then copy the OS disk and attach it to a new VM to create another copy.</span></span> <span data-ttu-id="e2341-176">這適合用來測試，但如果您想要使用現有的 Azure VM 作為多個新 VM 的模型，則您實際上應改為建立**映像**。</span><span class="sxs-lookup"><span data-stu-id="e2341-176">This is fine for testing, but if you want to use an existing Azure VM as the model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="e2341-177">如需如何從現有 Azure VM 建立映像的詳細資訊，請參閱[使用 CLI 建立 Azure VM 的自訂映像](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="e2341-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="e2341-178">建立快照集</span><span class="sxs-lookup"><span data-stu-id="e2341-178">Create a snapshot</span></span>

<span data-ttu-id="e2341-179">這個範例會在名為 myResourceGroup 資源群組中建立名為 myVM 的 VM 快照集，並建立名為 osDiskSnapshot 的快照集。</span><span class="sxs-lookup"><span data-stu-id="e2341-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-the-managed-disk"></a><span data-ttu-id="e2341-180">建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="e2341-180">Create the managed disk</span></span>

<span data-ttu-id="e2341-181">從快照集建立新的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="e2341-181">Create a new managed disk from the snapshot.</span></span>

<span data-ttu-id="e2341-182">取得快照集的識別碼。</span><span class="sxs-lookup"><span data-stu-id="e2341-182">Get the ID of the snapshot.</span></span> <span data-ttu-id="e2341-183">在此範例中，快照集的名稱為 osDiskSnapshot 且位於 myResourceGroup 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="e2341-183">In this example, the snapshot is named *osDiskSnapshot* and it is in the *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="e2341-184">建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="e2341-184">Create the managed disk.</span></span> <span data-ttu-id="e2341-185">在此範例中，我們將從快照集中建立名為 myManagedDisk 的受控磁碟，其在標準儲存體中大小為 128 GB。</span><span class="sxs-lookup"><span data-stu-id="e2341-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-the-vm"></a><span data-ttu-id="e2341-186">建立 VM</span><span class="sxs-lookup"><span data-stu-id="e2341-186">Create the VM</span></span>

<span data-ttu-id="e2341-187">現在，使用 [az vm create](/cli/azure/vm#create) 建立您的 VM，並連接 (--attach-os-disk) 受控磁碟作為 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="e2341-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) the managed disk as the OS disk.</span></span> <span data-ttu-id="e2341-188">下列範例會使用從您上傳之 VHD 建立的受控磁碟來建立名為 myNewVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="e2341-188">The following example creates a VM named *myNewVM* using the managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="e2341-189">您應該能夠使用來源 VM 的認證，SSH 到 VM。</span><span class="sxs-lookup"><span data-stu-id="e2341-189">You should be able to SSH into the VM using the credentials from the source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e2341-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2341-190">Next steps</span></span>
<span data-ttu-id="e2341-191">在您備妥並上傳自訂虛擬磁碟之後，您可以深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e2341-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e2341-192">您也可以 [將資料磁碟新增](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 至您的新 VM。</span><span class="sxs-lookup"><span data-stu-id="e2341-192">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="e2341-193">如果您需要存取在您的 VM 上執行的應用程式，請務必 [開啟連接埠和端點](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e2341-193">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

