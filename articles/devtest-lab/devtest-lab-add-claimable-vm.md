---
title: "aaaAdd Azure DevTest Labs claimable VM tooa 實驗室 |Microsoft 文件"
description: "深入了解如何 tooadd claimable 虛擬機器 tooa 實驗室中 Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>在 Azure DevTest Labs 中加入 claimable VM tooa 實驗室
您可以加入 claimable VM tooa 實驗室環境中類似的方式 toohow 您[加入標準 VM](devtest-lab-add-vm.md) – 從*基底*也就是 [自訂映像](devtest-lab-create-template.md)，[公式](devtest-lab-manage-formulas.md)，或[Marketplace 映像](devtest-lab-configure-marketplace-images.md)。 本教學課程引導您使用 Azure 入口網站 tooadd hello DevTest Labs claimable VM tooa 實驗室，並顯示 hello 程序的使用者依照 tooclaim hello VM。

> [!NOTE]
> 如果您將部署到實驗室 Vm [Azure 資源管理員範本](devtest-lab-create-environment-from-arm.md)，您可以建立 claimable Vm 設定 hello **allowClaim**屬性 tootrue hello 屬性區段中的。
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a>步驟 tooadd Azure DevTest Labs claimable VM tooa 實驗室
1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
1. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
1. 從 hello 清單的實驗室中，選取 hello 實驗室中您想要 toocreate hello claimable VM。  
1. 在 hello 實驗室**概觀**刀鋒視窗中，選取**+ 加**。  

    ![加入 VM 按鈕](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. 在 hello**選擇基底**刀鋒視窗中，選取一個 hello VM 的基底。
1. 在 hello**虛擬機器**刀鋒視窗中，輸入 hello 新的虛擬機器的名稱在 hello**虛擬機器名稱**文字方塊。

    ![實驗室 VM 刀鋒視窗](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. 輸入**使用者名**，授與 hello 虛擬機器上的系統管理員權限。  
1. 如果您想要 toouse 密碼儲存在您[密碼存放區](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)，選取**使用已儲存的密碼**，並指定一個索引鍵的值，對應 tooyour 秘密 （密碼）。 否則，標示為的 hello 文字欄位中輸入密碼**輸入值**。
1. hello**虛擬機器磁碟類型**會決定哪些儲存磁碟類型可供 hello hello 實驗室中的虛擬機器。
1. 選取**虛擬機器大小**和選取 hello 的其中一個預先定義的指定 hello 處理器核心、 RAM 大小，以及 hello VM toocreate hello 硬碟大小的項目。
1. 選取**成品**及從 hello 成品的清單，選取並設定您想 tooadd toohello 基底映像的 hello 成品。 如果您是新 tooDevTest 實驗室或設定成品，請參閱 toohello[加入現有的成品 tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm)區段，然後再在完成時，返回此處。
1. 選取**進階設定**tooconfigure hello VM 的網路選項和到期選項。 在下**宣告選項**，選擇**是**claimable toomake hello 機器。

  ![選擇 toomake hello claimable VM。](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. 如果您想 tooview，或複製 hello Azure 資源管理員範本，請參閱 toohello[儲存 Azure Resource Manager 範本](devtest-lab-add-vm.md#save-azure-resource-manager-template)區段，然後完成時，請回到這裡。
1. 選取**建立**tooadd hello 指定 VM toohello 實驗室。
1. hello 實驗室刀鋒視窗會顯示 hello 狀態的 hello VM 建立-第一次為**建立**，然後為**執行**之後 hello VM 已啟動。


## <a name="using-a-claimable-vm"></a>使用可宣告 VM

使用者可以宣告任何 hello 清單中的 「 Claimable 虛擬機器 」 的 VM 執行這些步驟的其中一項：

* 從 hello 清單中的 「 Claimable 虛擬機器 」 在 hello hello 實驗室概觀刀鋒視窗的底部，以滑鼠右鍵按一下其中一個 hello 清單中的 hello Vm 上，然後選擇 **宣告機器**。

 ![要求特定可宣告 VM。](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* 頂端的 hello hello**概觀**刀鋒視窗中，選擇**宣告任何**。 隨機的虛擬機器指派的 hello claimable Vm 清單。

 ![要求任何可宣告 VM。](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


在使用者宣告 VM 之後，該 VM 將會移至該使用者的 [我的虛擬機器] 清單，且其他使用者將無法宣告該 VM。

## <a name="next-steps"></a>後續步驟
* 一次 hello 在建立 VM，您可以連接 toohello VM 選取**連接**hello VM 刀鋒視窗上。
* 瀏覽 hello [DevTest Labs Azure 資源管理員的快速入門範本庫](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)
