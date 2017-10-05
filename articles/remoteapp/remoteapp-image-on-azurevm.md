---
title: "建立以 Azure VM 為基礎的 Azure RemoteApp 映像 | Microsoft Docs"
description: "了解如何開始使用 Azure 虛擬機器來建立 Azure RemoteApp 映像。"
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
ms.openlocfilehash: ee64b86835af8e6237cddcd8acc779fc6dac8214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="9cf24-103">建立以 Azure 虛擬機器為基礎的 Azure RemoteApp 映像</span><span class="sxs-lookup"><span data-stu-id="9cf24-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cf24-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="9cf24-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9cf24-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="9cf24-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9cf24-106">您可以從 Azure 虛擬機器建立 Azure RemoteApp 映像 (其中保存您在集合中共用的應用程式)。</span><span class="sxs-lookup"><span data-stu-id="9cf24-106">You can create Azure RemoteApp images (which hold the apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="9cf24-107">您也可以使用我們已新增至 Azure VM 映像資源庫的虛擬機器映像，其符合所有 Azure RemoteApp 映像需求。如果您想要的話，您可以將該 VM 映像做為您自己 VM 的起點使用。</span><span class="sxs-lookup"><span data-stu-id="9cf24-107">You could also choose to use a virtual machine image we added to the Azure VM image gallery that meets all the Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="9cf24-108">只需在映像庫中尋找「Windows Server 遠端桌面工作階段主機」。</span><span class="sxs-lookup"><span data-stu-id="9cf24-108">Just look for the "Windows Server Remote Desktop Session Host" image in the library.</span></span>

<span data-ttu-id="9cf24-109">根據 Azure VM 建立您的專屬映像共有兩個步驟：建立映像，然後將它從 Azure VM 映像庫上傳至 Azure RemoteApp。</span><span class="sxs-lookup"><span data-stu-id="9cf24-109">There are two steps to create your own image based on an Azure VM - create the image and then upload it from the Azure VM library to Azure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="9cf24-110">建立以 Azure VM 為基礎的自訂映像</span><span class="sxs-lookup"><span data-stu-id="9cf24-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="9cf24-111">使用這些步驟來建立以 Azure VM 為基礎的映像。</span><span class="sxs-lookup"><span data-stu-id="9cf24-111">Use these steps to create an image based on an Azure VM.</span></span>

1. <span data-ttu-id="9cf24-112">建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9cf24-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="9cf24-113">您可以使用 Azure 虛擬機器映像庫中的「Windows Server 遠端桌面工作階段主機」或「Windows Server 遠端桌面工作階段主機與 Microsoft Office 365 ProPlus」映像。</span><span class="sxs-lookup"><span data-stu-id="9cf24-113">You can use the "Windows Server Remote Desktop Session Host" or the "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from the Azure virtual machine image gallery.</span></span> <span data-ttu-id="9cf24-114">此映像符合所有的 Azure RemoteApp 範本映像需求。</span><span class="sxs-lookup"><span data-stu-id="9cf24-114">This image meets all the Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="9cf24-115">如需詳細資訊，請參閱[建立執行 Windows 的 VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="9cf24-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="9cf24-116">連接至 VM，並安裝和設定您想要透過 RemoteApp 共用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cf24-116">Connect to the VM and install and configure the apps that you want to share through RemoteApp.</span></span> <span data-ttu-id="9cf24-117">請務必執行您應用程式所需的任何其他 Windows 設定。</span><span class="sxs-lookup"><span data-stu-id="9cf24-117">Make sure to perform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="9cf24-118">如需詳細資訊，請參閱[如何登入執行 Windows Server 的虛擬機器](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="9cf24-118">For details, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="9cf24-119">如果您打算使用 Windows Server 遠端桌面工作階段主機映像之一，它包含了可確保您的 VM 符合 RemoteApp 先決條件的驗證指令碼。</span><span class="sxs-lookup"><span data-stu-id="9cf24-119">If you are using one of the Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets the RemoteApp pre-reqs.</span></span> <span data-ttu-id="9cf24-120">若要執行指令碼，請按兩下桌面上的 **ValidateRemoteAppImage** 。</span><span class="sxs-lookup"><span data-stu-id="9cf24-120">To run script, double-click **ValidateRemoteAppImage** on the desktop.</span></span> <span data-ttu-id="9cf24-121">在繼續進行下一個步驟之前，請確定已修正指令碼所報告的所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="9cf24-121">Ensure that all errors reported by the script are fixed before proceeding to the next step.</span></span>
4. <span data-ttu-id="9cf24-122">SYSPREP 一般化和擷取映像。</span><span class="sxs-lookup"><span data-stu-id="9cf24-122">SYSPREP generalize and capture the image.</span></span> <span data-ttu-id="9cf24-123">如需相關指示，請參閱[如何擷取 Windows 虛擬機器作為範本使用](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) 。</span><span class="sxs-lookup"><span data-stu-id="9cf24-123">See [How to Capture a Windows Virtual Machine to Use as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-the-image-into-the-azure-remoteapp-image-library"></a><span data-ttu-id="9cf24-124">將映像匯入 Azure RemoteApp 映像庫</span><span class="sxs-lookup"><span data-stu-id="9cf24-124">Import the image into the Azure RemoteApp image library</span></span>
<span data-ttu-id="9cf24-125">使用下列步驟將新的映像匯入 Azure RemoteApp：</span><span class="sxs-lookup"><span data-stu-id="9cf24-125">Use these steps to import the new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="9cf24-126">在 [ **範本映像** ] 索引標籤中：</span><span class="sxs-lookup"><span data-stu-id="9cf24-126">In the **Template Images** tab:</span></span>
   
   * <span data-ttu-id="9cf24-127">如果您沒有現有的映像，請按一下 [ **上傳或匯入範本映像**]。</span><span class="sxs-lookup"><span data-stu-id="9cf24-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="9cf24-128">如果您已經有一個以上的映像，請按一下 [ **+** ] 以新增映像。</span><span class="sxs-lookup"><span data-stu-id="9cf24-128">If you have at least one image already, click **+** to add a new image.</span></span>
2. <span data-ttu-id="9cf24-129">選取 [從您的虛擬機器映像庫匯入映像]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9cf24-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="9cf24-130">在下一個頁面上，從清單中選取自訂映像，並確認您已遵循建立映像時的所列步驟進行。</span><span class="sxs-lookup"><span data-stu-id="9cf24-130">On the next page, select your custom image from the list and confirm that you followed the steps listed when you created your image.</span></span> <span data-ttu-id="9cf24-131">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9cf24-131">Click **Next**.</span></span>
4. <span data-ttu-id="9cf24-132">輸入新 RemoteApp 映像的名稱，並挑選一個位置，然後按一下核取記號以開始匯入程序。</span><span class="sxs-lookup"><span data-stu-id="9cf24-132">Enter a name for the new RemoteApp image and pick the location, then click the checkmark to start the import process.</span></span>

> [!NOTE]
> <span data-ttu-id="9cf24-133">您可以將映像從 Azure 虛擬機器支援的任何 Azure 位置，匯入到 Azure RemoteApp 支援的任何 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="9cf24-133">You can import images from any Azure location supported by Azure Virtual Machines to any Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="9cf24-134">視位置而定，匯入可能需要多達 25 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="9cf24-134">Depending on the locations the import can take up to 25 minutes.</span></span>
> 
> 

<span data-ttu-id="9cf24-135">現在您已經準備好開始建立新的收藏 ([雲端](remoteapp-create-cloud-deployment.md)收藏或[混合式](remoteapp-create-hybrid-deployment.md))，視您的需求而定。</span><span class="sxs-lookup"><span data-stu-id="9cf24-135">Now you are ready to create your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

