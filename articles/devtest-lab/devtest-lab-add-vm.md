---
title: "aaaAdd VM tooa 實驗室中 Azure DevTest Labs |Microsoft 文件"
description: "深入了解如何在 Azure DevTest Labs 虛擬機器 tooa 實驗室 tooadd"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 82838e4349550db56de311264c188140b9556b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-vm-tooa-lab-in-azure-devtest-labs"></a>新增 VM tooa 實驗室中 Azure DevTest Labs
如果您已經[建立您的第一個 VM](devtest-lab-create-first-vm.md)，您很有可能是透過預先載入的 [Marketplace 映像](devtest-lab-configure-marketplace-images.md)來完成的。 現在，如果您想 tooadd 後續 Vm tooyour 實驗室，您也可以選擇*基底*也就是 [自訂映像](devtest-lab-create-template.md)或[公式](devtest-lab-manage-formulas.md)。 本教學課程會引導您使用 Azure 入口網站 tooadd VM tooa 實驗室 hello DevTest 實驗室中。

本文也會顯示如何 toomanage hello 成品您的實驗室中的 VM。

## <a name="steps-tooadd-a-vm-tooa-lab-in-azure-devtest-labs"></a>步驟 tooadd VM tooa 實驗室中 Azure DevTest Labs
1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
1. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
1. 從 hello 清單的實驗室中，選取您想在其中 toocreate hello VM hello 實驗室。  
1. 在 hello 實驗室**概觀**刀鋒視窗中，選取**+ 加**。  

    ![加入 VM 按鈕](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. 在 hello**選擇基底**刀鋒視窗中，選取一個 hello VM 的基底。
1. 在 hello**虛擬機器**刀鋒視窗中，輸入 hello 新的虛擬機器的名稱在 hello**虛擬機器名稱**文字方塊。

    ![實驗室 VM 刀鋒視窗](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. 輸入**使用者名**，授與 hello 虛擬機器上的系統管理員權限。  
1. 如果您想要 toouse 密碼儲存在您[密碼存放區](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)，選取**使用已儲存的密碼**，並指定一個索引鍵的值，對應 tooyour 秘密 （密碼）。 否則，標示為的 hello 文字欄位中輸入密碼**輸入值**。
1. hello**虛擬機器磁碟類型**會決定哪些儲存磁碟類型可供 hello hello 實驗室中的虛擬機器。
1. 選取**虛擬機器大小**和選取 hello 的其中一個預先定義的指定 hello 處理器核心、 RAM 大小，以及 hello VM toocreate hello 硬碟大小的項目。
1. 選取**成品**和-從成品-hello 清單選取，然後設定您想 tooadd toohello 基底映像的 hello 成品。
    **注意：**若您是新 tooDevTest 實驗室或設定成品，請參閱 toohello[加入現有的成品 tooa VM](#add-an-existing-artifact-to-a-vm)區段，然後再在完成時，返回此處。
1. 選取**進階設定**tooconfigure hello VM 的網路選項和到期選項。 

   tooset 到期選項，選擇 hello 行事曆圖示 toospecify 日期所在 hello VM 將會自動刪除。  根據預設，永遠不會過期 hello VM。 
1. 如果您想 tooview，或複製 hello Azure 資源管理員範本，請參閱 toohello[儲存 Azure Resource Manager 範本](#save-azure-resource-manager-template)區段，然後完成時，請回到這裡。
1. 選取**建立**tooadd hello 指定 VM toohello 實驗室。
1. hello 實驗室刀鋒視窗會顯示 hello 狀態的 hello VM 建立-第一次為**建立**，然後為**執行**之後 hello VM 已啟動。

> [!NOTE]
> [新增 claimable VM](devtest-lab-add-claimable-vm.md)顯示 toomake 如何 hello claimable VM，使其可供使用 hello 實驗室中的任何使用者。
>
>

## <a name="add-an-existing-artifact-tooa-vm"></a>加入現有的成品 tooa VM
建立 VM 時，您可以加入現有的構件。 每個實驗室包括了 hello 公用 DevTest 實驗室成品儲存機制的成品以及成品，您已建立和加入的 tooyour 擁有成品儲存機制。

* Azure 的 DevTest Labs*成品*可讓您指定*動作*hello VM 已佈建時，例如執行 Windows PowerShell 指令碼、 執行 Bash 指令和安裝軟體會執行。
* 成品*參數*可讓您自訂您的特定案例的 hello 成品

如何 toocreate 成品，請參閱的 toodiscover hello 文件：[深入了解如何 tooauthor 您自己的成品以利使用的 DevTest Labs](devtest-lab-artifact-author.md)。

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
1. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
1. 從 hello 清單的實驗室中，選取包含您要與其 toowork hello VM hello 實驗室。  
1. 選取 [我的虛擬機器]。
1. 選取 hello 所需的 VM。
1. 選取 [構件]。 
1. 選取 [套用構件]。
1. 在 hello**套用成品**刀鋒視窗中，選取 hello 成品想 tooadd toohello VM。
1. 在 hello**新增成品**刀鋒視窗中，輸入所需的 hello 參數值和任何您需要的選擇性參數。  
1. 選取**新增**tooadd hello 成品，並傳回 toohello**套用成品**刀鋒視窗。
1. 視需要繼續為您的 VM 加入構件。
1. 一旦您已經加入您的成品，您可以[變更執行哪些 hello 成品的 hello 順序](#change-the-order-in-which-artifacts-are-run)。 您也可以移回太[檢視或修改成品](#view-or-modify-an-artifact)。
1. 當您新增好構件時，選取 [套用]

## <a name="change-hello-order-in-which-artifacts-are-run"></a>變更成品所執行的 hello 順序
根據預設，會執行的 hello 成品的 hello 動作 hello 順序就加入 toohello VM。 hello 下列步驟說明如何 toochange hello 的 hello 成品執行的順序。

1. 頂端的 hello hello**套用成品**刀鋒視窗中，選取 hello 連結表示 hello toohello VM 已加入的成品數目。
   
    ![加入 tooVM 數量的成品。](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. 在 hello**選取成品**hello 刀鋒視窗，拖曳和卸除 hello 成品所需的順序。 **注意：**如果您無法將拖曳 hello 成品，請確定您正在從 hello hello 成品的左方拖曳。 
1. 完成時選取 [確定]  。  

## <a name="view-or-modify-an-artifact"></a>檢視或修改構件
hello 下列步驟說明如何 tooview 或修改成品的 hello 參數：

1. 頂端的 hello hello**套用成品**刀鋒視窗中，選取 hello 連結表示 hello toohello VM 已加入的成品數目。
   
    ![加入 tooVM 數量的成品。](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. 在 hello**選取成品**刀鋒視窗中，您想 tooview 或編輯選取的 hello 成品。  
1. 在 hello**新增成品**刀鋒視窗中，任何所需的變更，且在選取**確定** tooclose hello**新增成品**刀鋒視窗。
1. 選取**確定**tooclose hello**選取成品**刀鋒視窗。

## <a name="save-azure-resource-manager-template"></a>儲存 Azure Resource Manager 範本
Azure Resource Manager 範本提供的宣告方式 toodefine 可重複的部署。 hello 下列步驟說明如何 toosave hello hello VM 正在建立的 Azure Resource Manager 範本。
儲存之後，您也可以使用 hello Azure Resource Manager 範本[部署新的 Vm，使用 Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment)。

1. 在 hello**虛擬機器**刀鋒視窗中，選取**檢視 ARM 範本**。
2. 在 hello**檢視 Azure Resource Manager 範本**刀鋒視窗中，選取 hello 範本文字。
3. 將複製 hello 選取的文字 toohello 剪貼簿。
4. 選取**確定**tooclose hello**刀鋒視窗中檢視 Azure Resource Manager 範本**。
5. 開啟文字編輯器。
6. 在 hello 剪貼簿中的 hello 範本文字中貼上。
7. 儲存 hello 檔案供日後使用。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>後續步驟
* 一次 hello 在建立 VM，您可以連接 toohello VM 選取**連接**hello VM 刀鋒視窗上。
* 了解如何太[DevTest Labs vm 建立自訂的成品](devtest-lab-artifact-author.md)。
* 瀏覽 hello [DevTest Labs Azure 資源管理員的快速入門範本庫](https://github.com/Azure/azure-devtestlab/tree/master/Samples)。
