---
title: "教學課程：Azure Active Directory 與 Workplace by Facebook 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與工作地點的 Facebook 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>教學課程：設定使用者佈建的 Workplace by Facebook

本教學課程 hello 目標是 tooshow hello 需要 tooperform 工作地點中的 Facebook 和 Azure AD tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooWorkplace 由 Facebook 的步驟。

## <a name="prerequisites"></a>必要條件

tooconfigure 由 Facebook 的工作場所的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Workplace by Facebook 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="assigning-users-tooworkplace-by-facebook"></a>由 Facebook 指派的使用者 tooWorkplace

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour 工作地點的 Facebook 應用程式。 一旦決定，您可以遵循這裡的指示 hello 指派這些使用者 tooyour 工作地點的 Facebook 應用程式：

[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>指派由 Facebook 使用者 tooWorkplace 的重要秘訣

*   建議在單一 Azure AD 使用者指派 tooWorkplace Facebook tootest hello 佈建的組態。 其他使用者及/或群組可能會稍後再指派。

*   由 Facebook 使用者 tooWorkplace 指派時，您必須選取有效的使用者角色。 hello 「 預設的存取 」 角色不適用於佈建。

## <a name="enable-user-provisioning"></a>啟用使用者佈建

本節將引導您透過 Azure AD tooWorkplace 連接 Facebook 的使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello，更新，請停用在工作地點的使用者和群組為基礎的 Facebook 指派的使用者帳戶Azure AD 中的指派。

>[!Tip]
>您也可以選擇 tooenabled SAML 型單一登入的 Facebook、 hello 指示中所提供的工作場所[Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>在 Azure AD 中佈建由 Facebook tooWorkplace tooconfigure 使用者帳戶：

hello 本節目標在於 toooutline 如何 tooenable 佈建的 Active Directory 使用者帳戶 tooWorkplace 由 Facebook。

Azure AD 支援 hello 能力 tooautomatically 同步處理的 hello 帳戶詳細資料指派給使用者 tooWorkplace 由 Facebook。 此自動同步處理工作地點啟用 Facebook tooget hello 資料之前需要 tooauthorize 使用者進行存取，這些嘗試 toosign 中的 hello 第一次。 當存取在 Azure AD 中被撤銷時，它也會從 Workplace by Facebook 取消佈建使用者。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory** > **企業應用程式** > **的所有應用程式** > 一節。

2. 如果您已經設定工作地點的 Facebook 進行單一登入，則會搜尋執行個體的 Facebook 使用 hello 搜尋欄位中的工作場所。 否則，請選取**新增**並搜尋**工作地點的 Facebook** hello 應用程式庫中。 從 hello 搜尋結果中，選取由 Facebook 的工作地點，並將它新增 tooyour 的應用程式的清單。

3. 選取您的工作地點的 Facebook、 執行個體，然後選取 hello**佈建** 索引標籤。

4. 設定 hello**佈建模式**太**自動**。 

    ![佈建](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. 在 hello**系統管理員認證**區段中，輸入 hello 密碼語彙基元，hello Facebook 管理員工作地點的租用戶 URL。

6. 在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 可連接 tooyour 工作地點的 Facebook 應用程式。 如果 hello 連線失敗，請確定您的工作場所的 Facebook 帳戶有小組系統管理員權限。

7. 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。

8. 按一下 [儲存]。

9. 在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooWorkplace 由 Facebook。**

10. 在 hello**屬性對應**區段中，檢閱 hello 從 Azure AD tooWorkplace Facebook 會同步處理的使用者屬性。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在工作地點的 Facebook 進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

11. tooenable hello Azure AD 佈建服務工作場所的 Facebook、 變更 hello**佈建狀態**太**上**在 hello**設定**區段

12. 按一下 [儲存]。

如需有關如何 tooconfigure 自動佈建，請參閱[https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

您現在可以建立測試帳戶了。 等候總 tooverify hello 帳戶已經過同步處理由 Facebook tooWorkplace too20 分鐘。

## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-workplacebyfacebook-tutorial.md)

