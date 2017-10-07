---
title: "教學課程：Azure Active Directory 與 Workplace by Facebook 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與工作地點的 Facebook 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>教學課程：Azure Active Directory 與 Workplace by Facebook 整合

在此教學課程中，您學會如何 toointegrate 由 Facebook 與 Azure Active Directory (Azure AD) 的工作場所。

與 Azure AD 整合的 Facebook 的工作地點可以提供下列優點的 hello:

- 您可以控制存取 tooWorkplace 由 Facebook 的 Azure AD 中。
- 您可以啟用您 tooautomatically 取得以登入 tooWorkplace Facebook （單一登入） 透過其 Azure AD 帳戶的使用者。
- 您可以管理您的帳戶，在單一中央位置： hello Azure 入口網站。

如需軟體即服務 (SaaS) 應用程式與 Azure AD 整合的更多詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure 由 Facebook 的工作場所的 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 Workplace by Facebook (SSO) 單一登入的訂用帳戶

tootest hello 步驟在本教學課程，請遵循下列建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD SSO。 本教學課程所述的 hello 案例包含兩個主要建置組塊：

1. 加入工作地點的 Facebook 從 hello 組件庫。
2. 設定和測試 Azure AD 單一登入。

## <a name="add-workplace-by-facebook-from-hello-gallery"></a>加入工作地點的 Facebook 從 hello 組件庫
tooconfigure hello 整合工作地點的 Facebook 到 Azure AD 中，加入工作地點的 Facebook hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左的窗格中選取**Azure Active Directory**。 

    ![hello Azure Active Directory 按鈕][1]

2. 瀏覽過**企業應用程式** > **所有應用程式**。

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. tooadd hello 新應用程式，選取**新的應用程式**hello 最上層顯示 hello 對話方塊。

    ![hello 新應用程式按鈕][3]

4. Hello 搜尋方塊中，輸入**工作地點的 Facebook**，然後選取**工作地點的 Facebook**從結果中。 然後選取**新增**，tooadd hello 應用程式。

    ![由 Facebook hello [結果] 清單中的工作場所](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Workplace by Facebook 搭配運作的 Azure AD SSO。

SSO toowork Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者工作地點的 Facebook 都 tooa 使用者在 Azure AD 中。 換句話說，您應該建立 Azure AD 使用者與工作地點的 Facebook 中的 hello 相關的使用者之間的連結關聯性。

此關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**由 Facebook 的工作地點中。

### <a name="configure-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，hello Azure 入口網站中啟用 Azure AD 的 SSO 與您工作地點中設定 SSO 的 Facebook 應用程式。

1. 在 Azure 入口網站上 hello hello**工作地點的 Facebook**應用程式整合頁面上，選取**單一登入**。

    ![設定單一登入連結][4]

2. 在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable SSO。
 
    ![單一登入對話方塊](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. 在 hello **Facebook 網域和 Url 的工作場所**區段中，執行下列 hello:

    a. 在 hello**登入 URL**文字方塊中，輸入使用下列模式的 hello 的 URL:`https://<company subdomain>.facebook.com`

    b. 在 hello**識別碼**文字方塊中，輸入使用下列模式的 hello 的 URL:`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > 這些值僅為範例。 更新這些值與 hello 實際登入 URL 和識別碼。 連絡 hello [Facebook 用戶端支援小組的工作場所](https://workplace.fb.com/faq/)tooget 這些值。 

4. 在 hello **SAML 簽章憑證**區段中，選取**憑證 (Base64)**，然後儲存您的電腦上的 hello 憑證檔案。

    ![hello 憑證下載連結](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. 選取 [ **儲存**]。

    ![設定單一登入儲存按鈕](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. 在 hello **Facebook 組態的工作場所**區段中，選取**Facebook 所設定的工作場所**tooopen hello**設定登入**視窗。 複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考**> 一節。

    ![Workplace by Facebook 設定](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. 在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Facebook 公司網站的工作場所。
  
   > [!NOTE] 
   > Hello SAML 驗證程序的一部分，工作地點可以使用向上 too2.5 kb 為單位的查詢字串的大小順序 toopass 參數 tooAzure AD 中。

8. 在 [hello**公司儀表板**，go toohello**驗證**] 索引標籤。

9. 在下**SAML 驗證**，選取**只有 SSO** hello 下拉式清單中。

10. 輸入 hello 值從 hello 複製**Facebook 組態的工作場所**hello hello 對應欄位中的 Azure 入口網站的區段：

    *   在**SAML URL**  文字方塊中，貼上 hello 值**單一登入服務 URL**，從 hello Azure 入口網站複製的。
    *   在**SAML 簽發者 URL**  文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 hello Azure 入口網站複製的。
    *   在**SAML 登出重新導向 （選擇性）**，貼上的 hello 值**登出 URL**，從 hello Azure 入口網站複製的。
    *   開啟您**base 64 編碼憑證**，在 [記事本]，從 hello Azure 入口網站下載。 Hello 內容複製到剪貼簿，然後將它貼入 toothe **SAML 憑證**文字方塊。

11. 您可能需要 tooenter hello 觀眾 URL、 收件者的 URL 和 ACS （判斷提示取用者服務） URL，列在 hello **SAML 設定**> 一節。

12. 捲動 toohello 底部 hello 區段中，並選取**測試 SSO**。 快顯視窗隨即出現，並 hello Azure AD 登入頁面。 tooauthenticate，像平常一樣，輸入您的認證。 請從 Azure AD 傳回的 hello 電子郵件地址是 hello 與 hello 您用來登入的工作場所帳戶相同。

13. 如果 hello 測試成功完成後，捲動 toohello hello 頁面並選取底部**儲存**。

14. 使用 Workplace 的所有使用者現在都會看到進行驗證的 Azure AD 登入頁面。

您可以選擇 tooconfigure URL，可以在 hello Azure AD 的登出頁面使用的 toopoint SAML 登出。 當此設定已啟用並設定時，hello 使用者已不再導向的 toohello 工作地點的登出頁面。 相反地，hello 使用者是已加入 hello SAML 登出重新導向設定中的重新導向的 toohello URL。


> [!TIP]
> 您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式。 加入此應用程式從 hello 之後**Active Directory** > **企業應用程式**區段中，只需選取 hello**單一登入** 索引標籤，並存取 hello內嵌文件，透過 hello**組態**hello 底部的區段。 閱讀更多有關 hello embedded 文件功能的 hello [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。

### <a name="configure-reauthentication-frequency"></a>設定重新驗證頻率

您可以設定 SAML 檢查每一天，三天一週、 兩週，一個月的工作場所 tooprompt 或永遠不會。

> [!NOTE] 
>hello hello SAML 檢查行動應用程式的最小值設定 tooone 週。

您也可以強制所有使用者重設 SAML。 toodo，使用 hello**需要 SAML 驗證所有使用者現在** 按鈕。


### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。

![建立 Azure AD 使用者][100]

1. 在 hello **Azure 入口網站**，在 hello 左的窗格中選取**Azure Active Directory**。

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. toodisplay hello 使用者清單，請移過**使用者和群組**，然後選取**所有使用者**。
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. tooopen hello**使用者**對話方塊中，選取**新增**。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. 在 hello**使用者**對話方塊方塊中，執行下列 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    a. 在 hello**名稱**文字方塊中，輸入**BrittaSimon**。

    b. 在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。

    c. 選取 [顯示密碼]，並將它寫下來。

    d. 選取 [ **建立**]。
 
### <a name="create-a-workplace-by-facebook-test-user"></a>建立 Workplace by Facebook 測試使用者

本節會在 Workplace by Facebook 中建立名為 Britta Simon 的使用者。 Workplace by Facebook 支援預設啟用的 Just-In-Time 佈建。

在這一節沒有您需要進行的動作。 如果使用者不存在的 Facebook 的工作地點中，建立一個新是當您嘗試 tooaccess 工作地點的 Facebook。

>[!Note]
>若要手動 toocreate 使用者，請連絡 hello [Facebook 用戶端支援小組的工作場所](https://workplace.fb.com/faq/)。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，以啟用許 Simon toouse Azure SSO 授與存取 tooWorkplace 由 Facebook。

![指派使用者][200] 

1. 在 hello Azure 入口網站，開啟 hello 應用程式檢視。 移 toohello 目錄檢視，請移過**企業應用程式**，然後選取**所有應用程式**。

    ![指派使用者][201] 

2. 在 [hello] 應用程式清單中，選取**工作地點的 Facebook**。

    ![Facebook hello 應用程式清單中每個連結的 hello 工作場所](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. 在左側 hello hello 功能表中選取**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202] 

4. 選取 [新增] 。 然後，在 hello**將作業加入**窗格中，選取**使用者和群組**。

    ![hello 將作業加入窗格][203]

5. 在 [hello**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。

6. 在 hello**使用者和群組**對話方塊中，選取**選取**。

7. 在 hello**將作業加入**對話方塊中，選取**指派**。
    
### <a name="test-single-sign-on"></a>測試單一登入

如果您想 tootest SSO 設定，請開啟 hello 存取面板。
如需詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。


## <a name="next-steps"></a>後續步驟

* 請參閱 hello[如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)。
* 閱讀[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。
* 深入了解如何太[設定使用者佈建](active-directory-saas-facebook-at-work-provisioning-tutorial.md)。



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

