---
title: "請 hello VM 資料磁碟的 d： 磁碟機 |Microsoft 文件"
description: "描述如何 toochange 磁碟機代號為 Windows vm 以便您可以使用 hello d： 磁碟機的資料磁碟機。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Hello d： 磁碟機做為 Windows VM 上的資料磁碟機
如果您的應用程式需要 toouse hello D 磁碟機 toostore 資料，請遵循這些指示 toouse hello 暫存磁碟的不同磁碟機代號。 絕對不要使用，您需要 tookeep hello 暫存磁碟 toostore 資料。

如果您調整大小或**停止 （取消配置）**的虛擬機器，這可能會觸發 hello 虛擬機器 tooa 新 hypervisor 的位置。 已規劃或未規劃的維護事件也可能會觸發這個放置動作。 在此案例中，hello 暫存磁碟會重新指派的 toohello 第一個可用的磁碟機代號。 如果您有特別需要 hello d： 磁碟機的應用程式，您需要 toofollow，這些步驟 tootemporarily 移動 hello pagefile.sys，將新的資料磁碟，並將它指派 hello 代號為 D，然後移動 hello pagefile.sys 回 toohello 暫存磁碟機。 完成後，Azure 將不會傳回 hello d： 如果 hello VM 移 tooa 不同 hypervisor。

如需 Azure 的 hello 暫存磁碟的使用方式的詳細資訊，請參閱[了解 hello 暫存磁碟機上的 Microsoft Azure 虛擬機器](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>附加 hello 資料磁碟
首先，您必須 tooattach hello 資料磁碟 toohello 虛擬機器。 toodo 此使用 hello 入口網站，請參閱[tooattach managed 資料 hello Azure 入口網站中的磁碟](attach-managed-disk-portal.md)。

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>暫時移動 pagefile.sys tooC 磁碟機
1. Toohello 虛擬機器連線。 
2. 以滑鼠右鍵按一下 hello**啟動**功能表，然後選取**系統**。
3. 在 hello 左側功能表中選取**進階系統設定**。
4. 在 hello**效能**區段中，選取**設定**。
5. 選取 hello**進階** 索引標籤。
6. 在 hello**虛擬記憶體**區段中，選取**變更**。
7. 選取 hello **C**磁碟機，然後按一下**系統管理大小**，然後按一下**設定**。
8. 選取 hello **D**磁碟機，然後按一下**沒有分頁檔**，然後按一下**設定**。
9. 按一下 [套用]。 您會收到警告，該 hello 電腦需要 toobe hello 變更 tootake 會影響重新啟動。
10. 重新啟動 hello 虛擬機器。

## <a name="change-hello-drive-letters"></a>變更 hello 磁碟機代號
1. 一次 hello VM 重新啟動時，登入 toohello VM。
2. 按一下 hello**啟動**功能表和型別**diskmgmt.msc**並按下 Enter。 隨即會啟動「磁碟管理」。
3. 以滑鼠右鍵按一下**D**，hello 暫存磁碟機，然後選取 **變更磁碟機代號及路徑**。
4. 在磁碟機代號下方，選取新的磁碟機 (例如 **T**)，然後按一下確定。 
5. 以滑鼠右鍵按一下 hello 資料磁碟，然後選取**變更磁碟機代號及路徑**。
6. 在 磁碟機代號 下方，選取磁碟機 **D**，然後按一下確定。 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>將 pagefile.sys 後 toohello 暫存磁碟機
1. 以滑鼠右鍵按一下 hello**啟動**功能表，然後選取**系統**
2. 在 hello 左側功能表中選取**進階系統設定**。
3. 在 hello**效能**區段中，選取**設定**。
4. 選取 hello**進階** 索引標籤。
5. 在 hello**虛擬記憶體**區段中，選取**變更**。
6. 選取 hello 作業系統磁碟機**C**按一下**沒有分頁檔**，然後按一下**設定**。
7. 選取 hello 暫存磁碟機**T** ，然後按一下**系統管理大小**，然後按一下**設定**。
8. 按一下 [Apply (套用)] 。 您會收到警告，該 hello 電腦需要 toobe hello 變更 tootake 會影響重新啟動。
9. 重新啟動 hello 虛擬機器。

## <a name="next-steps"></a>後續步驟
* 您可以增加 hello 儲存體可用 tooyour 虛擬機器的[附加額外的資料磁碟](attach-managed-disk-portal.md)。

