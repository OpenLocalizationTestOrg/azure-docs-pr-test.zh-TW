---
title: "教學課程：Azure Active Directory 與 Wizergos Productivity Software 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Wizergos 生產力軟體之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a>教學課程：Azure Active Directory 與 Wizergos Productivity Software 整合
本教學課程的 hello 目標是 tooshow 您如何 toointegrate Wizergos 生產力軟體與 Azure Active Directory (Azure AD)。

與 Azure AD 整合 Wizergos 生產力軟體可以提供下列優點 hello:

* 您可以控制存取 tooWizergos 生產力軟體的 Azure AD 中
* 您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooWizergos 生產力軟體單一登入 (SSO)
* 您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
tooconfigure Wizergos 生產力軟體與 Azure AD 整合，您需要下列項目 hello:

* Azure AD 訂用帳戶
* 啟用 Wizergos Productivity Software SSO 的訂用帳戶

>[!NOTE]
>本教學課程中的步驟 tootest hello，不建議使用實際執行環境。 
> 

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

* 除非必要，否則您不應使用生產環境，。
* 如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 的 SSO 在測試環境中。

本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 從 hello 圖庫加入 Wizergos 生產力軟體
2. 設定並測試 Azure AD SSO

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a>從 hello 圖庫加入 Wizergos 生產力軟體
tooconfigure hello 整合 Wizergos 生產力軟體到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Wizergos 生產力軟體。

**tooadd Wizergos 生產力軟體從 hello 組件庫中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。 
   
    ![Active Directory][1]
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。
   
    ![應用程式][2]
4. 按一下**新增**hello hello 頁底端。
   
    ![應用程式][3]
5. 在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。
   
    ![應用程式][4]
6. 在 [hello] 搜尋方塊中，輸入**Wizergos 生產力軟體**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. 在 hello 結果 窗格中，選取  **Wizergos 生產力軟體**，然後按一下**完成**tooadd hello 應用程式。
   
    ![選取在 hello 圖庫中的 hello 應用程式](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>設定並測試 Azure AD SSO
hello 本節目標在於 tooshow 如何 tooconfigure 和測試 Azure AD SSO Wizergos 生產力軟體根據稱為 「 許 Simon"的測試使用者。

SSO toowork Azure AD 需要 tooknow Wizergos 生產力軟體 tooan 使用者在 Azure AD 中哪些 hello 對等項目的使用者。 換句話說，Azure AD 使用者與 hello Wizergos 生產力軟體中的相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Wizergos 生產力軟體中。

tooconfigure 及 BynWizergos 產能 Softwareder 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
3. **[建立 Wizergos 生產力軟體測試使用者](#creating-a-wizergos-productivity-software-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Wizergos 生產力軟體中對應項目。
4. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-sso"></a>設定 Azure AD SSO
在本節中，您可以啟用 Azure AD 單一登入 hello 傳統入口網站中，並 Wizergos 生產力軟體應用程式中設定單一登入。

**tooconfigure Azure AD 單一登入 Wizergos 生產力軟體，執行下列步驟的 hello:**

1. Hello 傳統入口網站中，在 hello **Wizergos 生產力軟體**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。
   
    ![設定單一登入][6] 
2. 在 hello**如何想您使用者 toosign tooWizergos 生產力軟體上**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**:
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. 在 hello**設定應用程式設定**對話方塊頁面上，按一下 **下一步**:
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. 在 hello**於 Wizergos 產能 Software 設定單一登入**頁面上，按一下**下載憑證**，然後儲存您的電腦上的 hello 檔案：
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Wizergos 生產力軟體租用戶。
6. 從 hello 漢堡功能表上，選取**Admin**。
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. 在 [系統管理] 頁面左側的功能表中，選取 [驗證]，然後按一下 [Azure AD]。
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. 執行下列步驟 hello**驗證**> 一節。
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. 按一下**上傳**按鈕 tooupload hello Azure AD 從下載的憑證。 
  2. 在 hello**簽發者 URL**文字方塊放 hello 值**簽發者 URL**從 Azure AD 應用程式組態精靈。
  3. 在 hello**單一登入 URL**文字方塊放 hello 值**單一登入服務 URL**從 Azure AD 應用程式組態精靈。
  4. 在 hello**單一登出 URL**文字方塊放 hello 值**單一登出服務 URL**從 Azure AD 應用程式組態精靈。
  5. 按一下 [儲存]  按鈕。
9. Hello 傳統入口網站中選取 hello 單一登入組態確認，然後**下一步**。
   
    ![Azure AD 單一登入][10]
10. 在 hello**單一登入確認**頁面上，按一下**完成**。  
    
    ![Azure AD 單一登入][11]

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節 hello 目標是 toocreate 測試使用者呼叫許 Simon hello 傳統入口網站中。

![建立 Azure AD 使用者][20]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. 從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。
3. toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. 在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. 針對 [使用者類型]，選取 [您組織中的新使用者]。
  2. 在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。
  3. 按一下 [下一步] 。
6. 在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. 在 hello**名字**文字方塊中，輸入**許**。  
  2. 在 hello**姓氏**文字方塊中，輸入， **Simon**。
  3. 在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。
  4. 在 hello**角色**清單中，選取**使用者**。
  5. 按一下 [下一步] 。
7. 在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. 在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. 請記下 hello hello 值**新密碼**。
  2. 按一下頁面底部的 [新增] 。   

### <a name="create-a-wizergos-productivity-software-test-user"></a>建立 Wizergos Productivity Software 測試使用者
在本節中，您要在 Wizergos Productivity Software 中建立名為 Britta Simon 的使用者。 請使用透過 Wizergos 生產力軟體支援小組[ support@wizergos.com ](emailTo:support@wizergos.com) tooadd hello hello Wizergos 生產力軟體平台的使用者。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者
本節 hello 目標是 tooenabling 許 Simon toouse Azure SSO 授與他們存取 tooWizergos 生產力軟體。

  ![指派使用者][200]

**tooassign 許 Simon tooWizergos 生產力軟體，執行下列步驟的 hello:**

1. Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。
   
    ![指派使用者][201]
2. 在 [hello] 應用程式清單中，選取**Wizergos 生產力軟體**。
   
    ![設定單一登入](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. 在 hello 最上層顯示 hello 功能表上，按一下**使用者**。
   
    ![指派使用者][203]
4. 在 hello 使用者清單中選取**許 Simon**。
5. 在 hello hello 底部的工具列中按一下**指派**。
   
    ![指派使用者][205]

### <a name="test-single-sign-on"></a>測試單一登入
hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。

當您按一下 hello Wizergos 生產力軟體磚 hello 存取面板中的時，您應該取得自動登入 tooyour Wizergos 生產力軟體應用程式。

## <a name="additional-resources"></a>其他資源
* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
