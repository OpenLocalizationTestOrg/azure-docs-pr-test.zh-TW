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
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows
您將使用 hello**連接**hello Azure 入口網站的 toostart 從 Windows 桌面的遠端桌面 (RDP) 工作階段中的按鈕。 您第一次連接 toohello 虛擬機器，然後登入。

如果您嘗試 tooconnect tooa 從 Mac Windows VM，您需要想 RDP 用戶端適用於 Mac 的 tooinstall [Microsoft 遠端桌面](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417)。

## <a name="connect-toohello-virtual-machine"></a>Toohello 虛擬機器連線
1. 如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 中樞功能表中，按一下 **虛擬機器**。
3. 從 [hello] 清單中選取 hello 虛擬機器。
4. 在 hello 刀鋒視窗中的 hello 虛擬機器，按一下 **連接**。
   
    ![螢幕擷取畫面的 hello Azure 入口網站的顯示方式 tooconnect tooyour VM。](./media/connect-logon/connect.png)
   
   > [!TIP]
   > 如果 hello**連接**hello 入口網站中的按鈕會呈現灰色，而您並不透過連線的 tooAzure [Express Route](../../expressroute/expressroute-introduction.md)或[站對站 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)連線，您需要 toocreate 和將 VM 指派的公用 IP 位址，才能使用 RDP。 您可以深入了解 [Azure 中的公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)。
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>登入 toohello 虛擬機器
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>後續步驟
如果您會遇到問題，當您嘗試 tooconnect 時，請參閱[疑難排解遠端桌面連線](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 本文會逐步帶領您診斷及解決常見的問題。

