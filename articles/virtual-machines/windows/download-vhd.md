---
title: "從 Azure Windows VHD aaaDownload |Microsoft 文件"
description: "下載 Windows VHD 使用 hello Azure 入口網站。"
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="b1dcc-103">從 Azure 下載 Windows VHD</span><span class="sxs-lookup"><span data-stu-id="b1dcc-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="b1dcc-104">在本文中，您將學習如何 toodownload [Windows 虛擬硬碟 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)檔案從 Azure 中，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="b1dcc-105">Azure 的使用中的虛擬機器 (Vm)[磁碟](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)位置 toostore 作業系統、 應用程式，以及資料。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="b1dcc-106">所有 Azure VM 都至少有兩個磁碟：一個 Windows 作業系統磁碟和一個暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="b1dcc-107">從映像，一開始建立 hello 作業系統磁碟和 hello 作業系統磁碟和 hello 映像會儲存在 Azure 儲存體帳戶的 Vhd。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="b1dcc-108">虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="b1dcc-109">停止 hello VM</span><span class="sxs-lookup"><span data-stu-id="b1dcc-109">Stop hello VM</span></span>

<span data-ttu-id="b1dcc-110">如果它已附加，無法從 Azure 下載 VHD tooa 執行 VM。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="b1dcc-111">您需要 toostop hello VM toodownload VHD。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="b1dcc-112">如果您想 toouse VHD 當做[映像](tutorial-custom-images.md)toocreate 您使用其他的 Vm 與新的磁碟， [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello hello 檔案中包含的作業系統，然後再停止 hello VM。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="b1dcc-113">toouse hello VHD 現有的 VM 或資料磁碟的新執行個體的磁碟，您只需要 toostop 和解除配置 hello VM。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="b1dcc-114">toouse hello 做為映像 toocreate 其他 Vm 的 VHD，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b1dcc-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="b1dcc-115">如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="b1dcc-116">[連接 toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="b1dcc-117">在 hello VM，系統管理員身分開啟 hello 命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="b1dcc-118">變更 hello 目錄太*%windir%\system32\sysprep*執行 sysprep.exe。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="b1dcc-119">在 hello 系統準備工具 對話方塊中，選取 **進入系統的全新體驗 (OOBE)**，並確定**一般化**已選取。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="b1dcc-120">在 關機選項 中選取 關機，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="b1dcc-121">toouse hello 做為現有的 VM 或資料磁碟的新執行個體磁碟的 VHD 會完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b1dcc-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="b1dcc-122">Hello 中樞 hello Azure 入口網站中，按一下功能表上**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="b1dcc-123">Hello 清單中選取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="b1dcc-124">Hello VM hello] 刀鋒視窗，按一下 [**停止**。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![停止 VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="b1dcc-126">產生 SAS URL</span><span class="sxs-lookup"><span data-stu-id="b1dcc-126">Generate SAS URL</span></span>

<span data-ttu-id="b1dcc-127">toodownload hello VHD 檔案，您需要 toogenerate[共用的存取簽章 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="b1dcc-128">當產生 hello URL 時，到期時間會指派 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="b1dcc-129">在 hello VM 的 hello 刀鋒視窗的 [hello] 功能表上按一下**磁碟**。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="b1dcc-130">選取 VM，hello hello 作業系統磁碟，然後按一下**匯出**。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="b1dcc-131">設定 hello URL hello 到期時間太*36000*。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="b1dcc-132">按一下 [產生 URL]。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-132">Click **Generate URL**.</span></span>

    ![產生 URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="b1dcc-134">hello 到期時間會增加從 hello 預設 tooprovide 足夠 toodownload hello Windows 伺服器作業系統的大型 VHD 檔案的時間。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="b1dcc-135">您可以預期包含 hello Windows Server 作業系統 tootake 取決於您的連線數個小時 toodownload 的 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="b1dcc-136">如果您正在下載資料磁碟的 VHD，hello 預設時間已足夠。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="b1dcc-137">下載 VHD</span><span class="sxs-lookup"><span data-stu-id="b1dcc-137">Download VHD</span></span>

1.  <span data-ttu-id="b1dcc-138">下所產生的 hello URL，按一下 下載 hello VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![下載 VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="b1dcc-140">您可能需要 tooclick**儲存**hello 瀏覽器 toostart hello 下載中。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="b1dcc-141">hello hello VHD 檔案的預設名稱是*abcd*。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Hello 瀏覽器中，按一下 [儲存]](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="b1dcc-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1dcc-143">Next steps</span></span>

- <span data-ttu-id="b1dcc-144">了解如何太[上傳 VHD 檔案 tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="b1dcc-145">[從儲存體帳戶中的非受控磁碟建立受控磁碟](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="b1dcc-146">[使用 PowerShell 管理 Azure 磁碟](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b1dcc-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

