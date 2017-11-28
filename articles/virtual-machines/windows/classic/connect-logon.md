---
title: "登入傳統 Azure VM | Microsoft Docs"
description: "使用 Azure 入口網站來登入以傳統部署模型建立的 Windows 虛擬機器。"
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
ms.openlocfilehash: 43d54de7e875de9212c23c49ad0539bf2272a312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="d7615-103">使用 Azure 入口網站登入 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d7615-103">Log on to a Windows virtual machine using the Azure portal</span></span>
<span data-ttu-id="d7615-104">在 Azure 入口網站中，使用 [連接]  按鈕來啟動遠端桌面工作階段，並登入 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="d7615-104">In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.</span></span>

<span data-ttu-id="d7615-105">您想要連線至 Linux VM 嗎？</span><span class="sxs-lookup"><span data-stu-id="d7615-105">Do you want to connect to a Linux VM?</span></span> <span data-ttu-id="d7615-106">請參閱[如何登入執行 Linux 的虛擬機器](../../linux/mac-create-ssh-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="d7615-106">See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how to [perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="d7615-107">Azure 建立和處理資源的部署模型有二種： [Resource Manager 和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d7615-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d7615-108">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="d7615-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d7615-109">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="d7615-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="d7615-110">如需如何使用 Resource Manager 模型登入 VM 的詳細資訊，請參閱[這裡](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d7615-110">For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="d7615-111">連接至虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d7615-111">Connect to the virtual machine</span></span>
1. <span data-ttu-id="d7615-112">登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d7615-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="d7615-113">按一下您想要存取的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d7615-113">Click on the virtual machine that you want to access.</span></span> <span data-ttu-id="d7615-114">名稱會在 [所有資源] 窗格中列出。</span><span class="sxs-lookup"><span data-stu-id="d7615-114">The name is listed in the **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="d7615-116">按一下虛擬機器儀表板頂端命令列上的 [連接]。</span><span class="sxs-lookup"><span data-stu-id="d7615-116">Click **Connect** on the command bar atop the virtual machine dashboard.</span></span>

    ![虛擬機器的 [連接] 圖示](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If the **Connect** button isn't available, see the troubleshooting tips at the end of this article.
>
>
-->

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="d7615-118">登入虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d7615-118">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="d7615-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7615-119">Next steps</span></span>
* <span data-ttu-id="d7615-120">如果 [連接] 按鈕無法使用，或是有其他「遠端桌面」連線問題，請嘗試重設組態。</span><span class="sxs-lookup"><span data-stu-id="d7615-120">If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration.</span></span> <span data-ttu-id="d7615-121">從虛擬機器儀表板按一下 [重設遠端存取]。</span><span class="sxs-lookup"><span data-stu-id="d7615-121">click **Reset remote access** from the virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="d7615-123">如果是您的密碼有問題，請嘗試重設密碼。</span><span class="sxs-lookup"><span data-stu-id="d7615-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="d7615-124">按一下沿著虛擬機器儀表板左側邊緣 [支援與疑難排解] 底下的 [重設密碼]。</span><span class="sxs-lookup"><span data-stu-id="d7615-124">Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="d7615-126">如果這些秘訣無效，或者不是您所需要的，請參閱[針對以 Windows 為基礎之 Azure 虛擬機器的遠端桌面連線進行疑難排解](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d7615-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d7615-127">本文會逐步帶領您診斷及解決常見的問題。</span><span class="sxs-lookup"><span data-stu-id="d7615-127">This article walks you through diagnosing and resolving common problems.</span></span>
