---
title: "Windows Azure VM 的映像 aaaCapture |Microsoft 文件"
description: "擷取與 hello 傳統部署模型所建立的 Azure Windows 虛擬機器的映像。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="0fbc6-103">擷取與 hello 傳統部署模型所建立的 Azure Windows 虛擬機器的映像。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-103">Capture an image of an Azure Windows virtual machine created with hello classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0fbc6-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0fbc6-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0fbc6-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0fbc6-107">如需 Resource Manager 模型的資訊，請參閱[在 Azure 中擷取一般化 VM 的受管理映像](../capture-image-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="0fbc6-108">本文章將示範如何 toocapture Azure 虛擬機器執行 Windows，您可以將它當做映像 toocreate 其他虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-108">This article shows you how toocapture an Azure virtual machine running Windows so you can use it as an image toocreate other virtual machines.</span></span> <span data-ttu-id="0fbc6-109">此映像包含 hello 作業系統磁碟，而且是所有資料磁碟都附加 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-109">This image includes hello operating system disk and any data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="0fbc6-110">它不包含網路設定，讓您將需要其他使用 hello 映像的虛擬機器建立 hello tooset 網路組態設定。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-110">It doesn't include networking configurations, so you'll need tooset up network configurations when you create hello other virtual machines that use hello image.</span></span>

<span data-ttu-id="0fbc6-111">Azure 的存放區 hello 下方影像**VM 映像 （傳統）**、**計算**列出當您檢視所有的服務 hello Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-111">Azure stores hello image under **VM images (classic)**, a **Compute** service that is listed when you view all hello Azure services.</span></span> <span data-ttu-id="0fbc6-112">這是 hello 儲存任何您已上傳的映像的相同位置。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-112">This is hello same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="0fbc6-113">如需映像的詳細資訊，請參閱 [有關虛擬機器的映像](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0fbc6-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="0fbc6-114">Before you begin</span></span>
<span data-ttu-id="0fbc6-115">這些步驟假設您已經建立 Azure 虛擬機器，並設定 hello 作業系統，包括附加的任何資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-115">These steps assume that you've already created an Azure virtual machine and configured hello operating system, including attaching any data disks.</span></span> <span data-ttu-id="0fbc6-116">如果您還沒有這麼做，請參閱下列文章中的資訊建立和準備 hello 虛擬機器上的 hello:</span><span class="sxs-lookup"><span data-stu-id="0fbc6-116">If you haven't done this yet, see hello following articles for information on creating and preparing hello virtual machine:</span></span>

* [<span data-ttu-id="0fbc6-117">從映像建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0fbc6-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="0fbc6-118">如何 tooattach 資料磁碟 tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0fbc6-118">How tooattach a data disk tooa virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="0fbc6-119">請確定 hello 伺服器角色支援使用 Sysprep。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-119">Make sure hello server roles are supported with Sysprep.</span></span> <span data-ttu-id="0fbc6-120">如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="0fbc6-121">此程序在經擷取後便會刪除 hello 原始虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-121">This process deletes hello original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="0fbc6-122">先前的 Azure 虛擬機器的映像 toocapturing，建議您備份 hello 目標虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-122">Prior toocapturing an image of an Azure virtual machine, it is recommended hello target virtual machine be backed up.</span></span> <span data-ttu-id="0fbc6-123">Azure 虛擬機器可使用 Azure 備份進行備份。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="0fbc6-124">如需詳細資訊，請參閱 [備份 Azure 虛擬機器](../../../backup/backup-azure-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="0fbc6-125">來自認證合作夥伴的其他解決方案也可供使用。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="0fbc6-126">toofind 解目前可用，搜尋 hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-126">toofind out what’s currently available, search hello Azure Marketplace.</span></span>

## <a name="capture-hello-virtual-machine"></a><span data-ttu-id="0fbc6-127">擷取 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0fbc6-127">Capture hello virtual machine</span></span>
1. <span data-ttu-id="0fbc6-128">在 hello [Azure 入口網站](http://portal.azure.com)，**連接**toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-128">In hello [Azure portal](http://portal.azure.com), **Connect** toohello virtual machine.</span></span> <span data-ttu-id="0fbc6-129">如需指示，請參閱[如何 tooa 虛擬機器執行 Windows Server 中的 toosign][How toosign in tooa virtual machine running Windows Server]。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-129">For instructions, see [How toosign in tooa virtual machine running Windows Server][How toosign in tooa virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="0fbc6-130">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="0fbc6-131">變更 hello 目錄太`%windir%\system32\sysprep`，然後執行 sysprep.exe。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-131">Change hello directory too`%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="0fbc6-132">hello**系統準備工具** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-132">hello **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="0fbc6-133">請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="0fbc6-133">Do hello following:</span></span>

   * <span data-ttu-id="0fbc6-134">在 [系統清理動作] 中選取 [Enter System Out-of-Box Experience (OOBE)]，並確認 [一般化] 已勾選。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="0fbc6-135">如需有關使用 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介][How tooUse Sysprep: An Introduction]。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-135">For more information about using Sysprep, see [How tooUse Sysprep: An Introduction][How tooUse Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="0fbc6-136">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="0fbc6-137">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-137">Click **OK**.</span></span>

   ![執行 Sysprep](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="0fbc6-139">Sysprep 關閉 hello 虛擬機器，會隨之變更的 hello hello Azure 入口網站中的虛擬機器的 hello 狀態**已停止**。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-139">Sysprep shuts down hello virtual machine, which changes hello status of hello virtual machine in hello Azure portal too**Stopped**.</span></span>
6. <span data-ttu-id="0fbc6-140">在 hello Azure 入口網站，按一下 **虛擬機器 （傳統）**和選取 hello 想 toocapture 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-140">In hello Azure portal, click **Virtual Machines (classic)** and select hello virtual machine you want toocapture.</span></span> <span data-ttu-id="0fbc6-141">hello **VM 映像 （傳統）**群組列在**計算**當您檢視**更多服務**。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-141">hello **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="0fbc6-142">Hello 命令列上，按一下**擷取**。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-142">On hello command bar, click **Capture**.</span></span>

   ![擷取虛擬機器](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="0fbc6-144">hello**擷取 hello 虛擬機器** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-144">hello **Capture hello Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="0fbc6-145">在**映像名稱**，輸入 hello 新映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-145">In **Image name**, type a name for hello new image.</span></span> <span data-ttu-id="0fbc6-146">在**映像標籤**，輸入 hello 新映像的標籤。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-146">In **Image label**, type a label for hello new image.</span></span>

9. <span data-ttu-id="0fbc6-147">按一下**我已在 hello 虛擬機器上執行 Sysprep**。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-147">Click **I've run Sysprep on hello virtual machine**.</span></span> <span data-ttu-id="0fbc6-148">此核取方塊是指在步驟 3-5 Sysprep toohello 動作。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-148">This checkbox refers toohello actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="0fbc6-149">映像_必須_執行 Sysprep 之前新增 Windows Server 映像 tooyour 設定的自訂映像一般化。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image tooyour set of custom images.</span></span>

10. <span data-ttu-id="0fbc6-150">Hello 新映像完成 hello 擷取時，會出現在 hello **Marketplace**，在 hello**計算**， **VM 映像 （傳統）**容器。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-150">Once hello capture completes, hello new image becomes available in hello **Marketplace**, in hello **Compute**, **VM images (classic)** container.</span></span>

    ![成功擷取映像](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="0fbc6-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fbc6-152">Next steps</span></span>
<span data-ttu-id="0fbc6-153">hello 映像已準備好用的 toobe toocreate 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-153">hello image is ready toobe used toocreate virtual machines.</span></span> <span data-ttu-id="0fbc6-154">toodo，您將建立虛擬機器選取 hello**更多服務**hello hello 服務 功能表的底部，然後在功能表項目**VM 映像 （傳統）**在 hello**計算**群組。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-154">toodo this, you'll create a virtual machine by selecting hello **More services** menu item at hello bottom of hello services menu, then **VM images (classic)** in hello **Compute** group.</span></span> <span data-ttu-id="0fbc6-155">如需指示，請參閱 [從映像建立虛擬機器](createportal.md)。</span><span class="sxs-lookup"><span data-stu-id="0fbc6-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
