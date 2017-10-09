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
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a>登入 tooa 使用 hello Azure 入口網站的 Windows 虛擬機器
在 hello Azure 入口網站，您可以使用 hello**連接**按鈕 toostart 遠端桌面工作階段，然後登入 tooa Windows VM。

您想 tooconnect tooa Linux VM 嗎？ 請參閱[如何 tooa 執行 Linux 的虛擬機器上的 toolog](../../linux/mac-create-ssh-keys.md)。

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 如需有關如何在 tooa VM 使用 toolog hello 資源管理員資訊模型，請參閱[這裡](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="connect-toohello-virtual-machine"></a>Toohello 虛擬機器連線
1. 登入 toohello Azure 入口網站。
2. 按一下您想 tooaccess hello 虛擬機器。 hello 名稱會列在 hello**所有資源**窗格。

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. 按一下**連接**hello hello 虛擬機器儀表板頂端的命令列上。

    ![Connect hello 虛擬機器圖示](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a>登入 toohello 虛擬機器
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>後續步驟
* 如果 hello**連接**按鈕無法使用，或有其他 hello 遠端桌面連線的問題，請嘗試重設 hello 組態。 按一下**重設遠端存取**從 hello 虛擬機器儀表板。

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* 如果是您的密碼有問題，請嘗試重設密碼。 按一下**重設密碼**沿著 hello 左邊緣的虛擬機器儀表板，底下**支援 + 疑難排解**。

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

如果這些秘訣無法運作，或不是您的需要請參閱[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 本文會逐步帶領您診斷及解決常見的問題。
