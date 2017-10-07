---
title: "在 Azure DevTest Labs aaaConfigure Azure Marketplace 映像設定 |Microsoft 文件"
description: "設定在 Azure DevTest Labs 中建立 VM 時可以使用哪些 Azure Marketplace 映像"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a>在 Azure DevTest Labs 中設定 Azure Marketplace 映像設定
DevTest Labs 支援建立 Vm，視您如何設定您的實驗室中使用 Azure Marketplace 映像 toobe Azure Marketplace 映像為基礎。 本文章將示範如何 toospecify 它，如果有的話，可以是 Azure Marketplace 映像在實驗室中建立 Vm 時使用。 這可確保您的小組只具有所需的存取 toohello Marketplace 映像。 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a>選取在建立 VM 時允許使用哪些 Azure Marketplace 映像
1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
3. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。 
4. 在 hello 實驗室刀鋒視窗中，選取 **組態和原則**。
5. 在實驗室的 [組態和原則] 刀鋒視窗的 [Virtual Machine Bases] \(虛擬機器基礎) 下，選取 [Marketplace 映像]。
6. 指定您是否要在所有 hello 限定的 Azure Marketplace 映像 toobe 可供使用，做為基底的新 VM。 如果您選取**是**，然後所有 hello Azure Marketplace 映像的符合所有下列準則 hello 都允許 hello 實驗室中：
   
   * hello 映像建立之單一 VM，**和**
   * hello 映像會使用 Azure Resource Manager tooprovision Vm，**和**
   * hello 映像並不需要購買額外授權計劃
     
    如果您想允許，沒有映像 toobe 或您想要的映像可用，請選取的 toospecify**否**。
     
     ![選項 tooallow 所有 Marketplace 映像 toobe 都做為基底映像的 Vm](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. 如果您選取**否**toohello 前一個步驟，hello**允許映像/選取所有**核取方塊會啟用。 
   您可以使用此選項，連同 hello 搜尋 tooquickly 中，選取或取消選取所有顯示在 [hello] 清單中的 hello 項目。
   * 選取您想要 tooallow VM 建立個別選取每個映像的對應核取方塊的 hello Azure Marketplace 映像。
   * 執行任何動作從清單中選取 hello 如果您不想 tooallow hello 實驗室中使用任何 Azure Marketplace 映像 toobe。
   
    ![您可以指定可使用哪些 Marketplace 映像做為 VM 的基底映像](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>後續步驟
一旦您已建立 VM 時，如何允許 Azure Marketplace 映像，hello 下一個步驟太[加入 VM tooyour 實驗室](devtest-lab-add-vm-with-artifacts.md)。

