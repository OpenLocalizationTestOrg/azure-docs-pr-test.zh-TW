---
title: "建立 Linux VHD 並上傳至 Azure | Microsoft Docs"
description: "使用傳統部署模型來建立及上傳包含 Linux 作業系統的 Azure 虛擬硬碟 (VHD)。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 23c30c954875598ce3e01db137b0ef8cda9779f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-the-linux-operating-system"></a><span data-ttu-id="26219-103">建立及上傳包含 Linux 作業系統的虛擬硬碟</span><span class="sxs-lookup"><span data-stu-id="26219-103">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="26219-104">Azure 建立和處理資源的部署模型有二種： [Resource Manager 和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="26219-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="26219-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="26219-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="26219-106">Microsoft 建議讓大部分的新部署使用 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="26219-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="26219-107">您也可以[使用 Azure Resource Manager 上傳自訂磁碟映像](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="26219-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="26219-108">本文說明如何建立及上傳虛擬硬碟 (VHD)，以便用它做為您自己的映像，在 Azure 中建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="26219-108">This article shows you how to create and upload a virtual hard disk (VHD) so you can use it as your own image to create virtual machines in Azure.</span></span> <span data-ttu-id="26219-109">了解如何準備作業系統，以便使用它根據該映像建立多部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="26219-109">Learn how to prepare the operating system so you can use it to create multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="26219-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="26219-110">Prerequisites</span></span>
<span data-ttu-id="26219-111">本文假設您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="26219-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="26219-112">**以 .vhd 檔案安裝的 Linux 作業系統** - 您已經以 VHD 格式將 [Azure 背書的 Linux 散發套件](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (或參閱[非背書散發套件的資訊](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) 安裝到虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="26219-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="26219-113">有多項工具可用來建立 VM 和 VHD：</span><span class="sxs-lookup"><span data-stu-id="26219-113">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="26219-114">安裝和設定 [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) 或 [KVM](http://www.linux-kvm.org/page/RunningKVM)，並小心使用 VHD 做為您的映像格式。</span><span class="sxs-lookup"><span data-stu-id="26219-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="26219-115">如有需要，您可以使用 `qemu-img convert` 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)。</span><span class="sxs-lookup"><span data-stu-id="26219-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="26219-116">您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="26219-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="26219-117">Azure 不支援較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="26219-117">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="26219-118">當您建立 VM 時，請指定 VHD 做為格式。</span><span class="sxs-lookup"><span data-stu-id="26219-118">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="26219-119">如有需要，您可以使用 [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) 或 [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell Cmdlet 將 VHDX 磁碟轉換為 VHD。</span><span class="sxs-lookup"><span data-stu-id="26219-119">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="26219-120">此外，Azure 不支援上傳動態 VHD，因此您必須將此類磁碟轉換成靜態 VHD 再上傳。</span><span class="sxs-lookup"><span data-stu-id="26219-120">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="26219-121">您可以在上傳至 Azure 的期間使用 [適用於 GO 的 Azure VHD 公用程式](https://github.com/Microsoft/azure-vhd-utils-for-go) 之類的工具來轉換動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="26219-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>

* <span data-ttu-id="26219-122">**Azure 命令列介面** - 安裝最新的 [Azure 命令列介面](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) 來上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="26219-122">**Azure Command-line Interface** - Install the latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to upload the VHD.</span></span>

<span data-ttu-id="26219-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="26219-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-the-image-to-be-uploaded"></a><span data-ttu-id="26219-124">步驟 1：準備要上傳的映像</span><span class="sxs-lookup"><span data-stu-id="26219-124">Step 1: Prepare the image to be uploaded</span></span>
<span data-ttu-id="26219-125">Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="26219-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="26219-126">下列文章會逐步引導您了解如何準備 Azure 上支援的各種 Linux 散發套件：</span><span class="sxs-lookup"><span data-stu-id="26219-126">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="26219-127">完成下列指南中的步驟並已有一個準備好可上傳到 Azure 的 VHD 檔案之後，請回到這裡：</span><span class="sxs-lookup"><span data-stu-id="26219-127">After you complete the steps in the following guides, come back here once you have a VHD file that is ready to upload to Azure:</span></span>

* <span data-ttu-id="26219-128">**[CentOS 型散發套件](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="26219-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="26219-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="26219-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="26219-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="26219-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="26219-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="26219-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="26219-132">**[SLES 和 openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="26219-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="26219-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="26219-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="26219-134">**[其他：非背書散發套件](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="26219-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="26219-135">只有使用其中一個背書散發套件搭配[經 Azure 背書之配送映像上的 Linux](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中＜支援的版本＞底下指定的組態詳細資料時，Azure 平台 SLA 才適用於執行 Linux OS 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="26219-135">The Azure platform SLA applies to virtual machines running the Linux OS only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="26219-136">Azure 映像庫中的所有 Linux 散發套件，皆為使用必要組態的背書散發套件。</span><span class="sxs-lookup"><span data-stu-id="26219-136">All Linux distributions in the Azure image gallery are endorsed distributions with the required configuration.</span></span>
> 
> 

<span data-ttu-id="26219-137">如需有關為 Azure 準備 Linux 映像的更多一般秘訣，另請參閱 **[Linux 安裝注意事項](../create-upload-generic.md#general-linux-installation-notes)**。</span><span class="sxs-lookup"><span data-stu-id="26219-137">Also see the **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="26219-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="26219-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-the-connection-to-azure"></a><span data-ttu-id="26219-139">步驟 2：準備與 Azure 的連接</span><span class="sxs-lookup"><span data-stu-id="26219-139">Step 2: Prepare the connection to Azure</span></span>
<span data-ttu-id="26219-140">確定您是在傳統部署模型中使用 Azure CLI (`azure config mode asm`)，然後登入您的帳戶︰</span><span class="sxs-lookup"><span data-stu-id="26219-140">Make sure you are using the Azure CLI in the classic deployment model (`azure config mode asm`), then log in to your account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="26219-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="26219-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-the-image-to-azure"></a><span data-ttu-id="26219-142">步驟 3：將映像上傳至 Azure</span><span class="sxs-lookup"><span data-stu-id="26219-142">Step 3: Upload the image to Azure</span></span>
<span data-ttu-id="26219-143">您需要一個可供上傳 VHD 檔案的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="26219-143">You need a storage account to upload your VHD file to.</span></span> <span data-ttu-id="26219-144">您可以選取現有的儲存體帳戶或[建立新帳戶](../../../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="26219-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="26219-145">使用 Azure CLI 上傳映像，方法是使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="26219-145">Use the Azure CLI to upload the image by using the following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="26219-146">在上述範例中︰</span><span class="sxs-lookup"><span data-stu-id="26219-146">In the previous example:</span></span>

* <span data-ttu-id="26219-147">**BlobStorageURL** 是您打算使用的儲存體帳戶 URL</span><span class="sxs-lookup"><span data-stu-id="26219-147">**BlobStorageURL** is the URL for the storage account you plan to use</span></span>
* <span data-ttu-id="26219-148">**YourImagesFolder** 是 Blob 儲存體內您要用來儲存映像的容器</span><span class="sxs-lookup"><span data-stu-id="26219-148">**YourImagesFolder** is the container within blob storage where you want to store your images</span></span>
* <span data-ttu-id="26219-149">**VHDName** 是入口網站中用來識別虛擬硬碟的顯示標籤。</span><span class="sxs-lookup"><span data-stu-id="26219-149">**VHDName** is the label that appears in portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="26219-150">**PathToVHDFile** 是 .vhd 檔案在您電腦上的完整路徑和名稱。</span><span class="sxs-lookup"><span data-stu-id="26219-150">**PathToVHDFile** is the full path and name of the .vhd file on your machine.</span></span>

<span data-ttu-id="26219-151">以下顯示完整的範例：</span><span class="sxs-lookup"><span data-stu-id="26219-151">The following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-the-image"></a><span data-ttu-id="26219-152">步驟 4：從映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="26219-152">Step 4: Create a VM from the image</span></span>
<span data-ttu-id="26219-153">您使用 `azure vm create` 以和一般 VM 相同的方式建立 VM。</span><span class="sxs-lookup"><span data-stu-id="26219-153">You create a VM using `azure vm create` in the same way as a regular VM.</span></span> <span data-ttu-id="26219-154">指定您在前一個步驟中提供給映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="26219-154">Specify the name you gave your image in the previous step.</span></span> <span data-ttu-id="26219-155">在下列範例中，我們會使用在前一個步驟中提供的 **myImage** 映像名稱：</span><span class="sxs-lookup"><span data-stu-id="26219-155">In the following example, we use the **myImage** image name given in the previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="26219-156">若要建立您自己的 VM，請提供您自己的使用者名稱 + 密碼、位置、DNS 名稱，以及映像名稱。</span><span class="sxs-lookup"><span data-stu-id="26219-156">To create your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26219-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26219-157">Next steps</span></span>
<span data-ttu-id="26219-158">如需詳細資訊，請參閱 [Azure 傳統部署模型的 Azure CLI 參考](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="26219-158">For more information, see [Azure CLI reference for the Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare the image to be uploaded]:#prepimage
[Step 2: Prepare the connection to Azure]:#connect
[Step 3: Upload the image to Azure]:#upload
