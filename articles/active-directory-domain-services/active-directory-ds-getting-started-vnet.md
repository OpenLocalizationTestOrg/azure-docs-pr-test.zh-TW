---
title: "Azure Active Directory Domain Services：建立或選取虛擬網路 | Microsoft Docs"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a>為 Azure Active Directory Domain Services 建立或選取虛擬網路
## <a name="before-you-begin"></a>開始之前
請參閱太[Azure Active Directory 網域服務的網路功能考量](active-directory-ds-networking.md)。

## <a name="task-2-create-an-azure-virtual-network"></a>工作 2：建立 Azure 虛擬網路
hello 下一項組態工作，而且 toocreate Azure 虛擬網路內的子網路。 您可在虛擬網路內的這個子網路中啟用 Azure Active Directory Domain Services。 如果您有現有的虛擬網路，您會希望 toouse，您可以略過此步驟。

> [!NOTE]
> 請確定該 hello Azure 虛擬網路，您建立或選擇 [與 Azure Active Directory 網域服務 toouse 所屬 tooan 支援的 Azure Active Directory 網域服務的 Azure 區域。 tooascertain hello Azure Active Directory 網域服務可用的 Azure 區域，請參閱[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)。
>
>請注意，當您在後續的設定步驟中啟用 Azure Active Directory 網域服務時選取 hello 右虛擬網路的 hello 虛擬網路 tooensure hello 名稱。


toocreate 想 tooenable Azure Active Directory 網域服務，Azure 虛擬網路，請遵循這些設定指示：

1. 移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. Hello 左窗格中，選取**網路**。

    ![網路節點](./media/active-directory-domain-services-getting-started/networks-node.png)  
    hello**虛擬網路**視窗隨即開啟。
3. 在 [hello 工作窗格在 hello hello 視窗的底部，按一下**新增**。

    ![虛擬網路視窗](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. 按一下 [網絡服務]，然後選取 [虛擬網路]。

    ![虛擬網路 - 快速建立](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. 按一下 [虛擬網路，toocreate**快速建立**。

6. 指定**名稱**為虛擬網路，然後考慮 hello 下列：
    * 您可以選擇 tooconfigure**位址空間**或**最大 VM 計數**對此網路。
    * 您可以保留 hello **DNS 伺服器**設定為**無**現在。 啟用 Azure Active Directory 網域服務之後，您可以更新 hello 設定。
7. 在 [hello**位置**下拉式清單中，選取支援的 Azure 區域。  
    tooascertain hello Azure Active Directory 網域服務可用的 Azure 區域，請參閱[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)。
8. toocreate 虛擬網路，按一下 [**建立虛擬網路**。

    ![為 Azure Active Directory Domain Services 建立虛擬網路](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. 您已建立虛擬網路之後，選取 hello hello 虛擬網路名稱，然後按一下 [hello**設定**] 索引標籤。

    ![建立子網路](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. 在下**虛擬網路位址空間**，按一下 [**加入子網路**，然後指定子網路與 hello 名稱**AaddsSubnet**。

    ![為 Azure Active Directory Domain Services 建立子網路](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. toocreate hello 子網路中，按一下**儲存**。


## <a name="next-step"></a>後續步驟
[工作 3︰啟用 Azure Active Directory Domain Services](active-directory-ds-getting-started-enableaadds.md)
