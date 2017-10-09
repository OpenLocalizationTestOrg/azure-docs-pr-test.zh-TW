---
title: "從 Azure Linux VHD aaaDownload |Microsoft 文件"
description: "下載 Linux VHD 使用 hello Azure CLI 和 hello Azure 入口網站。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="c3c1e-103">從 Azure 下載 Linux VHD</span><span class="sxs-lookup"><span data-stu-id="c3c1e-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="c3c1e-104">在本文中，您將學習如何 toodownload [Linux 虛擬硬碟 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)檔案從 Azure 中，使用 hello Azure CLI 和 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="c3c1e-105">Azure 的使用中的虛擬機器 (Vm)[磁碟](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)位置 toostore 作業系統、 應用程式，以及資料。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="c3c1e-106">所有 Azure VM 都至少有兩個磁碟：一個 Windows 作業系統磁碟和一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="c3c1e-107">從映像，一開始建立 hello 作業系統磁碟和 hello 作業系統磁碟和 hello 映像會儲存在 Azure 儲存體帳戶的 Vhd。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="c3c1e-108">虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="c3c1e-109">如果尚未安裝 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)，請先安裝。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="c3c1e-110">停止 hello VM</span><span class="sxs-lookup"><span data-stu-id="c3c1e-110">Stop hello VM</span></span>

<span data-ttu-id="c3c1e-111">如果它已附加，無法從 Azure 下載 VHD tooa 執行 VM。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="c3c1e-112">您需要 toostop hello VM toodownload VHD。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="c3c1e-113">如果您想 toouse VHD 當做[映像](tutorial-custom-images.md)toocreate 其他 Vm 使用新磁碟時，需要 toodeprovision 和一般化 hello 中所包含的 hello 作業系統檔案，並停止 hello VM。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="c3c1e-114">toouse hello VHD 現有的 VM 或資料磁碟的新執行個體的磁碟，您只需要 toostop 和解除配置 hello VM。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="c3c1e-115">toouse hello 做為映像 toocreate 其他 Vm 的 VHD，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c3c1e-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="c3c1e-116">使用 SSH、 hello 帳戶名稱，以及的 hello VM tooconnect tooit hello 公用 IP 位址和取消佈建它。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="c3c1e-117">hello + 使用者參數也會移除 hello 最後一個佈建的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="c3c1e-118">如果您將 toohello VM 中的帳戶認證，會省略這 + user 參數。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="c3c1e-119">hello 下列範例會移除 hello 最後一個佈建的使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="c3c1e-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="c3c1e-120">使用的 Azure 帳戶登入 tooyour [az 登入](https://docs.microsoft.com/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="c3c1e-121">停止並取消配置 hello VM。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="c3c1e-122">一般化 hello VM。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="c3c1e-123">toouse hello 做為現有的 VM 或資料磁碟的新執行個體磁碟的 VHD 會完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c3c1e-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="c3c1e-124">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="c3c1e-125">在 hello 中樞功能表中，按一下 **虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="c3c1e-126">Hello 清單中選取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="c3c1e-127">Hello VM hello] 刀鋒視窗，按一下 [**停止**。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![停止 VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="c3c1e-129">產生 SAS URL</span><span class="sxs-lookup"><span data-stu-id="c3c1e-129">Generate SAS URL</span></span>

<span data-ttu-id="c3c1e-130">toodownload hello VHD 檔案，您需要 toogenerate[共用的存取簽章 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="c3c1e-131">當產生 hello URL 時，到期時間會指派 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="c3c1e-132">在 hello VM 的 hello 刀鋒視窗的 [hello] 功能表上按一下**磁碟**。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="c3c1e-133">選取 VM，hello hello 作業系統磁碟，然後按一下**匯出**。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="c3c1e-134">按一下 [產生 URL]。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-134">Click **Generate URL**.</span></span>

    ![產生 URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="c3c1e-136">下載 VHD</span><span class="sxs-lookup"><span data-stu-id="c3c1e-136">Download VHD</span></span>

1.  <span data-ttu-id="c3c1e-137">下所產生的 hello URL，按一下 下載 hello VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![下載 VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="c3c1e-139">您可能需要 tooclick**儲存**hello 瀏覽器 toostart hello 下載中。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="c3c1e-140">hello hello VHD 檔案的預設名稱是*abcd*。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Hello 瀏覽器中，按一下 [儲存]](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="c3c1e-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3c1e-142">Next steps</span></span>

- <span data-ttu-id="c3c1e-143">了解如何太[上傳並從自訂的磁碟以 hello Azure CLI 2.0 建立 Linux VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="c3c1e-144">[管理 Azure 磁碟 hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c3c1e-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

