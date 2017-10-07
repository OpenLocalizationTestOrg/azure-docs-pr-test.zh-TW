---
title: "Azure Active Directory Domain Services：開始使用 | Microsoft Docs"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）


## <a name="before-you-begin"></a>開始之前
請參閱太[Azure Active Directory 網域服務的網路功能考量](active-directory-ds-networking.md)。


## <a name="task-2-configure-network-settings"></a>工作 2：設定網路設定
hello 下一項組態工作，而且 toocreate Azure 虛擬網路內的專用子網路。 您可在虛擬網路內的這個子網路中啟用 Azure Active Directory Domain Services。 您也可以挑選現有的虛擬網路，並建立 hello 專用子網路內。

1. 按一下**虛擬網路**tooselect 虛擬網路。
2. 在 hello**選擇虛擬網路**刀鋒視窗中，您會看到所有現有的虛擬網路。 您會看到只 hello 屬於 toohello 資源群組和 Azure 位置 hello 上已選取虛擬網路**基本概念**精靈頁面。

3. 選擇已啟用 Azure AD 網域服務的 hello 虛擬網路。 按一下**建立新**，如果您偏好 toocreate 新的虛擬網路。 強烈建議針對 Azure AD Domain Services 使用專用子網路。 如果您挑選現有的虛擬網路，[建立專用子網路使用 hello 虛擬網路的延伸模組](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)然後選擇 子網路。 

    ![挑選虛擬網路](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. 按一下**子網路**toopick hello 這個虛擬網路，在內哪些 tooenable 新受管理網域中的專用子網路。 在 hello**建立子網路**刀鋒視窗中，指定 hello 子網路名稱，然後按一下**確定**完成。 例如，建立子網路與 hello 名稱 'DomainServices'，因此可方便的其他系統管理員 toounderstand hello 子網路內部署的內容。

    ![挑選 hello 虛擬網路內的子網路](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **選取子網路的指導方針**
  > 1. 針對 Azure AD Domain Services 使用專用子網路。 不會部署任何其他虛擬機器 toothis 子網路。 此設定可讓您 tooconfigure 網路安全性群組 (Nsg) 為您的工作負載/虛擬機器而不會中斷您受管理的網域。 如需詳細資訊，請參閱 [Azure Active Directory Domain Services 的網路考量](active-directory-ds-networking.md)。
  2. 請勿選取部署 Azure AD 網域服務的 hello 閘道子網路，因為它不是支援的組態。
  3. 請確定您已選取該 hello 子網路有足夠可用的位址空間至少 3-5 可用的 IP 位址。
  >

5. 當您完成之後時，按一下  **確定**上 toohello toomove **Administrator 群組**hello 精靈頁面。


## <a name="next-step"></a>後續步驟
[工作 3：設定系統管理群組並啟用 Azure AD Domain Services](active-directory-ds-getting-started-admingroup.md)
