---
title: "Windows Server VM 的 aaaConnect tooa |Microsoft 文件"
description: "了解 tooconnect 和 tooa Windows VM 使用登入 hello Azure 入口網站與 hello Resource Manager 部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="0fe22-103">如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows</span><span class="sxs-lookup"><span data-stu-id="0fe22-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="0fe22-104">您將使用 hello**連接**hello Azure 入口網站的 toostart 從 Windows 桌面的遠端桌面 (RDP) 工作階段中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0fe22-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="0fe22-105">您第一次連接 toohello 虛擬機器，然後登入。</span><span class="sxs-lookup"><span data-stu-id="0fe22-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="0fe22-106">如果您嘗試 tooconnect tooa 從 Mac Windows VM，您需要想 RDP 用戶端適用於 Mac 的 tooinstall [Microsoft 遠端桌面](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417)。</span><span class="sxs-lookup"><span data-stu-id="0fe22-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="0fe22-107">Toohello 虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="0fe22-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="0fe22-108">如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0fe22-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0fe22-109">在 hello 中樞功能表中，按一下 **虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="0fe22-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="0fe22-110">從 [hello] 清單中選取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0fe22-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="0fe22-111">在 hello 刀鋒視窗中的 hello 虛擬機器，按一下 **連接**。</span><span class="sxs-lookup"><span data-stu-id="0fe22-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![螢幕擷取畫面的 hello Azure 入口網站的顯示方式 tooconnect tooyour VM。](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="0fe22-113">如果 hello**連接**hello 入口網站中的按鈕會呈現灰色，而您並不透過連線的 tooAzure [Express Route](../../expressroute/expressroute-introduction.md)或[站對站 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)連線，您需要 toocreate 和將 VM 指派的公用 IP 位址，才能使用 RDP。</span><span class="sxs-lookup"><span data-stu-id="0fe22-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="0fe22-114">您可以深入了解 [Azure 中的公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="0fe22-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="0fe22-115">登入 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0fe22-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="0fe22-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fe22-116">Next steps</span></span>
<span data-ttu-id="0fe22-117">如果您會遇到問題，當您嘗試 tooconnect 時，請參閱[疑難排解遠端桌面連線](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0fe22-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="0fe22-118">本文會逐步帶領您診斷及解決常見的問題。</span><span class="sxs-lookup"><span data-stu-id="0fe22-118">This article walks you through diagnosing and resolving common problems.</span></span>

