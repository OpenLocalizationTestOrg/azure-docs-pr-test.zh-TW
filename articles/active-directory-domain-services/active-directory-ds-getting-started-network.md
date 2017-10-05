---
title: "Azure Active Directory Domain Services：開始使用 | Microsoft Docs"
description: "使用 Azure 入口網站 (預覽) 啟用 Azure Active Directory Domain Services"
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
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a>使用 Azure 入口網站 (預覽) 啟用 Azure Active Directory Domain Services


## <a name="before-you-begin"></a>開始之前
請參閱 [Azure Active Directory Domain Services 的網路考量](active-directory-ds-networking.md)。


## <a name="task-2-configure-network-settings"></a>工作 2：設定網路設定
下一個設定工作是建立 Azure 虛擬網路與其中的專用子網路。 您可在虛擬網路內的這個子網路中啟用 Azure Active Directory Domain Services。 您也可以挑選現有的虛擬網路，並且建立其中的專用子網路。

1. 按一下 [虛擬網路] 以選取虛擬網路。
2. 在 [選擇虛擬網路] 刀鋒視窗中，您會看到所有現有的虛擬網路。 您只會看到隸屬於您在 [基本] 精靈分頁上選取之資源群組和 Azure 位置的虛擬網路。

3. 選擇應該在其中啟用 Azure AD Domain Services 的虛擬網路。 如果您想要建立新的虛擬網路，請按一下 [新建]。 強烈建議針對 Azure AD Domain Services 使用專用子網路。 如果您挑選現有的虛擬網路，[使用虛擬網路延伸模組建立專用子網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)，然後挑選該子網路。 

    ![挑選虛擬網路](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. 按一下 [子網路] 以挑選此虛擬網路中的專用子網路，在其中啟用新的受管理的網域。 在 [建立子網路] 刀鋒視窗中，指定子網路的名稱，然後在您完成時按一下 [確定]。 例如，建立具有名稱 'DomainServices' 的子網路，讓其他系統管理員容易了解子網路內部署的內容。

    ![挑選虛擬網路內的子網路](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **選取子網路的指導方針**
  > 1. 針對 Azure AD Domain Services 使用專用子網路。 不要將任何其他虛擬機器部署到此子網路。 此設定可讓您為工作負載/虛擬機器設定網路安全性群組 (NSG)，而不會中斷受管理的網域。 如需詳細資訊，請參閱 [Azure Active Directory Domain Services 的網路考量](active-directory-ds-networking.md)。
  2. 請勿選取閘道子網路來部署 Azure AD Domain Services，因為它不是支援的設定。
  3. 請確定您選取的子網路具有足夠的可用位址空間，至少 3-5 個可用 IP 位址。
  >

5. 完成時，按一下 [確定] 以繼續前往精靈的 [Administrator 群組] 分頁。


## <a name="next-step"></a>後續步驟
[工作 3：設定系統管理群組並啟用 Azure AD Domain Services](active-directory-ds-getting-started-admingroup.md)
