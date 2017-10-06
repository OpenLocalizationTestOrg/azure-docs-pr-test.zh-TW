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
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>啟用 Azure Active Directory 網域服務使用 hello Azure 入口網站 （預覽）


## <a name="task-3-configure-administrative-group"></a>工作 3：設定系統管理群組
在這項設定工作中，您可以在 Azure AD 目錄中建立系統管理群組。 這個特殊的系統管理群組稱為 *AAD DC 系統管理員*。 系統管理員權限的電腦已加入網域的 toohello 受管理的網域，會授與此群組的成員。 已加入網域的電腦上，此群組會加入 toohello administrators 群組。 此外，此群組的成員可以使用遠端桌面 tooconnect 遠端 toodomain 加入機器。

> [!NOTE]
> 您沒有 hello 您使用 Azure Active Directory 網域服務建立的受管理網域的網域系統管理員或企業系統管理員權限。 上受管理的網域，這些權限所保留的 hello 服務，並不會使用 toousers hello 租用戶中。 不過，您可以使用特殊 hello 建立系統管理群組中此組態工作 tooperform 某些特殊權限操作。 這些作業包括加入電腦 toohello 網域屬於 toohello 管理群組已加入網域的機器上，設定群組原則。
>

hello 精靈會自動建立 Azure AD 目錄中的 hello 系統管理群組。 此群組名為「AAD DC 系統管理員」。 如果您有現有的群組具有此名稱在 Azure AD 目錄中，hello 精靈會選取此群組。 您可以設定群組成員資格使用 hello **Administrator 群組**精靈頁面。

1. tooconfigure 群組成員資格，按一下 [ **AAD DC 管理員**。

    ![設定群組成員資格](./media/getting-started/domain-services-blade-admingroup.png)

2. 按一下 hello**將成員加入**按鈕 tooadd 使用者從 Azure AD 目錄 toohello 系統管理員群組。

3. 當您完成之後時，按一下 [**確定**上 toohello toomove**摘要**hello 精靈頁面。

4. 在 [hello**摘要**精靈頁面的 hello] 檢閱 hello 組態設定 hello 受管理的網域。 您可以移回 tooany 步驟的 hello 精靈 toomake 變更，如有必要。 當您完成之後時，按一下 [**確定**toocreate hello 新增受管理的網域。

    ![摘要](./media/getting-started/domain-services-blade-summary.png)

5. 您會看到顯示 Azure AD 網域服務部署的 hello 進度通知。 按一下 hello 通知 toosee 詳細 hello 部署的進度。

    ![通知 - 部署進行中](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>佈建受管理的網域
佈建受管理的網域 hello 程序可能佔用 tooan 小時。

1. 在進行部署時，您可以搜尋 ' 網域中的服務' hello**搜尋資源**搜尋] 方塊。 選取**Azure AD 網域服務**從 hello 搜尋結果。 hello **Azure AD 網域服務**刀鋒視窗會列出 hello 正在佈建的受管理的網域。

    ![找出正在佈建的受管理的網域](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. 按一下 hello 受管理網域 (例如，' contoso100.com') toosee hello 名稱 hello 定義域有關的更多詳細資料。

    ![Domain Services - 佈建狀態](./media/getting-started/domain-services-provisioning-state.png)

3. hello**概觀**索引標籤會顯示目前正在佈建該 hello 網域。 完整佈建之前，您無法設定 hello 受管理的網域。 就會在完全佈建您受管理的網域 toobe tooan 小時。

    ![網域服務的 hello 佈建狀態在 [概觀] 索引標籤 ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Hello 受管理的網域完整佈建，hello**概觀**索引標籤會顯示 hello 網域狀態為**執行**。

    ![Domain Services - 完全佈建後的 [概觀] 索引標籤](./media/getting-started/domain-services-provisioned.png)

5. 在 [hello**屬性**索引標籤上，您會看到兩個在哪個網域控制站可供 hello 虛擬網路的 IP 位址。

    ![Domain Services - 完整佈建後的屬性索引標籤](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>後續步驟
[工作 4： 更新 hello hello Azure 虛擬網路的 DNS 設定](active-directory-ds-getting-started-dns.md)
