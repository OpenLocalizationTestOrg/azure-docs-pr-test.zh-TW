---
title: "教學課程︰在 Azure 中設定 Google Apps 來自動佈建使用者 | Microsoft Docs"
description: "了解如何 tooautomatically 佈建和取消佈建使用者帳戶從 Azure AD tooGoogle 應用程式。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>教學課程︰設定 Google Apps 來自動佈建使用者

本教學課程的 hello 目標是的 tooshow hello 您需要在 Google Apps 與 Azure AD tooautomatically 規定 tooperform 和解除佈建使用者帳戶從 Azure AD tooGoogle 應用程式的步驟。

## <a name="prerequisites"></a>必要條件

本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：

*   Azure Active Directory 租用戶。
*   您必須擁有 Google Apps for Work 或 Google Apps for Education 的有效租用戶。 您可以使用免費試用帳戶來使用任何服務。
*   Google Apps 中具有小組管理員權限的使用者帳戶。

## <a name="assigning-users-toogoogle-apps"></a>將使用者指派 tooGoogle 應用程式

Azure Active Directory 會使用稱為 「 指派 」 toodetermine 哪些使用者應該會收到存取 tooselected 應用程式的概念。 在 hello 內容中的自動帳戶佈建使用者，會同步處理的 hello 使用者和群組已 「 指派 」 tooan 應用程式在 Azure AD 中。

之前設定，及啟用 hello 佈建服務，您會需要 toodecide 哪些使用者和/或 Azure AD 中的群組代表 hello 使用者需要存取 tooyour Google Apps 的應用程式。 一旦決定，您可以將這些使用者 tooyour Google Apps 應用程式指派 hello 遵循指示：[指派使用者或群組的 tooan 企業應用程式](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   建議在單一 Azure AD 使用者被指派 tooGoogle 應用程式 tootest hello 佈建的組態。 其他使用者及/或群組可能會稍後再指派。
>*   指派使用者 tooGoogle 應用程式時，您必須在 hello 分派 對話方塊中選取 hello 使用者或 「 群組 」 角色。 hello 「 預設的存取 」 角色不適用於佈建。

## <a name="enable-automated-user-provisioning"></a>啟用自動使用者佈建

本節會引導您完成連接您的 Azure AD tooGoogle 應用程式的使用者帳戶佈建應用程式開發介面，並設定佈建服務 toocreate hello、 更新和停用 Azure AD 中的使用者和群組指派為基礎的 Google Apps 中指派的使用者帳戶.

>[!Tip]
>您也可以選擇 tooenabled SAML 型單一登入 Google 應用程式，請遵循所提供的 hello 指示[Azure 入口網站](https://portal.azure.com)。 可以獨立設定自動佈建的單一登入，雖然這兩個功能彼此補充。

### <a name="configure-automatic-user-account-provisioning"></a>設定使用者帳戶自動佈建

> [!NOTE]
> 自動化使用者佈建 tooGoogle 應用程式的另一個可行選項是 toouse [Google 應用程式目錄同步處理 (GADS)](https://support.google.com/a/answer/106368?hl=en)的佈建您的內部部署 Active Directory 身分識別 tooGoogle 應用程式。 相反地，在此教學課程中的 hello 方案佈建您的 Azure Active Directory （雲端） 使用者和群組已啟用郵件 tooGoogle 應用程式。 

1. 登入 hello [Google 應用程式系統管理員主控台](http://admin.google.com/)使用您的系統管理員帳戶，然後按一下**安全性**。 如果您沒有看到 hello 連結，它可能會隱藏在 hello**其他控制項**功能表底部 hello 囉 」 畫面。
   
    ![按一下 [安全性]。][10]

2. 在 hello**安全性**頁面上，按一下**API 參考**。
   
    ![按一下 [API 參考]。][15]

3. 選取 [啟用 API 存取] 。
   
    ![按一下 [API 參考]。][16]

    > [!IMPORTANT]
    > 針對您想 tooprovision tooGoogle 應用程式，其使用者名稱在 Azure Active Directory 中的每個使用者*必須*是 tooa 繫結的自訂網域。 例如，Google Apps 不會接受 bob@contoso.onmicrosoft.com 這樣的使用者名稱，但是會接受 bob@contoso.com。 您可以在 Azure AD 中編輯現有使用者的內容，來變更其網域。 指示 tooset Azure Active Directory 與 Google Apps 的自訂網域如何在中包含下列步驟。
      
4. 如果您尚未加入自訂網域名稱 tooyour Azure Active Directory，然後依照下列步驟的 hello:
  
    a. 在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，按一下**Active Directory**。 在 hello 目錄清單中，選取您的目錄。 

    b. 按一下**網域名稱**在 hello 左側瀏覽窗格，然後按一下**新增**。
     
     ![網域](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![新增網域](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. 您的網域名稱輸入 hello**網域名稱**欄位。 此網域名稱應該是 hello 想要 Google Apps toouse 相同的網域名稱。 準備就緒時，按一下 hello**新增網域** 按鈕。
     
     ![網域名稱](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. 按一下**下一步**toogo toohello 驗證 頁面。 tooverify 您擁有此網域，您必須編輯根據 toohello 值在此頁面提供的 hello 網域的 DNS 記錄。 您可以選擇使用 tooverify **MX 記錄**或**TXT 記錄**，視您選取的 hello**記錄類型**選項。 如需有關如何 tooverify 網域名稱與 Azure AD 的更完整指示，請參閱[加入您自己的網域名稱 tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409)。
     
     ![網域](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. 重複上述步驟，針對您想 tooadd tooyour 目錄的所有 hello 定義域 hello。

5. 您已經向 Azure AD 驗證所有網域，但是您還必須向 Google Apps 再驗證一次。 未與 Google Apps 註冊每個網域，執行下列步驟的 hello:
   
    a. 在 hello [Google 應用程式系統管理員主控台](http://admin.google.com/)，按一下 **網域**。
     
     ![按一下 [網域]][20]

    b.這是另一個 C# 主控台應用程式。 按一下 [新增網域或網域別名] 。
     
     ![新增網域][21]

    c. 選取**新增另一個網域**，然後輸入您想要 tooadd hello 網域之 hello 名稱。
     
     ![輸入您的網域名稱][22]

    d. 按一下 [繼續並驗證網域擁有權]。 然後，遵循 hello 步驟 tooverify 您擁有 hello 網域名稱。 如需如何 tooverify 與 Google Apps 網域查看全方位指示。 [向 Google Apps 驗證網站擁有權](https://support.google.com/webmasters/answer/35179)。

    e. 重複上述步驟，針對您想 tooadd tooGoogle 應用程式的任何其他網域的 hello。
     
     > [!WARNING]
     > 如果您變更您的 Google Apps 租用戶 hello 主要網域，而且如果已經設定單一登入與 Azure AD，則有 toorepeat 步驟 #3 下的[兩個步驟： 啟用單一登入](#step-two-enable-single-sign-on)。
       
6. 在 hello [Google 應用程式系統管理員主控台](http://admin.google.com/)，按一下 **系統管理員角色**。
   
     ![按一下 [Google Apps]][26]

7. 判斷哪一個系統管理員希望 toouse toomanage 使用者佈建的帳戶。 Hello**系統管理員角色**該帳戶中，編輯 hello**權限**該角色。 請確定它擁有所有 hello**管理員 API 的權限**啟用，所以此帳戶可以用於佈建。
   
     ![按一下 [Google Apps]][27]
   
    > [!NOTE]
    > 如果您要設定的實際執行環境，hello 最佳作法是 toocreate Google Apps 中系統管理員帳戶，特別針對此步驟。 這些帳戶必須具備 hello 必要 API 權限系統管理員角色與其相關聯。
     
8. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 toohello **Azure Active Directory > 企業應用程式 > 所有的應用程式**> 一節。

9. 如果您已經設定 Google Apps 的單一登入，搜尋您的 Google Apps 使用 hello 搜尋欄位中的執行個體。 否則，請選取**新增**並搜尋**Google Apps** hello 應用程式庫中。 從 hello 搜尋結果中，選取 Google Apps，並將它加入 tooyour 應用程式清單。

10. 選取您的 Google Apps 的執行個體，然後選取 hello**佈建** 索引標籤。

11. 設定 hello**佈建模式**太**自動**。 

     ![佈建](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. 在 hello**系統管理員認證**區段中，按一下**授權**。 這會在新的瀏覽器視窗中開啟 Google Apps 授權對話方塊。

13. 確認您想要 toogive Azure Active Directory 權限 toomake 變更 tooyour Google Apps 租用戶。 按一下 [接受]。
    
     ![確認權限。][28]

14. 在 hello Azure 入口網站，按一下 **測試連接**tooensure Azure AD 的 tooyour Google Apps 的應用程式可以連接。 如果 hello 連線失敗，請確定您的 Google Apps 帳戶已小組系統管理員權限，然後再次嘗試 hello **「 授權 」**步驟一次。

15. 輸入 hello 的個人或群組應該會收到 hello 中佈建錯誤通知的電子郵件地址**通知電子郵件**欄位，並選取 hello 核取方塊。

16. 按一下 [儲存]。

17. 在 hello 對應區段中，選取**同步處理 Azure Active Directory 使用者 tooGoogle 應用程式。**

18. 在 hello**屬性對應**區段中，檢閱已從 Azure AD tooGoogle 應用程式同步處理的 hello 使用者屬性。 hello 做為所選取的屬性**比對**屬性是使用的 toomatch hello 的使用者帳戶在 Google Apps 中進行更新作業。 選取 hello 儲存按鈕 toocommit 任何變更。

19. tooenable hello Azure AD 佈建服務，針對 Google 應用程式，變更 hello**佈建狀態**太**上**hello 設定 區段中

20. 按一下 [儲存]。

啟動 hello 初始同步處理的任何使用者和/或群組指派 tooGoogle hello 使用者和群組 > 一節中的應用程式。 hello 初始同步處理會較長的 tooperform 比發生大約每隔 20 分鐘，只要 hello 服務正在執行的後續同步處理。 您可以使用 hello**同步處理詳細資料**區段 toomonitor 進度，並遵循連結 tooprovisioning 活動報告，描述由 hello 佈建服務 Google Apps 的應用程式上執行的所有動作。

## <a name="additional-resources"></a>其他資源

* [管理企業應用程式的使用者帳戶佈建](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定單一登入](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png