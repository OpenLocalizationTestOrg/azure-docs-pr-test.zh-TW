---
title: "從 Azure 下載 Windows VHD | Microsoft Docs"
description: "使用 Azure 入口網站來下載 Windows VHD。"
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
ms.openlocfilehash: d8bf89a4b7c2a158302f9ba09a182a3d8d062adc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="cf051-103">從 Azure 下載 Windows VHD</span><span class="sxs-lookup"><span data-stu-id="cf051-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="cf051-104">本文說明如何使用 Azure 入口網站，從 Azure 下載 [Windows 虛擬硬碟 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 檔案。</span><span class="sxs-lookup"><span data-stu-id="cf051-104">In this article, you learn how to download a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using the Azure portal.</span></span> 

<span data-ttu-id="cf051-105">Azure 中的虛擬機器 (VM) 會使用[磁碟](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)來儲存作業系統、應用程式和資料。</span><span class="sxs-lookup"><span data-stu-id="cf051-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="cf051-106">所有 Azure VM 都至少有兩個磁碟：一個 Windows 作業系統磁碟和一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="cf051-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="cf051-107">作業系統磁碟最初是從映像建立，且作業系統磁碟與該映像都是儲存在 Azure 儲存體帳戶中的 VHD。</span><span class="sxs-lookup"><span data-stu-id="cf051-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="cf051-108">虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="cf051-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="cf051-109">停止 VM</span><span class="sxs-lookup"><span data-stu-id="cf051-109">Stop the VM</span></span>

<span data-ttu-id="cf051-110">如果 VHD 連接至執行中的 VM，便無法從 Azure 下載該 VHD。</span><span class="sxs-lookup"><span data-stu-id="cf051-110">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="cf051-111">您必須先停止 VM，才能下載 VHD。</span><span class="sxs-lookup"><span data-stu-id="cf051-111">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="cf051-112">如果您想要使用 VHD 作為[映像](tutorial-custom-images.md)，以新磁碟來建立其他 VM，請使用 [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation)來一般化包含在檔案中的作業系統，然後停止 VM。</span><span class="sxs-lookup"><span data-stu-id="cf051-112">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) to generalize the operating system contained in the file and then stop the VM.</span></span> <span data-ttu-id="cf051-113">若要使用 VHD 作為現有 VM 或資料磁碟新執行個體的磁碟，您只需要停止並解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="cf051-113">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="cf051-114">若要使用 VHD 作為映像來建立其他 VM，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cf051-114">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="cf051-115">如果您尚未登入 [Azure 入口網站](https://portal.azure.com/)，請先登入。</span><span class="sxs-lookup"><span data-stu-id="cf051-115">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="cf051-116">[連接至 VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cf051-116">[Connect to the VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="cf051-117">在 VM 上，以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="cf051-117">On the VM, open the Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="cf051-118">切換至 *%windir%\system32\sysprep* 目錄並執行 sysprep.exe。</span><span class="sxs-lookup"><span data-stu-id="cf051-118">Change the directory to *%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="cf051-119">在 [系統準備工具] 對話方塊中，選取 [進入系統全新體驗 (OOBE)]，並確認已選取 [一般化]。</span><span class="sxs-lookup"><span data-stu-id="cf051-119">In the System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="cf051-120">在 [關機選項] 中選取 [關機]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="cf051-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="cf051-121">若要使用 VHD 作為現有 VM 或資料磁碟新執行個體的磁碟，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cf051-121">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="cf051-122">在 Azure 入口網站的中樞功能表中，按一下 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="cf051-122">On the Hub menu in the Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="cf051-123">從清單中選取 VM。</span><span class="sxs-lookup"><span data-stu-id="cf051-123">Select the VM from the list.</span></span>
3.  <span data-ttu-id="cf051-124">在 VM 的刀鋒視窗中，按一下 [停止]。</span><span class="sxs-lookup"><span data-stu-id="cf051-124">On the blade for the VM, click **Stop**.</span></span>

    ![停止 VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="cf051-126">產生 SAS URL</span><span class="sxs-lookup"><span data-stu-id="cf051-126">Generate SAS URL</span></span>

<span data-ttu-id="cf051-127">若要下載 VHD 檔案，您需要產生[共用存取簽章 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL。</span><span class="sxs-lookup"><span data-stu-id="cf051-127">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="cf051-128">產生 URL 時，會將到期時間指派給 URL。</span><span class="sxs-lookup"><span data-stu-id="cf051-128">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="cf051-129">在 VM 刀鋒視窗的功能表中，按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="cf051-129">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="cf051-130">選取 VM 的作業系統磁碟，然後按一下 [匯出]。</span><span class="sxs-lookup"><span data-stu-id="cf051-130">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="cf051-131">將 URL 的到期時間設定為 *36000*。</span><span class="sxs-lookup"><span data-stu-id="cf051-131">Set the expiration time of the URL to *36000*.</span></span>
4.  <span data-ttu-id="cf051-132">按一下 [產生 URL]。</span><span class="sxs-lookup"><span data-stu-id="cf051-132">Click **Generate URL**.</span></span>

    ![產生 URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="cf051-134">到期時間會從預設設定增加，以提供足夠的時間來下載 Windows Server 作業系統的大型 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="cf051-134">The expiration time is increased from the default to provide enough time to download the large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="cf051-135">根據您的連線速度而定，包含 Windows Server 作業系統的 VHD 檔案可能會花數小時的時間下載。</span><span class="sxs-lookup"><span data-stu-id="cf051-135">You can expect a VHD file that contains the Windows Server operating system to take several hours to download depending on your connection.</span></span> <span data-ttu-id="cf051-136">如果您正在下載資料磁碟的 VHD，預設的時間便已足夠。</span><span class="sxs-lookup"><span data-stu-id="cf051-136">If you are downloading a VHD for a data disk, the default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="cf051-137">下載 VHD</span><span class="sxs-lookup"><span data-stu-id="cf051-137">Download VHD</span></span>

1.  <span data-ttu-id="cf051-138">在產生的 URL 之下，按一下 [下載 VHD 檔案]。</span><span class="sxs-lookup"><span data-stu-id="cf051-138">Under the URL that was generated, click Download the VHD file.</span></span>

    ![下載 VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="cf051-140">您可能需要在瀏覽器中按一下 [儲存] 以開始下載。</span><span class="sxs-lookup"><span data-stu-id="cf051-140">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="cf051-141">VHD 檔案的預設名稱是 *abcd*。</span><span class="sxs-lookup"><span data-stu-id="cf051-141">The default name for the VHD file is *abcd*.</span></span>

    ![在瀏覽器中按一下 [儲存]](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="cf051-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf051-143">Next steps</span></span>

- <span data-ttu-id="cf051-144">了解如何[將 VHD 檔案上傳至 Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cf051-144">Learn how to [upload a VHD file to Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="cf051-145">[從儲存體帳戶中的非受控磁碟建立受控磁碟](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cf051-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="cf051-146">[使用 PowerShell 管理 Azure 磁碟](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="cf051-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

