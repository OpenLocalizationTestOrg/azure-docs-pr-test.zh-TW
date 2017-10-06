---
title: "教學課程︰以 Azure Active Directory 設定自動使用者佈建的 Slack | Microsoft Docs"
description: "了解如何 tooconfigure Azure Active Directory tooautomatically 佈建和取消佈建使用者帳戶 tooSlack。"
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a>教學課程︰設定自動使用者佈建的 Slack


hello 這個教學課程的目標是 tooshow hello 需要 tooperform Slack 和 Azure 中的步驟 AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooSlack。 

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶
*   Slack 租用戶以 hello[再加上計劃](https://aadsyncfabric.slack.com/pricing)或進一步啟用 
*   具有小組系統管理員權限的 Slack 使用者帳戶 

注意： hello Azure AD 佈建整合依賴 hello [Slack SCIM API](https://api.slack.com/scim)也就是可用 tooSlack 小組 hello 再加上計劃或更高。

## <a name="assigning-users-tooslack"></a>指派使用者 tooSlack

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，將同步的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。 

在之前設定，及啟用 hello 佈建服務，您必須 toodecide 哪些使用者和/或 Azure AD 代表 hello 使用者需要存取 tooyour Slack 的應用程式中的群組。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour Slack 應用程式：

[指派使用者或群組的 tooan 企業應用程式](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a>指派使用者 tooSlack 的重要秘訣

*   建議在單一 Azure AD 使用者被指派 tooSlack tootest hello 佈建的組態。 其他使用者及/或群組可能會稍後再指派。

*   指派使用者 tooSlack 時，您必須選取 hello**使用者**或 hello 分派對話方塊中的 「 群組 」 角色。 hello 「 預設的存取 」 角色不適用於佈建。


## <a name="configuring-user-provisioning-tooslack"></a>設定使用者佈建 tooSlack 

本節會引導您完成連接您的 Azure AD tooSlack 使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新並停用在 Slack 的 Azure AD 中的使用者和群組指派為基礎的指派的使用者帳戶。

**提示：**您也可以選擇 tooenabled SAML 型單一登入 slack，hello 指示 （Azure 入口網站） 中提供 [https://portal.azure.com]。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a>在 Azure AD 中佈建 tooSlack tooconfigure 自動使用者帳戶：


1)  在 [hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

2) 如果您已經設定進行單一登入 Slack，搜尋您的 Slack 使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**Slack** hello 應用程式庫中。 從 hello 搜尋結果中，選取 [Slack，並將它新增 tooyour 的應用程式的清單。

3)  選取您的 Slack，執行個體，然後選取 hello**佈建**] 索引標籤。

4)  設定 hello**佈建模式**太**自動**。

![Slack 佈建](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  在 [hello**系統管理員認證**區段中，按一下**授權**。 這會在新的瀏覽器視窗中開啟 Slack 授權對話方塊。 

6) 在 hello 新視窗中，登入 Slack 使用您的小組系統管理員帳戶。 在 hello 產生授權對話方塊中，選取 hello Slack 的小組，您想要佈建 tooenable，然後選取**授權**。 一旦完成，則傳回 toohello Azure 入口網站 toocomplete hello 佈建的組態。

![授權對話方塊](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) 在 [hello Azure 入口網站，按一下 [**測試連接**tooensure Azure AD 的 tooyour Slack 的應用程式可以連接。 如果 hello 連線失敗，請確定您的 Slack 帳戶具有小組系統管理員權限，然後再次嘗試的 hello 「 授權 」 步驟一次。

8) 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊下方。

9) 按一下 [儲存] 。 

10) 在 [hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooSlack**。

11) 在 [hello**屬性對應**區段中，檢閱將會從 Azure AD tooSlack 同步處理的 hello 使用者屬性。 請注意，hello 做為所選取的屬性**比對**屬性將會使用的 toomatch hello 中的使用者帳戶 Slack 進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

12) tooenable hello Azure AD 佈建服務 slack，變更 hello**佈建狀態**太**上**在 hello**設定**區段

13) 按一下 [儲存] 。 

這會啟動 hello 初始同步任何的處理使用者和/或群組指派 tooSlack 在 hello 使用者和群組 > 一節。 請注意，hello 初始同步處理會花費較長的 tooperform 比發生大約每 10 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Slack 的應用程式上執行的所有動作。

## <a name="optional-configuring-group-object-provisioning-tooslack"></a>[選用]設定佈建 tooSlack 群組物件 

（選擇性） 您可以啟用群組物件，從 Azure AD tooSlack hello 佈建。 這是不同的 「 指派的使用者群組 」，該 hello 實際群組物件中除了 tooits 成員將會複寫從 Azure AD tooSlack。 例如，如果您在 Azure AD 中有名為「我的群組」的群組，則會在 Slack 內建立名為「我的群組」的完全相同群組。

### <a name="tooenable-provisioning-of-group-objects"></a>tooenable 佈建群組物件：

1) 在 [hello 對應區段中，選取**同步處理 Azure Active Directory 群組 tooSlack**。

2) 在屬性對應的 hello 刀鋒視窗中，會設定已啟用 tooYes。

3) 在 [hello**屬性對應**區段中，檢閱將會從 Azure AD tooSlack 同步處理的 hello 群組屬性。 請注意，hello 做為所選取的屬性**比對**屬性將會使用的 toomatch hello 群組 Slack 中進行更新作業。 

4) 按一下 [儲存] 。

這個結果中的 hello 任何群組指派物件 tooSlack**使用者和群組**區段從 Azure AD tooSlack 完整同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Slack 的應用程式上執行的所有動作。


## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-enterprise-apps-manage-provisioning.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
