---
title: "教學課程：設定使用者佈建的 Workplace by Facebook | Microsoft Docs"
description: "了解如何 tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooWorkplace 由 Facebook。"
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a>教學課程：設定使用者佈建的 Workplace by Facebook

此教學課程會顯示 hello 步驟需要 tooautomatically 佈建和解除佈建的 Azure Active Directory (Azure AD) tooWorkplace 由 Facebook 使用者帳戶。

## <a name="prerequisites"></a>必要條件

tooconfigure 由 Facebook 的工作場所的 Azure AD 整合，您需要下列 hello:

- Azure AD 訂用帳戶
- 已啟用 Workplace by Facebook (SSO) 單一登入的訂用帳戶

tootest hello 步驟在本教學課程，請遵循下列建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="assign-users-tooworkplace-by-facebook"></a>指派由 Facebook 使用者 tooWorkplace

Azure AD 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已指派 Azure AD 中的 tooan 應用程式。

設定及啟用 hello 佈建服務，決定哪些使用者和群組在 Azure AD 中之前代表 hello 使用者需要存取 tooyour 工作地點的 Facebook 應用程式。 然後您可以指派這些使用者 tooyour 工作地點的 Facebook 應用程式遵循 hello 中的指示[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)。

>[!IMPORTANT]
>*   藉由指派單一佈建組態的測試 hello Azure AD 使用者 tooWorkplace 由 Facebook。 稍後指派額外的使用者和群組。
>*   當您將指派由 Facebook 使用者 tooWorkplace 時，您必須選取有效的使用者角色。 hello 預設存取角色不適用於佈建。

## <a name="enable-automated-user-provisioning"></a>啟用自動使用者佈建

本節將引導您完成連線 Azure AD toohello 使用者帳戶佈建應用程式開發介面的工作地點的 Facebook。 此外，您也會學習如何 tooconfigure hello 佈建服務 toocreate、 更新和停用在工作地點的 Facebook 指派的使用者帳戶。 這是以 Azure AD 中的使用者和群組指派為基礎。

>[!Tip]
>您也可以選擇 tooenabled SAML 單一登入工作場所的 Facebook，藉由遵循 hello 中提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。 您可以獨立設定自動佈建的 SSO，雖然這兩個功能彼此補充。

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>設定 Azure AD 中佈建 tooWorkplace 由 Facebook 使用者帳戶

Azure AD 支援 hello 能力 tooautomatically 同步處理的 hello 帳戶詳細資料指派給使用者 tooWorkplace 由 Facebook。 此自動同步處理工作地點啟用 Facebook tooget hello 資料之前需要 tooauthorize 使用者進行存取，這些嘗試 toosign 中的 hello 第一次。 當存取在 Azure AD 中被撤銷時，它也會從 Workplace by Facebook 取消佈建使用者。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，選取**Azure Active Directory** > **企業應用程式** > **所有應用程式**.

2. 如果您已經為 SSO 設定由 Facebook 的工作場所，請利用 hello 搜尋欄位中搜尋執行個體的 Facebook 的工作場所。 否則，請選取**新增**並搜尋**工作地點的 Facebook** hello 應用程式庫中。 選取**工作地點的 Facebook** hello 從搜尋結果，並將它加入 tooyour 的應用程式的清單。

3. 選取您的工作地點的 Facebook、 執行個體，然後選取 [hello**佈建**] 索引標籤。

4. 設定**佈建模式**太**自動**。 

    ![Workplace by Facebook 佈建選項的螢幕擷取畫面](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. 在 hello**系統管理員認證**區段中，輸入 hello**密碼語彙基元**和 hello**租用戶 URL** Facebook 管理員工作地點。

6. 在 hello Azure 入口網站，選取 **測試連接**tooensure Azure AD 可連接 tooyour 工作地點的 Facebook 應用程式。 如果 hello 連線失敗，請確定您的工作場所的 Facebook 帳戶具有小組系統管理員權限。

7. 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，然後 hello 核取方塊。

8. 選取 [ **儲存**]。

9. 在 hello 對應區段中，選取**由 Facebook 的同步處理 Azure Active Directory 使用者 tooWorkplace**。

10. 在 hello**屬性對應**區段中，檢閱 hello 從 Azure AD tooWorkplace Facebook 會同步處理的使用者屬性。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在工作地點的 Facebook 進行更新作業。 任何變更，請選取 toocommit**儲存**。

11. tooenable hello Azure AD 佈建服務的 Facebook 的工作場所中 hello**設定**區段中，變更 hello**佈建狀態**太**上**。

12. 選取 [ **儲存**]。

如需有關如何 tooconfigure 自動佈建，請參閱[hello Facebook 文件](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)。

您現在可以建立測試帳戶了。 等候總 tooverify hello 帳戶已經過同步處理由 Facebook tooWorkplace too20 分鐘。

## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-facebook-at-work-tutorial.md)

