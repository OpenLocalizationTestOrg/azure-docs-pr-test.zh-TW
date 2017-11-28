---
title: "aaaCreate 並上傳 Linux VHD tooAzure |Microsoft 文件"
description: "建立及上傳 Azure 虛擬硬碟 (VHD)，其中包含使用 hello 傳統部署模型將 hello Linux 作業系統"
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
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="bc45c-103">建立和上傳的虛擬硬碟包含 hello Linux 作業系統</span><span class="sxs-lookup"><span data-stu-id="bc45c-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="bc45c-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="bc45c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bc45c-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="bc45c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="bc45c-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="bc45c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="bc45c-107">您也可以[使用 Azure Resource Manager 上傳自訂磁碟映像](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bc45c-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="bc45c-108">本文章將示範如何在 toocreate 和上傳虛擬硬碟 (VHD)，您可以將它當做自己映像 toocreate 在 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc45c-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="bc45c-109">了解如何 tooprepare hello 作業系統讓您可以使用它 toocreate 多部虛擬機器基礎映像上。</span><span class="sxs-lookup"><span data-stu-id="bc45c-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="bc45c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bc45c-110">Prerequisites</span></span>
<span data-ttu-id="bc45c-111">本文假設您有下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="bc45c-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="bc45c-112">**安裝.vhd 檔案中的 Linux 作業系統**-您已安裝[支援 Azure 的 linux Linux 發佈](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(或參閱[非背書發佈資訊](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa 虛擬磁碟hello VHD 格式。</span><span class="sxs-lookup"><span data-stu-id="bc45c-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="bc45c-113">VM 和 VHD toocreate 有多個工具：</span><span class="sxs-lookup"><span data-stu-id="bc45c-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="bc45c-114">安裝和設定[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU)或[KVM](http://www.linux-kvm.org/page/RunningKVM)，小心 toouse VHD 作為映像格式。</span><span class="sxs-lookup"><span data-stu-id="bc45c-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="bc45c-115">如有需要，您可以使用 `qemu-img convert` 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)。</span><span class="sxs-lookup"><span data-stu-id="bc45c-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="bc45c-116">您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="bc45c-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="bc45c-117">在 Azure 中不支援 hello 較新的 VHDX 格式。</span><span class="sxs-lookup"><span data-stu-id="bc45c-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="bc45c-118">當您建立 VM 時，指定 hello 格式 VHD。</span><span class="sxs-lookup"><span data-stu-id="bc45c-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="bc45c-119">如有需要您可以將轉換使用的 VHDX 磁碟 tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)或 hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bc45c-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="bc45c-120">此外，Azure 不支援將動態 Vhd 上, 傳，以便您需要 tooconvert 這類磁碟 toostatic Vhd 上傳之前。</span><span class="sxs-lookup"><span data-stu-id="bc45c-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="bc45c-121">您可以使用工具，例如[Azure VHD 公用程式 GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert 動態磁碟上傳 tooAzure hello 程序期間。</span><span class="sxs-lookup"><span data-stu-id="bc45c-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="bc45c-122">**Azure 命令列介面**-最新安裝 hello [Azure 命令列介面](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)tooupload hello VHD。</span><span class="sxs-lookup"><span data-stu-id="bc45c-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="bc45c-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="bc45c-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="bc45c-124">步驟 1： 準備上傳的 hello 映像 toobe</span><span class="sxs-lookup"><span data-stu-id="bc45c-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="bc45c-125">Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="bc45c-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="bc45c-126">hello 下列文章會引導您完成 tooprepare hello Azure 所支援各種 Linux 散發套件的方式。</span><span class="sxs-lookup"><span data-stu-id="bc45c-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="bc45c-127">完成 hello 下列指南中的 hello 步驟之後，再回到這裡之後準備 tooupload tooAzure 的 VHD 檔案：</span><span class="sxs-lookup"><span data-stu-id="bc45c-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="bc45c-128">**[CentOS 型散發套件](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="bc45c-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="bc45c-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="bc45c-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="bc45c-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="bc45c-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="bc45c-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="bc45c-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="bc45c-132">**[SLES 和 openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="bc45c-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="bc45c-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="bc45c-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="bc45c-134">**[其他：非背書散發套件](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="bc45c-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="bc45c-135">hello Azure 平台 SLA 套用 toovirtual 機器中執行 Linux 作業系統，其中一個 hello 背書分佈時，才會搭配 hello 設定詳細資料，以指定在支援版本的 hello [Linux Azure-Endorsed 發佈](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bc45c-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="bc45c-136">Hello Azure 映像庫中的所有 Linux 散發套件都是背書分佈利用 hello 必要的設定。</span><span class="sxs-lookup"><span data-stu-id="bc45c-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="bc45c-137">另請參閱 hello  **[Linux 安裝注意事項](../create-upload-generic.md#general-linux-installation-notes)**如需有關準備 Azure Linux 映像的多個一般秘訣。</span><span class="sxs-lookup"><span data-stu-id="bc45c-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="bc45c-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="bc45c-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="bc45c-139">步驟 2： 準備 hello 連接 tooAzure</span><span class="sxs-lookup"><span data-stu-id="bc45c-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="bc45c-140">請確定您使用 hello 傳統部署模型中的 hello Azure CLI (`azure config mode asm`)，然後登入 tooyour 帳戶：</span><span class="sxs-lookup"><span data-stu-id="bc45c-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="bc45c-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="bc45c-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="bc45c-142">步驟 3： 上傳 hello 映像 tooAzure</span><span class="sxs-lookup"><span data-stu-id="bc45c-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="bc45c-143">您需要儲存體帳戶 tooupload 您的 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="bc45c-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="bc45c-144">您可以選取現有的儲存體帳戶或[建立新帳戶](../../../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="bc45c-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="bc45c-145">使用下列命令的 hello 使用 hello Azure CLI tooupload hello 映像：</span><span class="sxs-lookup"><span data-stu-id="bc45c-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="bc45c-146">在 hello 前一個範例中：</span><span class="sxs-lookup"><span data-stu-id="bc45c-146">In hello previous example:</span></span>

* <span data-ttu-id="bc45c-147">**BlobStorageURL**是您計劃 toouse hello 儲存體帳戶的 hello URL</span><span class="sxs-lookup"><span data-stu-id="bc45c-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="bc45c-148">**YourImagesFolder**是 hello blob 儲存容器所在 toostore 您的映像</span><span class="sxs-lookup"><span data-stu-id="bc45c-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="bc45c-149">**VHDName** hello 標籤出現在入口網站 tooidentify hello 虛擬硬碟中。</span><span class="sxs-lookup"><span data-stu-id="bc45c-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="bc45c-150">**PathToVHDFile**是 hello 完整路徑和名稱在您的電腦上的 hello.vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="bc45c-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="bc45c-151">下列命令的 hello 示範完整的範例：</span><span class="sxs-lookup"><span data-stu-id="bc45c-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="bc45c-152">步驟 4： 從 hello 映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="bc45c-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="bc45c-153">您建立 VM 使用`azure vm create`在 hello 與規則 VM 相同的方式。</span><span class="sxs-lookup"><span data-stu-id="bc45c-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="bc45c-154">指定您為您的映像提供 hello 上一個步驟中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="bc45c-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="bc45c-155">在下列範例的 hello，我們會使用 hello **myImage** hello 上一個步驟中提供的映像名稱：</span><span class="sxs-lookup"><span data-stu-id="bc45c-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="bc45c-156">toocreate Vm，提供您自己的使用者名稱 + 密碼、 位置、 DNS 名稱和映像名稱。</span><span class="sxs-lookup"><span data-stu-id="bc45c-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc45c-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc45c-157">Next steps</span></span>
<span data-ttu-id="bc45c-158">如需詳細資訊，請參閱[hello Azure 傳統部署模型的 Azure CLI 參考](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="bc45c-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
