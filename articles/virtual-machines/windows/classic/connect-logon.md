---
title: "在 tooa aaaLog 傳統 Azure VM |Microsoft 文件"
description: "使用 Azure 入口網站 toolog hello tooa 與 hello 傳統部署模型所建立的 Windows 虛擬機器上。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="0ed05-103">登入 tooa 使用 hello Azure 入口網站的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0ed05-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="0ed05-104">在 hello Azure 入口網站，您可以使用 hello**連接**按鈕 toostart 遠端桌面工作階段，然後登入 tooa Windows VM。</span><span class="sxs-lookup"><span data-stu-id="0ed05-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="0ed05-105">您想 tooconnect tooa Linux VM 嗎？</span><span class="sxs-lookup"><span data-stu-id="0ed05-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="0ed05-106">請參閱[如何 tooa 執行 Linux 的虛擬機器上的 toolog](../../linux/mac-create-ssh-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="0ed05-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="0ed05-107">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="0ed05-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0ed05-108">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="0ed05-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0ed05-109">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="0ed05-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0ed05-110">如需有關如何在 tooa VM 使用 toolog hello 資源管理員資訊模型，請參閱[這裡](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0ed05-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="0ed05-111">Toohello 虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="0ed05-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="0ed05-112">登入 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0ed05-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="0ed05-113">按一下您想 tooaccess hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0ed05-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="0ed05-114">hello 名稱會列在 hello**所有資源**窗格。</span><span class="sxs-lookup"><span data-stu-id="0ed05-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="0ed05-116">按一下**連接**hello hello 虛擬機器儀表板頂端的命令列上。</span><span class="sxs-lookup"><span data-stu-id="0ed05-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![Connect hello 虛擬機器圖示](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="0ed05-118">登入 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0ed05-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="0ed05-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ed05-119">Next steps</span></span>
* <span data-ttu-id="0ed05-120">如果 hello**連接**按鈕無法使用，或有其他 hello 遠端桌面連線的問題，請嘗試重設 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="0ed05-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="0ed05-121">按一下**重設遠端存取**從 hello 虛擬機器儀表板。</span><span class="sxs-lookup"><span data-stu-id="0ed05-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="0ed05-123">如果是您的密碼有問題，請嘗試重設密碼。</span><span class="sxs-lookup"><span data-stu-id="0ed05-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="0ed05-124">按一下**重設密碼**沿著 hello 左邊緣的虛擬機器儀表板，底下**支援 + 疑難排解**。</span><span class="sxs-lookup"><span data-stu-id="0ed05-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="0ed05-126">如果這些秘訣無法運作，或不是您的需要請參閱[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0ed05-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="0ed05-127">本文會逐步帶領您診斷及解決常見的問題。</span><span class="sxs-lookup"><span data-stu-id="0ed05-127">This article walks you through diagnosing and resolving common problems.</span></span>
