---
title: "aaaCreate 的實驗室中 Azure DevTest Labs |Microsoft 文件"
description: "在 Azure DevTest Labs 中為虛擬機器建立實驗室"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a>在 Azure 研測實驗室中建立實驗室
位於 Azure DevTest 實驗室的實驗室是 hello 基礎結構包含一組資源，例如可讓您更佳的虛擬機器 (Vm)，藉由指定限制和配額管理這些資源。 這篇文章會引導您建立的實驗室使用 hello Azure 入口網站的 hello 程序。

## <a name="prerequisites"></a>必要條件
toocreate 實驗室，您需要：

* Azure 訂用帳戶。 請參閱有關 Azure 購買選項 toolearn[如何 toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/)或[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。 您必須是 hello hello 訂用帳戶 toocreate hello 實驗室擁有者。

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a>步驟 toocreate 的實驗室中 Azure DevTest Labs
hello 下列步驟說明如何 toouse 會 hello Azure 入口網站 toocreate Azure DevTest 實驗室中的實驗室。 

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
1. 從左邊為 hello hello 主功能表上，選取**更服務**（位於 hello hello 清單底部）。

    ![[更多服務] 功能表選項](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. 從可用服務清單中 hello **DevTest Labs**。
1. 在 hello **DevTest Labs**刀鋒視窗中，選取**新增**。
   
    ![新增實驗室](./media/devtest-lab-create-lab/add-lab-button.png)

1. 在 hello**建立 DevTest 實驗室**刀鋒視窗中：
   
    1. 輸入**實驗室名稱**hello 新實驗室。
    2. 選取 hello**訂用帳戶**tooassociate 與 hello 實驗室。
    3. 選取**位置**哪些 toostore hello 實驗室中。
    4. 選取**自動關機**toospecify 如果您想 tooenable-定義-hello 參數 hello 自動關閉的所有 hello lab 的 Vm。 hello 自動關閉功能是主要是節省成本的功能，您可以指定當您想 hello VM tooautomatically 關機。 您可以變更自動關閉設定 hello hello 文章所述的步驟建立 hello 實驗室之後[管理所有原則的實驗室中 Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown)。
    5. 選取**Pin tooDashboard**如果您想要的 hello 實驗室 tooappear hello 入口網站儀表板上的捷徑。
    6. 選取**自動化選項**tooget Azure 資源管理員範本組態自動化。 
    7. 選取 [ **建立**]。 選取之後**建立**，hello **DevTest Labs**刀鋒視窗會顯示。 您可以藉由監看 hello 監視 hello 實驗室建立程序的 hello 狀態**通知**區域。 完成後，重新整理 hello 頁面 toosee hello 新建立的實驗室的實驗室 hello 清單中。  
    
    ![建立實驗室刀鋒視窗](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>後續步驟
一旦您已建立您的實驗室，以下是一些下一個步驟 tooconsider:

* [安全存取 tooa 實驗室](devtest-lab-add-devtest-user.md)。
* [設定實驗室原則](devtest-lab-set-lab-policy.md)。
* [建立實驗室範本](devtest-lab-create-template.md)。
* [為您的 VM 建立自訂成品](devtest-lab-artifact-author.md)。
* [加入具有成品 tooa 實驗室 VM](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/)。

