---
title: "從 Azure 下載 Linux VHD | Microsoft Docs"
description: "使用 Azure CLI 和 Azure 入口網站來下載 Linux VHD。"
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
ms.openlocfilehash: 3eb88478b43f8e3a36ae04bf3703f238e8cb1f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="b56e9-103">從 Azure 下載 Linux VHD</span><span class="sxs-lookup"><span data-stu-id="b56e9-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="b56e9-104">本文說明如何使用 Azure CLI 和 Azure 入口網站，從 Azure 下載 [Linux 虛擬硬碟 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 檔案。</span><span class="sxs-lookup"><span data-stu-id="b56e9-104">In this article, you learn how to download a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using the Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="b56e9-105">Azure 中的虛擬機器 (VM) 會使用[磁碟](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)來儲存作業系統、應用程式和資料。</span><span class="sxs-lookup"><span data-stu-id="b56e9-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="b56e9-106">所有 Azure VM 都至少有兩個磁碟：一個 Windows 作業系統磁碟和一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="b56e9-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="b56e9-107">作業系統磁碟最初是從映像建立，且作業系統磁碟與該映像都是儲存在 Azure 儲存體帳戶中的 VHD。</span><span class="sxs-lookup"><span data-stu-id="b56e9-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="b56e9-108">虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="b56e9-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="b56e9-109">如果尚未安裝 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)，請先安裝。</span><span class="sxs-lookup"><span data-stu-id="b56e9-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="b56e9-110">停止 VM</span><span class="sxs-lookup"><span data-stu-id="b56e9-110">Stop the VM</span></span>

<span data-ttu-id="b56e9-111">如果 VHD 連接至執行中的 VM，便無法從 Azure 下載該 VHD。</span><span class="sxs-lookup"><span data-stu-id="b56e9-111">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="b56e9-112">您必須先停止 VM，才能下載 VHD。</span><span class="sxs-lookup"><span data-stu-id="b56e9-112">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="b56e9-113">如果您想要使用 VHD 作為[映像](tutorial-custom-images.md)，以新磁碟來建立其他 VM，則需要取消佈建並一般化包含在檔案中的作業系統，並停止 VM。</span><span class="sxs-lookup"><span data-stu-id="b56e9-113">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you need to deprovision and generalize the operating system contained in the file and stop the VM.</span></span> <span data-ttu-id="b56e9-114">若要使用 VHD 作為現有 VM 或資料磁碟新執行個體的磁碟，您只需要停止並解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="b56e9-114">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="b56e9-115">若要使用 VHD 作為映像來建立其他 VM，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b56e9-115">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1. <span data-ttu-id="b56e9-116">使用 SSH、帳戶名稱與 VM 的公用 IP 位址來連線至 VM，並取消佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="b56e9-116">Use SSH, the account name, and the public IP address of the VM to connect to it and deprovision it.</span></span> <span data-ttu-id="b56e9-117">+user 參數也會移除最後一個佈建的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b56e9-117">The +user parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="b56e9-118">如果要將帳戶認證備份至 VM 中，請省略此 +user 參數。</span><span class="sxs-lookup"><span data-stu-id="b56e9-118">If you are baking account credentials in to the VM, leave out this +user parameter.</span></span> <span data-ttu-id="b56e9-119">下列範例會移除最後一個佈建的使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="b56e9-119">The following example removes the last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="b56e9-120">使用 [az login](https://docs.microsoft.com/cli/azure/#login) 來登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b56e9-120">Sign in to your Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="b56e9-121">停止及解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="b56e9-121">Stop and deallocate the VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="b56e9-122">一般化 VM。</span><span class="sxs-lookup"><span data-stu-id="b56e9-122">Generalize the VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="b56e9-123">若要使用 VHD 作為現有 VM 或資料磁碟新執行個體的磁碟，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b56e9-123">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="b56e9-124">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b56e9-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="b56e9-125">在 [中樞] 功能表上，按一下 [虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="b56e9-125">On the Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="b56e9-126">從清單中選取 VM。</span><span class="sxs-lookup"><span data-stu-id="b56e9-126">Select the VM from the list.</span></span>
4.  <span data-ttu-id="b56e9-127">在 VM 的刀鋒視窗中，按一下 [停止]。</span><span class="sxs-lookup"><span data-stu-id="b56e9-127">On the blade for the VM, click **Stop**.</span></span>

    ![停止 VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="b56e9-129">產生 SAS URL</span><span class="sxs-lookup"><span data-stu-id="b56e9-129">Generate SAS URL</span></span>

<span data-ttu-id="b56e9-130">若要下載 VHD 檔案，您需要產生[共用存取簽章 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL。</span><span class="sxs-lookup"><span data-stu-id="b56e9-130">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="b56e9-131">產生 URL 時，會將到期時間指派給 URL。</span><span class="sxs-lookup"><span data-stu-id="b56e9-131">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="b56e9-132">在 VM 刀鋒視窗的功能表中，按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="b56e9-132">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="b56e9-133">選取 VM 的作業系統磁碟，然後按一下 [匯出]。</span><span class="sxs-lookup"><span data-stu-id="b56e9-133">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="b56e9-134">按一下 [產生 URL]。</span><span class="sxs-lookup"><span data-stu-id="b56e9-134">Click **Generate URL**.</span></span>

    ![產生 URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="b56e9-136">下載 VHD</span><span class="sxs-lookup"><span data-stu-id="b56e9-136">Download VHD</span></span>

1.  <span data-ttu-id="b56e9-137">在產生的 URL 之下，按一下 [下載 VHD 檔案]。</span><span class="sxs-lookup"><span data-stu-id="b56e9-137">Under the URL that was generated, click Download the VHD file.</span></span>

    ![下載 VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="b56e9-139">您可能需要在瀏覽器中按一下 [儲存] 以開始下載。</span><span class="sxs-lookup"><span data-stu-id="b56e9-139">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="b56e9-140">VHD 檔案的預設名稱是 *abcd*。</span><span class="sxs-lookup"><span data-stu-id="b56e9-140">The default name for the VHD file is *abcd*.</span></span>

    ![在瀏覽器中按一下 [儲存]](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="b56e9-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b56e9-142">Next steps</span></span>

- <span data-ttu-id="b56e9-143">瞭解如何[使用 Azure CLI 2.0 從自訂磁碟上傳並建立 Linux VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b56e9-143">Learn how to [upload and create a Linux VM from custom disk with the Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="b56e9-144">[使用 Azure CLI 管理 Azure 磁碟](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b56e9-144">[Manage Azure disks the Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

