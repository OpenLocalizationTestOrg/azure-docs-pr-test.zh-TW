---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 LinkedIn Sales Navigator | Microsoft Docs"
description: "了解 tooconfigure Azure Active Directory tooautomatically 佈建和取消佈建使用者帳戶 tooLinkedIn 銷售導覽的方式。"
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 322c5271535994c13a9fafadbf74f356cdfe865d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-sales-navigator-for-automatic-user-provisioning"></a>教學課程︰設定自動使用者佈建的 LinkedIn Sales Navigator


本教學課程的 hello 目標是 tooshow hello 需要 tooperform LinkedIn 銷售導覽和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooLinkedIn 銷售導覽中的步驟。 

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶
*   LinkedIn Sales Navigator 租用戶 
*   LinkedIn 銷售導覽中系統管理員帳戶具有存取 toohello LinkedIn 帳戶中心

> [!NOTE]
> Azure Active Directory 整合 LinkedIn 銷售導覽使用 hello [SCIM](http://www.simplecloud.info/)通訊協定。

## <a name="assigning-users-toolinkedin-sales-navigator"></a>指派使用者 tooLinkedIn 銷售導覽

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，將同步的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。 

之前設定，及啟用 hello 佈建服務，您將需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooLinkedIn 銷售導覽。 一旦決定，您可以指派這些使用者 tooLinkedIn 銷售導覽 hello 遵循指示：

[指派使用者或群組的 tooan 企業應用程式](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-sales-navigator"></a>指派使用者 tooLinkedIn 銷售導覽的重要秘訣

*   建議在單一 Azure AD 使用者被指派 tooLinkedIn 銷售導覽 tootest hello 佈建的組態。 其他使用者及/或群組可能會稍後再指派。

*   指派使用者 tooLinkedIn 銷售導覽時，您必須選取 hello**使用者**hello 分派對話方塊中的角色。 hello 「 預設的存取 」 角色不適用於佈建。


## <a name="configuring-user-provisioning-toolinkedin-sales-navigator"></a>設定使用者佈建 tooLinkedIn 銷售導覽

本節會引導您完成連接您 Azure AD tooLinkedIn 銷售導覽 SCIM 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新並停用使用者為基礎的 LinkedIn 銷售導覽中指派的使用者帳戶並在 Azure AD 中的群組指派。

> [!TIP]
> 您也可以選擇 tooenabled SAML 型單一登入的 LinkedIn 銷售導覽 中提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-sales-navigator-in-azure-ad"></a>在 Azure AD 中佈建 tooLinkedIn 銷售導覽 tooconfigure 自動使用者帳戶：


hello 第一個步驟是 tooretrieve LinkedIn 的存取語彙基元。 如果您是企業版系統管理員，可以自我佈建存取權杖。 在您的帳戶中心移過**設定&gt;通用設定**和開啟 hello **SCIM 安裝**面板。

> [!NOTE]
> 如果直接而不是透過連結存取 hello 帳戶中心，您可以使用下列步驟的 hello 到達。

1)  登入 tooAccount 中心。

2)  選取 [系統管理員] > [系統管理員設定]**&gt;**。

3)  按一下**進階整合**hello 左提要欄位上。 您已有向的 toohello 帳戶中心。

4)  按一下**+ 加入新的 SCIM 組態**遵循 hello 程序來填入每個欄位。

> 若未啟用自動指派授權，表示只有使用者資料會同步處理。

![LinkedIn Sales Navigator 佈建](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> 啟用 autolicense 指派時，您需要 toonote 應用程式執行個體及授權類型。 第一個伴隨指派授權，先做為基礎，直到所有 hello 授權會都取用。

![LinkedIn Sales Navigator 佈建](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  按一下 [產生權杖]。 您應該會看到您的存取權杖顯示在 [hello] 下**存取權杖**欄位。

6)  離開 hello 頁面之前，儲存您的存取語彙基元 tooyour 剪貼簿或電腦。

7) 接下來，登入 toohello [Azure 入口網站](https://portal.azure.com)，並瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

8) 如果您已經設定 LinkedIn 銷售導覽的單一登入，搜尋您 LinkedIn 銷售導覽使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**LinkedIn 銷售導覽**hello 應用程式庫中。 從 hello 搜尋結果中，選取 LinkedIn 銷售導覽，並將它新增 tooyour 的應用程式的清單。

9)  選取您的執行個體的 LinkedIn 銷售導覽中，然後選取 hello**佈建** 索引標籤。

10) 設定 hello**佈建模式**太**自動**。

![LinkedIn Sales Navigator 佈建](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  填寫下列欄位底下的 hello**系統管理員認證**:

* 在 hello**租用戶 URL**欄位中，輸入 https://api.linkedin.com。

* 在 hello**密碼語彙基元**欄位中輸入您在步驟 1 中產生的 hello 存取權杖，然後按一下**測試連接**。

* 您應該會看到您的入口網站的 hello upperright 端成功的通知。

12) 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊下方。

13) 按一下 [儲存] 。 

14) 在 hello**屬性對應**區段中，檢閱將會同步處理從 Azure AD tooLinkedIn 銷售導覽的 hello 使用者和群組屬性。 請注意，hello 做為所選取的屬性**比對**屬性將會使用的 toomatch hello 使用者帳戶和群組 LinkedIn 銷售導覽中的進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

![LinkedIn Sales Navigator 佈建](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) tooenable hello LinkedIn 銷售導覽器中，變更 hello 的 Azure AD 佈建服務**佈建狀態**太**上**在 hello**設定**區段

16) 按一下 [儲存] 。 

這會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooLinkedIn 銷售導覽 hello 使用者和群組 區段。 請注意，hello 初始同步處理會花費較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 LinkedIn 銷售導覽應用程式上的執行的所有動作。


## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-enterprise-apps-manage-provisioning.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
