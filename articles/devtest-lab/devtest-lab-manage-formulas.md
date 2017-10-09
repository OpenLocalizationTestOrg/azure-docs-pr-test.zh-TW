---
title: "在 Azure DevTest Labs toocreate Vm aaaManage 公式 |Microsoft 文件"
description: "深入了解如何 tooupdate 及移除 Azure DevTest Labs 公式"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>管理 Azure DevTest Labs 公式

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

本文將說明如何 toocreate 基底 （自訂映像、 Marketplace 映像或另一個公式） 或現有 VM 的公式。 本文也會引導您管理現有公式。

## <a name="create-a-formula"></a>建立公式
任何人都 DevTest Labs*使用者*權限是可以 toocreate Vm 做為基底中使用公式。 有兩種方式 toocreate 公式： 

* 基底-當您想使用 toodefine hello 公式的所有 hello 特性。
* 從現有的實驗室 VM-當您想 toocreate 公式時使用 hello 以設定為基礎的現有 VM。

如需有關新增使用者和權限的詳細資訊，請參閱[在 Azure DevTest Labs 中新增擁有者和使用者](./devtest-lab-add-devtest-user.md)。

### <a name="create-a-formula-from-a-base"></a>從基底建立公式
hello 步驟會引導您完成建立公式從自訂映像、 Marketplace 映像或另一個公式 hello 程序。

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。

2. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。

3. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。  

4. 在 hello 實驗室刀鋒視窗中，選取 **公式 （可重複使用基底）**。
   
    ![公式功能表](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. 在 hello**公式**刀鋒視窗中，選取**+ 加**。
   
    ![加入公式](./media/devtest-lab-create-formulas/add-formula.png)

6. 在 hello**選擇基底**刀鋒視窗中，選取 hello 基底 （自訂映像、 Marketplace 映像或公式） 要從中 toocreate hello 公式。
   
    ![基本清單](./media/devtest-lab-create-formulas/base-list.png)

7. 在 hello**建立公式**刀鋒視窗中，指定下列值的 hello:
   
    * **公式名稱** - 輸入公式的名稱。 這個值會顯示 hello 的基底映像的清單中，當您建立 VM 時。 當您輸入時，並不正確，如果訊息指出 hello 需求是有效的名稱，會驗證 hello 名稱。
    * **描述** - 輸入公式的有意義描述。 當您建立 VM 時，這個值是可從 hello 公式的內容功能表。
    * **使用者名稱** - 輸入被授與系統管理員權限的使用者名稱。
    * **密碼**-輸入-或從 hello 下拉式清單中選取-hello 秘密 （密碼） 的 toouse hello 指定使用者相關聯的值。 如需 hello 機密資料的詳細資訊，請參閱[Azure DevTest Labs： 密碼的個人存放區](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/)。
    * **虛擬機器磁碟類型**-指定任一個 （硬碟磁碟機） 的 HDD 或 SSD （固態硬碟） tooindicate 哪些儲存磁碟類型可供使用此基底映像來佈建 hello 虛擬機器。
    * * * 虛擬機器大小 * *-選取其中一個指定 hello 處理器核心、 RAM 大小，以及 hello VM toocreate hello 硬碟大小的 hello 預先定義的項目。 
    * **成品**-選取 tooopen hello**新增成品**刀鋒視窗中，您選取並設定您想 tooadd toohello 基底映像的 hello 成品。 如需構件的詳細資訊，請參閱[在 Azure DevTest Labs 中管理 VM 構件](./devtest-lab-add-vm-with-artifacts.md)。
    * **進階設定**-選取 tooopen hello**進階**刀鋒視窗中，您可以設定下列設定的 hello:
        * **虛擬網路**-指定 hello 所需的虛擬網路。
        * **子網路**-指定所需的 hello 子網路。    
        * **IP 位址設定**-指定是否要讓 hello 公用、 私人或共用的 IP 位址。 如需共用 IP 位址的詳細資訊，請參閱[了解 Azure DevTest Labs 中的共用 IP 位址](./devtest-lab-shared-ip.md)。
        * **讓此機器 claimable** -進行機器"claimable"表示，它將不會指派擁有權時建立的 hello。 改為實驗室使用者都能 tootake 擁有權 （「 宣告 」） hello 機器 hello 實驗室刀鋒視窗中。     
    * **映像**-這個欄位會顯示 hello 先前刀鋒視窗上的 hello 您選取的基底映像的名稱。 
     
       ![建立公式](./media/devtest-lab-create-formulas/create-formula.png)

8. 選取**建立**toocreate hello 公式。

9. 當建立 hello 公式之後時，它會顯示在 hello 的 hello 清單中**公式**刀鋒視窗。

### <a name="create-a-formula-from-a-vm"></a>從 VM 建立公式
hello 下列步驟會引導您建立公式，根據現有的 VM 的 hello 程序。 

> [!NOTE]
> toocreate 從 VM 的公式，hello VM 必須已建立 2016 年 3 月 30 日之後。 
> 
> 

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
3. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。  
4. 在 hello 實驗室**概觀**刀鋒視窗中，選取 hello VM 希望 toocreate hello 公式。
   
    ![實驗室 VM](./media/devtest-lab-create-formulas/my-vms.png)
5. 在 hello VM 刀鋒視窗中，選取 **建立公式 （可重複使用基底）**。
   
    ![建立公式](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. 在 hello**建立公式**刀鋒視窗中，輸入**名稱**和**描述**新公式。
   
    ![建立公式刀鋒視窗](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. 選取**確定**toocreate hello 公式。

## <a name="modify-a-formula"></a>修改公式
toomodify 公式，請遵循下列步驟：

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
3. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。  
4. 在 hello 實驗室刀鋒視窗中，選取 **公式 （可重複使用基底）**。
   
    ![公式功能表](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. 在 hello**實驗室公式**刀鋒視窗中，您想 toomodify 選取 hello 公式。
6. 在 hello**更新公式**刀鋒視窗中，進行所需的 hello 的編輯，然後選取**更新**。

## <a name="delete-a-formula"></a>刪除公式
toodelete 公式，請遵循下列步驟：

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
3. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。  
4. 在 hello 實驗室**設定**刀鋒視窗中，選取**公式**。
   
    ![公式功能表](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. 在 hello**實驗室公式**刀鋒視窗中，選取 hello hello 公式的右邊的省略符號 toohello 想 toodelete。
   
    ![公式功能表](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. Hello 公式的內容功能表上，選取**刪除**。
   
    ![公式操作功能表](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. 選取**是**toohello 刪除確認 對話方塊。

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>相關部落格文章
* [自訂映像或公式？](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>後續步驟
一旦您已經建立的公式，建立 VM 時下, 一個步驟的 hello 太[加入 VM tooyour 實驗室](devtest-lab-add-vm-with-artifacts.md)。

