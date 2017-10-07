---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 Cerner Central | Microsoft Docs"
description: "了解如何 tooconfigure Azure Active Directory tooautomatically 佈建使用者 tooa 名冊 Cerner 集中。"
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>教學課程︰設定自動使用者佈建的 Cerner Central

本教學課程的 hello 目標是 tooshow hello 需要 tooperform Cerner 中央與 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooa 使用者名冊 Cerner 集中中的步驟。 


## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶
*   Cerner Central 租用戶 

> [!NOTE]
> Azure Active Directory 整合與使用 hello Cerner 中央[SCIM](http://www.simplecloud.info/)通訊協定。

## <a name="assigning-users-toocerner-central"></a>指派使用者 tooCerner 中央

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。 

之前設定，及啟用 hello 佈建服務，您應該決定哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooCerner 中央。 一旦決定，您可以指派這些使用者 tooCerner 中央 hello 遵循指示：

[指派使用者或群組的 tooan 企業應用程式](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>指派使用者 tooCerner 中央的重要秘訣

*   建議在單一 Azure AD 使用者被指派 tooCerner 中央 tootest hello 佈建的組態。 其他使用者及/或群組可能會稍後再指派。

* 一旦初始測試完成為單一使用者，Cerner 中央建議任何 Cerner 方案 （不只是 Cerner 中部） 佈建 toobe tooCerner 使用者名冊指派的使用者預期 tooaccess hello 整個清單。  其他 Cerner 解決方案會利用這份 hello 使用者名單中的使用者。

*   指派使用者 tooCerner 管理中心時，您必須選取 hello**使用者**hello 分派對話方塊中的角色。 具有 hello 「 預設的存取 」 角色的使用者會排除佈建。


## <a name="configuring-user-provisioning-toocerner-central"></a>設定使用者佈建 tooCerner 中央

本節會引導您完成連接您 Azure AD tooCerner 中央使用者名單使用 Cerner 的 SCIM 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新，請停用 Cerner 管理中心中的帳戶以指派的使用者在 Azure AD 中使用者和群組指派。

> [!TIP]
> 您也可以選擇 SAML 型單一登入 tooenabled Cerner 中央，hello 指示提供在 [Azure 入口網站 (https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。 如需詳細資訊，請參閱 hello [Cerner 中央單一登入教學課程](active-directory-saas-cernercentral-tutorial.md)。


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>在 Azure AD 中佈建 tooCerner 中央 tooconfigure 自動使用者帳戶：


在順序 tooprovision 使用者帳戶 tooCerner 中央，您將需要 toorequest Cerner，從 Cerner 中央系統帳戶，並產生 tooconnect tooCerner SCIM 端點之後，可以使用 Azure AD 的 OAuth 承載權杖。 也建議 hello 整合，在之前部署 tooproduction Cerner 沙箱環境中執行。

1.  hello 第一個步驟是管理 hello Cerner tooensure hello 人員，以及 Azure AD 整合擁有 CernerCare 帳戶，也就是必要的 tooaccess hello 文件必要 toocomplete hello 指示。 如果有必要，請使用 hello Url toocreate CernerCare 帳戶下每個適用的環境中。

   * 沙箱環境：https://sandboxcernercare.com/accounts/create

   * 生產環境：https://cernercare.com/accounts/create  

2.  接下來，必須建立 Azure AD 的系統帳戶。 使用 hello toorequest 系統帳戶底下的指示您沙箱和實際執行環境。

   * 指示：https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * 沙箱環境：https://sandboxcernercentral.com/system-accounts/

   * 生產環境：https://cernercentral.com/system-accounts/

3.  接下來，產生每個系統帳戶的 OAuth 持有人權杖。 toodo，後續 hello 依照下列指示。

   * 指示：https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * 沙箱環境：https://sandboxcernercentral.com/system-accounts/

   * 生產環境：https://cernercentral.com/system-accounts/

4. 最後，您需要 tooacquire 使用者名冊領域識別碼 Cerner toocomplete hello 組態這兩種 hello 沙箱和實際執行環境。 如需詳細資訊 tooacquire，請參閱： https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM。 

5. 現在您可以設定 Azure AD tooprovision 使用者帳戶 tooCerner。 登入 toohello [Azure 入口網站](https://portal.azure.com)，並瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

6. 如果您已經設定 Cerner 中央進行單一登入，搜尋您 Cerner 中央使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**Cerner 中央**hello 應用程式庫中。 從 hello 搜尋結果中，選取 Cerner 中央，並將它新增 tooyour 的應用程式的清單。

7.  選取您的 Cerner 中央執行個體，然後選取 hello**佈建** 索引標籤。

8.  設定 hello**佈建模式**太**自動**。

   ![Cerner Central 佈建](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  填寫下列欄位底下的 hello**系統管理員認證**:

   * 在 hello**租用戶 URL**欄位中，輸入 「 使用者-名冊-領域-識別碼 」 取代貴用戶取得步驟 #4 中的 hello 領域識別碼 hello 格式下面 URL。

> 沙箱：https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> 生產：https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * 在 hello**密碼語彙基元**欄位中輸入您在步驟 3 中產生 hello OAuth 承載權杖，然後按一下**測試連接**。

   * 您應該會看到您的入口網站的 hello upperright 端成功的通知。

10. 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊下方。

11. 按一下 [儲存] 。 

12. 在 hello**屬性對應**區段中，檢閱 hello 使用者和群組屬性 toobe 從 Azure AD tooCerner 中央同步處理。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 使用者帳戶和群組 Cerner 集中進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

13. tooenable hello Azure AD 佈建服務 Cerner 中央，變更 hello**佈建狀態**太**上**在 hello**設定**區段

14. 按一下 [儲存] 。 

這會啟動 hello 初始同步處理的任何使用者和/或群組指派 tooCerner hello 使用者和群組 > 一節中的中央。 hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello Azure AD 佈建服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Cerner 管理中心應用程式上的執行的所有動作。

如需有關 tooread hello Azure AD 佈建的記錄方式的詳細資訊，請參閱[報告使用者自動帳戶佈建](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。

## <a name="additional-resources"></a>其他資源

* [Cerner Central：使用 Azure AD 發佈身分識別資料](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [教學課程：設定 Cerner Central 搭配 Azure Active Directory 進行單一登入](active-directory-saas-cernercentral-tutorial.md)
* [管理企業應用程式的使用者帳戶佈建](active-directory-enterprise-apps-manage-provisioning.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>後續步驟
* [了解 tooreview 記錄的方式，並取得報告的佈建活動](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting)。
