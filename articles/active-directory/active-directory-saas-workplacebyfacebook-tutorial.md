---
title: "教學課程：Azure Active Directory 與 Workplace by Facebook 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與工作地點的 Facebook 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>教學課程：Azure Active Directory 與 Workplace by Facebook 整合

在此教學課程中，您學會如何 toointegrate 由 Facebook 與 Azure Active Directory (Azure AD) 的工作場所。

與 Azure AD 整合的 Facebook 的工作地點可以提供下列優點的 hello:

- 您可以控制存取 tooWorkplace 由 Facebook 的 Azure AD 中
- 您可以啟用您的使用者 tooautomatically get 登入 tooWorkplace 由 Facebook （單一登入） 具有其 Azure AD 帳戶
- 您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站

如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 由 Facebook 的工作場所的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Workplace by Facebook 單一登入的訂用帳戶

> [!NOTE]
> 本教學課程中的步驟 tootest hello，不建議使用實際執行環境。

在本教學課程 tootest hello 步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 由 Facebook 從 hello 組件庫加入工作地點
2. 設定並測試 Azure AD 單一登入

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>由 Facebook 從 hello 組件庫加入工作地點
tooconfigure hello 整合工作地點的 Facebook 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 由 Facebook 的工作場所。

**由 Facebook hello 圖庫中，從工作場所 tooadd 執行 hello 下列步驟：**

1. 在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。 

    ![Active Directory][1]

2. 瀏覽過**企業應用程式**。 然後跳過**所有應用程式**。

    ![應用程式][2]
    
3. tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。

    ![應用程式][3]

4. 在 [hello] 搜尋方塊中，輸入**工作地點的 Facebook**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. 在 hello [結果] 窗格中，選取**工作地點的 Facebook**，然後按一下**新增**按鈕 tooadd hello 應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Workplace by Facebook 搭配運作的 Azure AD 單一登入。

單一登入 toowork，Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者工作地點的 Facebook 都 tooa 使用者在 Azure AD 中。 換句話說，Azure AD 使用者與工作地點的 Facebook 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。

此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**由 Facebook 的工作地點中。

tooconfigure 和測試 Azure AD 單一登入的 Facebook 的工作場所，您需要遵循的建置組塊 toocomplete hello:

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。
2. **[設定重新驗證頻率](#configuring-reauthentication-frequency)** -tooconfigure 工作場所 tooprompt SAML 檢查。
3. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。
4. **[建立 Facebook 測試使用者工作地點](#creating-a-workplace-by-facebook-test-user)** -toohave 許 Simon 由是連結的 toohello Azure AD 使用者表示法的 Facebook 的工作地點中對應項目。
5. **[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。
6. **[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您工作地點中的 Facebook 應用程式。

**tooconfigure Azure AD 單一登入的工作地點網路，由 Facebook，執行下列步驟的 hello:**

1. 在 Azure 入口網站上 hello hello**工作地點的 Facebook**應用程式整合頁面上，按一下**單一登入**。

    ![設定單一登入][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。
 
    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. 在 hello **Facebook 網域和 Url 的工作場所**區段中，執行下列步驟的 hello:

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    a. 在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.facebook.com`

    b. 在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > 這些值不是真正的 hello。 更新這些值與實際的 hello 登入 URL 和識別項。 請連絡[Facebook 用戶端支援小組的工作場所](https://workplace.fb.com/faq/)tooget 這些值。 

4. 在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. 在 hello **Facebook 組態的工作場所**區段中，按一下**Facebook 所設定的工作場所**tooopen**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. 在不同的網頁瀏覽器視窗中，登入 tooyour 由系統管理員身分的 Facebook 公司網站的工作場所。
  
   > [!NOTE] 
   > Hello SAML 驗證程序的一部分，工作地點可能利用向上 too2.5 kb 大小順序 toopass 參數 tooAzure AD 中的查詢字串。

8. 在 [hello**公司儀表板**，go toohello**驗證**] 索引標籤。

9. 在下**SAML 驗證**，選取**只有 SSO** hello 下拉式清單中。

10. 從複製輸入的 hello 值**Facebook 組態的工作場所**hello hello 對應欄位中的 Azure 入口網站的區段：

    *   在**SAML URL**文字方塊中，貼上 hello 值**單一登入服務 URL**，從 Azure 入口網站複製的。
    *   在**SAML 簽發者 URL 文字方塊中**，貼上的 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。
    *   在**SAML 登出重新導向**（選擇性），貼上的 hello 值**登出 URL**，從 Azure 入口網站複製的。
    *   開啟您**base 64 編碼憑證**從 Azure 入口網站下載 [記事本] 中的 hello 內容複製到剪貼簿，並貼 toothe **SAML 憑證**文字方塊。

11. 您可能需要 tooenter hello 觀眾 URL 收件者 URL 和 ACS （判斷提示取用者服務） 的 URL 列在 hello **SAML 設定**> 一節。

12. 捲動 toohello hello 區段的底部，按一下 [hello**測試 SSO** ] 按鈕。 快顯視窗中的這個結果隨即顯示，並會出現 Azure AD 登入頁面。 輸入您的認證，在做為一般 tooauthenticate。 

    **疑難排解：**請從 Azure AD 傳回的 hello 電子郵件地址是 hello 與 hello 您用來登入的工作場所帳戶相同。

13. 一旦 hello 測試已順利完成，請捲動 toohello hello 頁面的底部，然後按一下 hello**儲存** 按鈕。

14. 現在，使用 Workplace 的所有使用者都將會看到進行驗證的 Azure AD 登入頁面。

15. **SAML 登出重新導向 (選擇性)** - 

    您可以選擇 toooptionally 設定 SAML 登出 Url，可能會在 Azure AD 的登出頁面使用的 toopoint。 當此設定已啟用並設定時，hello 使用者將無法再導向的 toohello 工作場所登出頁面。 相反地，hello 使用者將其加入 hello SAML 登出重新導向設定中的重新導向的 toohello url。


> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！  加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>設定重新驗證頻率

您可以設定工作地點 tooprompt 的 SAML 檢查每一天，三天、 週、 兩週、 月或永遠不會。

> [!NOTE] 
>hello hello SAML 檢查行動應用程式的最小值設定 tooone 週。

您也可以強制所有使用者使用 hello 按鈕重設 SAML： 需要 SAML 驗證所有使用者現在。


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**

1. 在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取**顯示密碼**記下 hello hello 值**密碼**。

    d. 按一下 [建立] 。
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>建立 Workplace by Facebook 測試使用者

本節會在 Workplace by Facebook 中建立名為 Britta Simon 的使用者。 Workplace by Facebook 支援預設啟用的 Just-In-Time 佈建。

在這一節沒有您需要進行的動作。 如果使用者不存在的 Facebook 的工作地點中，建立一個新是當您嘗試 tooaccess 工作地點的 Facebook。

>[!Note]
>如果您需要以手動方式，請連絡使用者 toocreate [Facebook 用戶端支援小組的工作場所](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>指派 hello Azure AD 的測試使用者

在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooWorkplace 由 Facebook。

![指派使用者][200] 

**tooassign 許 Simon tooWorkplace 由 Facebook，執行下列步驟的 hello:**

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**工作地點的 Facebook**。

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. 在左側 hello hello 功能表上，按一下**使用者和群組**。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。
如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。


## <a name="additional-resources"></a>其他資源

* [如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定使用者佈建](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

