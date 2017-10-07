---
title: "根據 Azure VM 的 Azure RemoteApp 映像的 aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate 開始使用 Azure 虛擬機器的 Azure RemoteApp 映像。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="4da32-103">建立以 Azure 虛擬機器為基礎的 Azure RemoteApp 映像</span><span class="sxs-lookup"><span data-stu-id="4da32-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4da32-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="4da32-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4da32-105">讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4da32-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4da32-106">您可以從 Azure 虛擬機器建立 Azure RemoteApp 映像 （保存您共用您的集合中的 hello 應用程式）。</span><span class="sxs-lookup"><span data-stu-id="4da32-106">You can create Azure RemoteApp images (which hold hello apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="4da32-107">您也可以選擇 toouse 我們加入了 toohello Azure VM 映像庫符合所有 hello Azure RemoteApp 映像需求的虛擬機器映像-您可以使用該 VM 映像做為起點的 VM，如果您想要。</span><span class="sxs-lookup"><span data-stu-id="4da32-107">You could also choose toouse a virtual machine image we added toohello Azure VM image gallery that meets all hello Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="4da32-108">只尋找 hello hello 文件庫中的 「 Windows Server 遠端桌面工作階段主機 」 映像。</span><span class="sxs-lookup"><span data-stu-id="4da32-108">Just look for hello "Windows Server Remote Desktop Session Host" image in hello library.</span></span>

<span data-ttu-id="4da32-109">有自己的映像根據 Azure VM 的兩個步驟 toocreate-建立 hello 映像，然後將它上傳從 hello Azure VM 程式庫 tooAzure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="4da32-109">There are two steps toocreate your own image based on an Azure VM - create hello image and then upload it from hello Azure VM library tooAzure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="4da32-110">建立以 Azure VM 為基礎的自訂映像</span><span class="sxs-lookup"><span data-stu-id="4da32-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="4da32-111">使用這些步驟 toocreate 根據 Azure VM 映像。</span><span class="sxs-lookup"><span data-stu-id="4da32-111">Use these steps toocreate an image based on an Azure VM.</span></span>

1. <span data-ttu-id="4da32-112">建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4da32-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="4da32-113">您可以使用 hello 「 Windows Server 遠端桌面工作階段主機 」 或 「 Windows Server 遠端桌面工作階段主機與 Microsoft Office 365 ProPlus 」 映像 hello hello Azure 虛擬機器映像庫中。</span><span class="sxs-lookup"><span data-stu-id="4da32-113">You can use hello "Windows Server Remote Desktop Session Host" or hello "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from hello Azure virtual machine image gallery.</span></span> <span data-ttu-id="4da32-114">此映像符合所有的 hello Azure RemoteApp 範本映像需求。</span><span class="sxs-lookup"><span data-stu-id="4da32-114">This image meets all hello Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="4da32-115">如需詳細資訊，請參閱[建立執行 Windows 的 VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4da32-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="4da32-116">連接 toohello VM 安裝和設定您想要透過 RemoteApp tooshare hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4da32-116">Connect toohello VM and install and configure hello apps that you want tooshare through RemoteApp.</span></span> <span data-ttu-id="4da32-117">請確定 tooperform 您的應用程式所需的任何其他 Windows 設定。</span><span class="sxs-lookup"><span data-stu-id="4da32-117">Make sure tooperform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="4da32-118">如需詳細資訊，請參閱[如何 tooa 執行 Windows Server 的虛擬機器上的 tooLog](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4da32-118">For details, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="4da32-119">如果您使用其中一個 hello Windows Server 遠端桌面工作階段主機映像，則包含的驗證指令碼，將可確保您的 VM 符合 hello RemoteApp 前 reqs.</span><span class="sxs-lookup"><span data-stu-id="4da32-119">If you are using one of hello Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets hello RemoteApp pre-reqs.</span></span> <span data-ttu-id="4da32-120">toorun 指令碼，連按兩下**ValidateRemoteAppImage** hello 桌面上。</span><span class="sxs-lookup"><span data-stu-id="4da32-120">toorun script, double-click **ValidateRemoteAppImage** on hello desktop.</span></span> <span data-ttu-id="4da32-121">請繼續 toohello 下一個步驟之前修復的 hello 指令碼所報告的所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="4da32-121">Ensure that all errors reported by hello script are fixed before proceeding toohello next step.</span></span>
4. <span data-ttu-id="4da32-122">SYSPREP 一般化，擷取 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="4da32-122">SYSPREP generalize and capture hello image.</span></span> <span data-ttu-id="4da32-123">請參閱[如何 tooCapture 做為範本的 Windows 虛擬機器 tooUse](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="4da32-123">See [How tooCapture a Windows Virtual Machine tooUse as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a><span data-ttu-id="4da32-124">Hello 映像匯入 hello Azure RemoteApp 映像庫</span><span class="sxs-lookup"><span data-stu-id="4da32-124">Import hello image into hello Azure RemoteApp image library</span></span>
<span data-ttu-id="4da32-125">使用這些步驟 tooimport hello 新映像到 Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="4da32-125">Use these steps tooimport hello new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="4da32-126">在 [hello**範本映像**] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="4da32-126">In hello **Template Images** tab:</span></span>
   
   * <span data-ttu-id="4da32-127">如果您沒有現有的映像，請按一下 [ **上傳或匯入範本映像**]。</span><span class="sxs-lookup"><span data-stu-id="4da32-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="4da32-128">如果您已經有至少一個映像，請按一下 **+**  tooadd 新映像。</span><span class="sxs-lookup"><span data-stu-id="4da32-128">If you have at least one image already, click **+** tooadd a new image.</span></span>
2. <span data-ttu-id="4da32-129">選取 [從您的虛擬機器映像庫匯入映像]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="4da32-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="4da32-130">在 hello 下一個頁面上，從 hello 清單中選取自訂映像，並確認您已遵循 hello 列出當您建立您的映像的步驟。</span><span class="sxs-lookup"><span data-stu-id="4da32-130">On hello next page, select your custom image from hello list and confirm that you followed hello steps listed when you created your image.</span></span> <span data-ttu-id="4da32-131">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="4da32-131">Click **Next**.</span></span>
4. <span data-ttu-id="4da32-132">輸入 hello 新 RemoteApp 映像的名稱和挑選 hello 位置，然後按一下 hello 核取記號 toostart hello 匯入程序。</span><span class="sxs-lookup"><span data-stu-id="4da32-132">Enter a name for hello new RemoteApp image and pick hello location, then click hello checkmark toostart hello import process.</span></span>

> [!NOTE]
> <span data-ttu-id="4da32-133">您可以從任何支援的 Azure 虛擬機器 tooany Azure RemoteApp 所支援的 Azure 位置的 Azure 位置，以匯入映像。</span><span class="sxs-lookup"><span data-stu-id="4da32-133">You can import images from any Azure location supported by Azure Virtual Machines tooany Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="4da32-134">根據 hello 位置 hello 匯入可能會佔用 too25 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4da32-134">Depending on hello locations hello import can take up too25 minutes.</span></span>
> 
> 

<span data-ttu-id="4da32-135">現在您已準備好 toocreate 您新的集合，或是[雲端](remoteapp-create-cloud-deployment.md)集合或[混合式](remoteapp-create-hybrid-deployment.md)，視您的需求。</span><span class="sxs-lookup"><span data-stu-id="4da32-135">Now you are ready toocreate your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

