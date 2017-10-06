---
title: "aaaCreate 您在 Azure DevTest 實驗室的實驗室中的第一個 VM |Microsoft 文件"
description: "深入了解如何 toocreate Azure DevTest 實驗室中的實驗室中的第一個虛擬機器"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a>在 Azure DevTest Labs 的實驗室中建立您的第一個 VM

當您一開始存取 DevTest Labs，並想 toocreate 第一個 VM 時，您將可能會使用進行預先載入[基底 marketplace 映像](devtest-lab-configure-marketplace-images.md)。 在稍後，您也可以從能夠 toochoose[自訂映像和公式](devtest-lab-add-vm.md)時建立多個 Vm。 

本教學課程中引導您使用 Azure 入口網站 tooadd hello DevTest Labs 中的第一個 VM tooa 實驗室。

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a>步驟 tooadd Azure DevTest Labs 中的第一個 VM tooa 實驗室
1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
1. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
1. 從 hello 清單的實驗室中，選取您想在其中 toocreate hello VM hello 實驗室。  
1. 在 hello 實驗室**概觀**刀鋒視窗中，選取**+ 加**。  

    ![加入 VM 按鈕](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. 在 hello**選擇基底**刀鋒視窗中，選取 marketplace 映像的 hello VM。
1. 在 hello**虛擬機器**刀鋒視窗中，輸入 hello 新的虛擬機器的名稱在 hello**虛擬機器名稱**文字方塊。

    ![實驗室 VM 刀鋒視窗](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. 輸入**使用者名**，授與 hello 虛擬機器上的系統管理員權限。  
1. 標示的 hello 文字欄位中輸入密碼**輸入值**。
1. hello**虛擬機器磁碟類型**會決定哪些儲存磁碟類型可供 hello hello 實驗室中的虛擬機器。
1. 選取**虛擬機器大小**和選取 hello 的其中一個預先定義的指定 hello 處理器核心、 RAM 大小，以及 hello VM toocreate hello 硬碟大小的項目。
1. 選取**成品**和-從成品-hello 清單選取，然後設定您想 tooadd toohello 基底映像的 hello 成品。
    **注意：**若您是新 tooDevTest 實驗室或設定成品，請參閱 toohello[加入現有的成品 tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm)區段，然後再在完成時，返回此處。
1. 選取**建立**tooadd hello 指定 VM toohello 實驗室。

   hello 實驗室刀鋒視窗會顯示 hello 狀態的 hello VM 建立-第一次為**建立**，然後為**執行**之後 hello VM 已啟動。

## <a name="next-steps"></a>後續步驟
* 一次 hello 在建立 VM，您可以連接 toohello VM 選取**連接**hello VM 刀鋒視窗上。
* 簽出[加入 VM tooa 實驗室](devtest-lab-add-vm.md)如需將後續的 Vm 加入您的實驗室中的更完整資訊。
* 瀏覽 hello [DevTest Labs Azure 資源管理員的快速入門範本庫](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)。
