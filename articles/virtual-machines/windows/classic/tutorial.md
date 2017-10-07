---
title: "aaaCreate hello Azure 入口網站中的 VM |Microsoft 文件"
description: "在 hello Azure 入口網站中建立 Windows 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>建立執行 Windows hello Azure 入口網站中的虛擬機器
> [!div class="op_single_selector"]
> * [Azure 入口網站](tutorial.md)
> * [PowerShell：傳統部署](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 了解如何太[使用 hello Resource Manager 部署的模型執行這些步驟](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)使用 hello **Azure 入口網站**。

本教學課程示範如何 toocreate Azure hello Azure 入口網站中執行 Windows 的虛擬機器 (VM)。 我們將使用 Windows Server 映像，例如，但是，這是只有一個許多映像的 hello Azure 優惠。 請注意，您可以選擇何種映像取決於您的訂用帳戶。 例如，Windows 桌面映像可能是可用 tooMSDN 「 訂閱者 」。

這個區段會顯示如何 toouse hello**儀表板**在 hello Azure 入口網站 tooselect，然後再建立 hello 虛擬機器。

您也可以使用 [您自己的映像](createupload-vhd.md)來建立 VM。 toolearn 有關這個主題以及其他方法，請參閱[不同的方式 toocreate Windows 虛擬機器](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>建立 hello 的虛擬機器
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用 hello Resource Manager 部署模型建立 VM](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure 入口網站中。
* 登入 toohello 虛擬機器。 如需指示，請參閱[登入執行 Windows Server 的虛擬機器 tooa](connect-logon.md)。
* 附加磁碟 toostore 資料。 您可以附加空的磁碟和含有資料的磁碟。 如需指示，請參閱 hello[附加資料磁碟 tooa 建立 Windows 虛擬機器與 hello 傳統部署模型](attach-disk.md)。
