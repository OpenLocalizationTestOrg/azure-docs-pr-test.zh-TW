---
title: "aaaConfigure 位於 Azure 的 DevTest Labs 虛擬網路 |Microsoft 文件"
description: "深入了解如何 tooconfigure 現有的虛擬網路和子網路，並將其用於具有 Azure DevTest Labs 的 VM"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>設定 Azure DevTest Labs 中的虛擬網路
Hello 文章所述[加入成品 tooa 實驗室與 VM](devtest-lab-add-vm-with-artifacts.md)，當您建立 VM 在實驗室中，您可以指定設定的虛擬網路。 執行此動作的其中一個案例是您的公司網路資源，您使用的 Vm 所傳來如果您需要 tooaccess hello 與 ExpressRoute 或站對站 VPN 已經設定的虛擬網路。 hello 下列各節將說明如何 tooadd 實驗室的虛擬網路設定，讓建立 Vm 時，它會變成可用 toochoose 到您現有的虛擬網路。

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>設定實驗室，使用 hello Azure 入口網站的虛擬網路
hello 下列步驟引導您完成新增現有的虛擬網路 （和子網路） tooa 實驗室使 hello 中建立 VM 時才能使用相同的實驗室。 

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。
2. 選取**更服務**，然後選取**DevTest Labs**從 hello 清單。
3. 從 hello 清單的實驗室中，選取 hello 所需的實驗室。 
4. 在 hello 實驗室刀鋒視窗中，選取 **組態**。
5. 在 hello 實驗室**組態**刀鋒視窗中，選取**虛擬網路**。
6. 在 hello**虛擬網路**刀鋒視窗中，您會看到一份 hello 目前實驗室以及 hello 預設建立虛擬網路是您的實驗室中設定虛擬網路。 
7. 選取 [+ 新增] 。
   
    ![加入現有的虛擬網路 tooyour 實驗室](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. 在 hello**虛擬網路**刀鋒視窗中，選取**[選取虛擬網路]**。
   
    ![選取現有的虛擬網路](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. 在 hello**選擇虛擬網路**刀鋒視窗中，選取 hello 所需的虛擬網路。 hello 刀鋒視窗中顯示所有 hello 虛擬網路會在 hello 相同 hello 實驗室 hello 訂用帳戶中的區域。  
10. 選取虛擬網路之後, 您會返回 toohello**虛擬網路**按一下 hello hello 在 hello hello 刀鋒視窗底部的清單中的子網路。

    ![子網路清單](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    hello 實驗室子網路 刀鋒視窗會顯示。

    ![實驗室子網路刀鋒視窗](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. 指定 [實驗室子網路名稱]。
12. 在實驗室中建立 VM，使用子網路 toobe tooallow 選取**中建立虛擬機器使用**。
13. tooenable[共用公用 IP 位址](devtest-lab-shared-ip.md)，選取**啟用共用公用 IP**。
14. tooallow 公用 IP 位址的子網路中，選取**允許公用 IP 建立**。
15. 在 hello**每位使用者最多虛擬機器**欄位中，指定 hello 每位使用者每個子網路的最大 Vm。 如果您想要不限數目的 VM 數，請將此欄位保留空白。
16. 選取**確定**tooclose hello 實驗室子網路 刀鋒視窗。
17. 選取**儲存**tooclose hello 虛擬網路 刀鋒視窗。
18. 既然 hello 虛擬網路設定，也可以選取建立 VM 時。 
    toosee 如何 toocreate VM 並指定虛擬網路，請參閱 toohello 文章[加入成品 tooa 實驗室與 VM](devtest-lab-add-vm-with-artifacts.md)。 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>後續步驟
新增 hello 預期虛擬網路 tooyour 實驗室之後下, 一個步驟的 hello 太[加入 VM tooyour 實驗室](devtest-lab-add-vm-with-artifacts.md)。

