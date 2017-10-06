---
title: "教學課程：整合 Azure Active Directory 與 vxMaintain | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 vxMaintain 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>教學課程：整合 Azure Active Directory 與 vxMaintain

在此教學課程中，您學會如何 toointegrate vxMaintain 與 Azure Active Directory (Azure AD)。

這項整合提供一些重要優勢。 您可以：

- 在具有 Azure AD 中的控制項存取 toovxMaintain。
- 使用其 Azure AD 帳戶，以啟用您的使用者 tooautomatically 登入 toovxMaintain 搭配單一登入 (SSO)。
- 管理您的帳戶，在單一中央位置： hello Azure 入口網站。

toolearn 進一步了解 SaaS 應用程式整合，使用 Azure AD，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

tooconfigure vxMaintain 與 Azure AD 整合，您需要下列項目 hello:

- Azure AD 訂用帳戶
- 已啟用 vxMaintain SSO 的訂用帳戶

> [!NOTE]
> 當您測試 hello 步驟在本教學課程時，我們建議您不要使用實際執行環境。

tootest hello 步驟在本教學課程，請遵循下列建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 

本教學課程中概述的 hello 案例包含兩個主要建置組塊：

* 從 hello 圖庫加入 vxMaintain
* 設定並測試 Azure AD 單一登入

## <a name="add-vxmaintain-from-hello-gallery"></a>從 hello 圖庫新增 vxMaintain
tooconfigure hello vxMaintain 與 Azure AD 整合，您需要 tooadd vxMaintain hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。

從 hello 圖庫 tooadd vxMaintain hello 遵循：

1. 在 [hello [Azure 入口網站](https://portal.azure.com)，在 [hello 左的窗格中選取 hello **Azure Active Directory** ] 按鈕。 

    ![hello Azure Active Directory] 按鈕][1]

2. 選取 [企業應用程式] > [所有應用程式]。

    ![hello 「 企業應用程式 」 窗格][2]
    
3. 應用程式，在 hello tooadd**所有應用程式**對話方塊中，選取**新的應用程式**。

    ![hello 「 新的應用程式 」 按鈕][3]

4. 在 [hello] 搜尋方塊中，輸入**vxMaintain**。

    ![hello 「 單一登入模式 」 的下拉式清單](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. 在 [hello 結果清單中，選取 [ **vxMaintain**，然後選取**新增**。

    ![hello vxMaintain 連結](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，使用 vxMaintain 設定及測試 Azure AD SSO。

SSO toowork Azure AD 需要 tooknow hello vxMaintain 對應項目 toohello Azure AD 使用者。 也就是說，您必須建立 hello Azure AD 使用者與 hello 對應 vxMaintain 使用者之間的連結關聯性。

tooestablish hello 連結關聯性，指派 hello vxMaintain**使用者名**值為 hello Azure AD **Username**值。

tooconfigure 和測試 Azure AD SSO 使用 vxMaintain，完成下列建置組塊的 hello。

### <a name="configure-azure-ad-sso"></a>設定 Azure AD SSO

在本節中，您可在 hello Azure 入口網站中啟用 Azure AD 的 SSO 和 vxMaintain 應用程式中設定 SSO，藉由下列 hello:

1. 在 Azure 入口網站上 hello hello **vxMaintain**應用程式整合頁面上，選取**單一登入**。

    ![hello 「 單一登入 」 的命令][4]

2. 在 [hello tooenable SSO，**單一登入模式**下拉式清單中，選取**SAML 型登入**。
 
    ![hello [SAML 型登入] 命令](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. 在下**vxMaintain 網域和 Url**，請勿遵循 hello:

    ![hello vxMaintain 網域和 Url 的區段](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    a. 在 [hello**識別碼**方塊中，輸入 URL，請使用下列語法已經 hello:`https://<company name>.verisae.com`

    b. 在 [hello**回覆 URL**方塊中，輸入 URL，請使用下列語法已經 hello:`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > hello 上述值不是實際。 更新 hello 實際識別項，回覆 URL。 tooobtain hello 值，請連絡 hello [vxMaintain 支援小組](http://www.verisae.com/contact-us)。
 
4. 在下**SAML 簽章憑證**，選取**中繼資料 XML**，然後儲存 hello 中繼資料檔案 tooyour 電腦。

    ![hello 「 SAML 簽章憑證 」 一節](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. 選取 [ **儲存**]。

    ![hello [儲存] 按鈕](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** SSO，傳送嗨下載**中繼資料 XML**檔案 toohello [vxMaintain 支援小組](http://www.verisae.com/contact-us)。

> [!TIP]
> 當您設定 hello 應用程式時，您可以閱讀 hello hello 中前面指示的精簡版本[Azure 入口網站](https://portal.azure.com)。 從 hello 新增 hello 應用程式之後**Active Directory** > **企業應用程式**區段中，選取 hello**單一登入**] 索引標籤，然後再存取 hello內嵌文件從 hello**組態**> 一節。 
>
>toolearn 進一步了解 hello embedded 文件功能，請參閱[管理單一登入企業應用程式](https://go.microsoft.com/fwlink/?linkid=845985)。
> 

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
在本節中，您可以建立 hello Azure 入口網站中的測試使用者許 Simon 執行 hello 下列：

![hello Azure AD 的測試使用者][100]

1. 在 [hello **Azure 入口網站**，在 [hello 左的窗格中選取 hello **Azure Active Directory** ] 按鈕。

    ![hello"Azure Active Directory"的按鈕](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. toodisplay 使用者清單，請移過**使用者和群組** > **所有使用者**。
    
    ![hello，"All users"連結](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    hello**所有使用者**對話方塊隨即開啟。 

3. tooopen hello**使用者**對話方塊中，選取**新增**。
 
    ![hello [新增] 按鈕](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. 在 [hello**使用者**對話方塊方塊中，執行下列 hello:
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    a. 在 [hello**名稱**方塊中，輸入**BrittaSimon**。

    b. 在 [hello**使用者名**方塊中，測試使用者許 Simon 類型 hello 電子郵件地址。

    c. 選取 hello**顯示密碼**核取方塊，然後注意 hello 值所產生的 hello**密碼**方塊。

    d. 選取 [ **建立**]。
 
### <a name="create-a-vxmaintain-test-user"></a>建立 vxMaintain 測試使用者

在本節中，您會在 vxMaintain 中建立測試使用者 Britta Simon。 在 hello vxMaintain 平台中，tooadd 使用者使用[vxMaintain 支援小組](http://www.verisae.com/contact-us)。 使用 SSO 之前，先建立及啟動 hello 的使用者。

### <a name="assign-hello-azure-ad-test-user"></a>指派給 Azure AD hello 測試使用者

在本節中，您可以授與存取 toovxMaintain 啟用測試使用者許 Simon toouse Azure SSO。 toodo，請勿 hello 遵循：

![Hello 顯示名稱清單中的測試使用者][200] 

1. 在 Azure 入口網站 hello**應用程式**檢視，請進入太**目錄**檢視 >**企業應用程式** > **的所有應用程式**.

    ![hello [所有應用程式] 連結][201] 

2. 在 [hello**應用程式**清單中，選取**vxMaintain**。

    ![hello vxMaintain 連結](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. Hello 左窗格中，選取**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][202] 

4. 選取**新增**，然後在 hello**將作業加入**窗格中，選取**使用者和群組**。

    ![hello 「 使用者和群組 」 的連結][203]

5. 在 hello**使用者和群組**對話方塊中的，在 hello**使用者**清單中，選取**許 Simon**，然後選取 [hello**選取**] 按鈕。

7. 在 [hello**將作業加入**對話方塊中，選取**指派**。
    
### <a name="test-your-azure-ad-single-sign-on"></a>測試您的 Azure AD 單一登入

本節中，在中，您可以測試您的 Azure AD 的 SSO 組態使用 hello 存取面板。

選取 hello **vxMaintain** hello 存取面板中的圖格應該自動登入 tooyour vxMaintain 應用程式。

如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。

## <a name="next-steps"></a>後續步驟

* [整合 SaaS 應用程式與 Azure Active Directory 的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

