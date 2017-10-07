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
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>建立以 Azure 虛擬機器為基礎的 Azure RemoteApp 映像
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

您可以從 Azure 虛擬機器建立 Azure RemoteApp 映像 （保存您共用您的集合中的 hello 應用程式）。 您也可以選擇 toouse 我們加入了 toohello Azure VM 映像庫符合所有 hello Azure RemoteApp 映像需求的虛擬機器映像-您可以使用該 VM 映像做為起點的 VM，如果您想要。 只尋找 hello hello 文件庫中的 「 Windows Server 遠端桌面工作階段主機 」 映像。

有自己的映像根據 Azure VM 的兩個步驟 toocreate-建立 hello 映像，然後將它上傳從 hello Azure VM 程式庫 tooAzure RemoteApp。

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>建立以 Azure VM 為基礎的自訂映像
使用這些步驟 toocreate 根據 Azure VM 映像。

1. 建立 Azure 虛擬機器。 您可以使用 hello 「 Windows Server 遠端桌面工作階段主機 」 或 「 Windows Server 遠端桌面工作階段主機與 Microsoft Office 365 ProPlus 」 映像 hello hello Azure 虛擬機器映像庫中。 此映像符合所有的 hello Azure RemoteApp 範本映像需求。
   
    如需詳細資訊，請參閱[建立執行 Windows 的 VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
2. 連接 toohello VM 安裝和設定您想要透過 RemoteApp tooshare hello 應用程式。 請確定 tooperform 您的應用程式所需的任何其他 Windows 設定。
   
    如需詳細資訊，請參閱[如何 tooa 執行 Windows Server 的虛擬機器上的 tooLog](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。
3. 如果您使用其中一個 hello Windows Server 遠端桌面工作階段主機映像，則包含的驗證指令碼，將可確保您的 VM 符合 hello RemoteApp 前 reqs. toorun 指令碼，連按兩下**ValidateRemoteAppImage** hello 桌面上。 請繼續 toohello 下一個步驟之前修復的 hello 指令碼所報告的所有錯誤。
4. SYSPREP 一般化，擷取 hello 映像。 請參閱[如何 tooCapture 做為範本的 Windows 虛擬機器 tooUse](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)如需相關指示。

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Hello 映像匯入 hello Azure RemoteApp 映像庫
使用這些步驟 tooimport hello 新映像到 Azure RemoteApp:

1. 在 [hello**範本映像**] 索引標籤：
   
   * 如果您沒有現有的映像，請按一下 [ **上傳或匯入範本映像**]。
   * 如果您已經有至少一個映像，請按一下 **+**  tooadd 新映像。
2. 選取 [從您的虛擬機器映像庫匯入映像]，然後按 [下一步]。
3. 在 hello 下一個頁面上，從 hello 清單中選取自訂映像，並確認您已遵循 hello 列出當您建立您的映像的步驟。 按一下 [下一步] 。
4. 輸入 hello 新 RemoteApp 映像的名稱和挑選 hello 位置，然後按一下 hello 核取記號 toostart hello 匯入程序。

> [!NOTE]
> 您可以從任何支援的 Azure 虛擬機器 tooany Azure RemoteApp 所支援的 Azure 位置的 Azure 位置，以匯入映像。 根據 hello 位置 hello 匯入可能會佔用 too25 分鐘。
> 
> 

現在您已準備好 toocreate 您新的集合，或是[雲端](remoteapp-create-cloud-deployment.md)集合或[混合式](remoteapp-create-hybrid-deployment.md)，視您的需求。

