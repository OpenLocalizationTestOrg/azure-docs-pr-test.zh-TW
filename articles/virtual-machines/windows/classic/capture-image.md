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
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>擷取與 hello 傳統部署模型所建立的 Azure Windows 虛擬機器的映像。
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 如需 Resource Manager 模型的資訊，請參閱[在 Azure 中擷取一般化 VM 的受管理映像](../capture-image-resource.md)。

本文章將示範如何 toocapture Azure 虛擬機器執行 Windows，您可以將它當做映像 toocreate 其他虛擬機器。 此映像包含 hello 作業系統磁碟，而且是所有資料磁碟都附加 toohello 虛擬機器。 它不包含網路設定，讓您將需要其他使用 hello 映像的虛擬機器建立 hello tooset 網路組態設定。

Azure 的存放區 hello 下方影像**VM 映像 （傳統）**、**計算**列出當您檢視所有的服務 hello Azure 服務。 這是 hello 儲存任何您已上傳的映像的相同位置。 如需映像的詳細資訊，請參閱 [有關虛擬機器的映像](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json)。

## <a name="before-you-begin"></a>開始之前
這些步驟假設您已經建立 Azure 虛擬機器，並設定 hello 作業系統，包括附加的任何資料磁碟。 如果您還沒有這麼做，請參閱下列文章中的資訊建立和準備 hello 虛擬機器上的 hello:

* [從映像建立虛擬機器](createportal.md)
* [如何 tooattach 資料磁碟 tooa 虛擬機器](attach-disk.md)
* 請確定 hello 伺服器角色支援使用 Sysprep。 如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)。

> [!WARNING]
> 此程序在經擷取後便會刪除 hello 原始虛擬機器。
>
>

先前的 Azure 虛擬機器的映像 toocapturing，建議您備份 hello 目標虛擬機器。 Azure 虛擬機器可使用 Azure 備份進行備份。 如需詳細資訊，請參閱 [備份 Azure 虛擬機器](../../../backup/backup-azure-vms.md)。 來自認證合作夥伴的其他解決方案也可供使用。 toofind 解目前可用，搜尋 hello Azure Marketplace。

## <a name="capture-hello-virtual-machine"></a>擷取 hello 虛擬機器
1. 在 hello [Azure 入口網站](http://portal.azure.com)，**連接**toohello 虛擬機器。 如需指示，請參閱[如何 tooa 虛擬機器執行 Windows Server 中的 toosign][How toosign in tooa virtual machine running Windows Server]。
2. 以系統管理員身分開啟 [命令提示字元] 視窗。
3. 變更 hello 目錄太`%windir%\system32\sysprep`，然後執行 sysprep.exe。
4. hello**系統準備工具** 對話方塊隨即出現。 請勿 hello 遵循：

   * 在 [系統清理動作] 中選取 [Enter System Out-of-Box Experience (OOBE)]，並確認 [一般化] 已勾選。 如需有關使用 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介][How tooUse Sysprep: An Introduction]。
   * 在 [關機選項] 中選取 [關機]。
   * 按一下 [確定] 。

   ![執行 Sysprep](./media/capture-image/SysprepGeneral.png)
5. Sysprep 關閉 hello 虛擬機器，會隨之變更的 hello hello Azure 入口網站中的虛擬機器的 hello 狀態**已停止**。
6. 在 hello Azure 入口網站，按一下 **虛擬機器 （傳統）**和選取 hello 想 toocapture 虛擬機器。 hello **VM 映像 （傳統）**群組列在**計算**當您檢視**更多服務**。

7. Hello 命令列上，按一下**擷取**。

   ![擷取虛擬機器](./media/capture-image/CaptureVM.png)

   hello**擷取 hello 虛擬機器** 對話方塊隨即出現。

8. 在**映像名稱**，輸入 hello 新映像的名稱。 在**映像標籤**，輸入 hello 新映像的標籤。

9. 按一下**我已在 hello 虛擬機器上執行 Sysprep**。 此核取方塊是指在步驟 3-5 Sysprep toohello 動作。 映像_必須_執行 Sysprep 之前新增 Windows Server 映像 tooyour 設定的自訂映像一般化。

10. Hello 新映像完成 hello 擷取時，會出現在 hello **Marketplace**，在 hello**計算**， **VM 映像 （傳統）**容器。

    ![成功擷取映像](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>後續步驟
hello 映像已準備好用的 toobe toocreate 虛擬機器。 toodo，您將建立虛擬機器選取 hello**更多服務**hello hello 服務 功能表的底部，然後在功能表項目**VM 映像 （傳統）**在 hello**計算**群組。 如需指示，請參閱 [從映像建立虛擬機器](createportal.md)。

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
