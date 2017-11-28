---
title: "教學課程：Azure Active Directory 與 Adobe Sign 整合 | Microsoft Docs"
description: "了解如何 tooconfigure 單一登入 Azure Active Directory 與 Adobe 號之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="c3e37-103">教學課程：Azure Active Directory 與 Adobe Sign 整合</span><span class="sxs-lookup"><span data-stu-id="c3e37-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="c3e37-104">在此教學課程中，您學會如何 toointegrate Adobe 登入與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c3e37-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3e37-105">與 Azure AD 整合 Adobe 登可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="c3e37-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c3e37-106">您可以控制存取 tooAdobe 正負號的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="c3e37-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="c3e37-107">您可以啟用您使用者 tooautomatically get 登入 tooAdobe 符號 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="c3e37-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3e37-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c3e37-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c3e37-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c3e37-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3e37-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c3e37-110">Prerequisites</span></span>

<span data-ttu-id="c3e37-111">tooconfigure 與 Adobe 正負號的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c3e37-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="c3e37-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c3e37-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3e37-113">已啟用 Adobe Sign 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c3e37-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3e37-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c3e37-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3e37-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c3e37-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3e37-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c3e37-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3e37-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c3e37-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3e37-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c3e37-118">Scenario description</span></span>
<span data-ttu-id="c3e37-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c3e37-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3e37-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c3e37-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3e37-121">從 hello 圖庫加入 Adobe 符號</span><span class="sxs-lookup"><span data-stu-id="c3e37-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="c3e37-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c3e37-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="c3e37-123">從 hello 圖庫加入 Adobe 符號</span><span class="sxs-lookup"><span data-stu-id="c3e37-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="c3e37-124">tooconfigure hello 整合 Adobe 登入 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Adobe 符號。</span><span class="sxs-lookup"><span data-stu-id="c3e37-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c3e37-125">**tooadd Adobe 登 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c3e37-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3e37-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c3e37-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3e37-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c3e37-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c3e37-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c3e37-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c3e37-133">在 [hello] 搜尋方塊中，輸入**Adobe 登**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-133">In hello search box, type **Adobe Sign**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="c3e37-135">在 hello 結果 窗格中，選取  **Adobe 登**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3e37-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3e37-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c3e37-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3e37-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Adobe Sign 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c3e37-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c3e37-139">單一登入 toowork，Azure AD 需要 tooknow Adobe 正負號的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c3e37-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="c3e37-140">換句話說，Azure AD 使用者與 hello Adobe 正負號的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="c3e37-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="c3e37-141">在 Adobe 登 hello hello 值指派**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c3e37-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c3e37-142">tooconfigure 和測試 Azure AD 單一登入以 Adobe 號，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c3e37-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c3e37-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c3e37-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c3e37-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c3e37-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3e37-145">**[建立測試使用者 Adobe 登](#creating-an-adobe-sign-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Adobe 正負號的對應項目。</span><span class="sxs-lookup"><span data-stu-id="c3e37-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3e37-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c3e37-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3e37-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c3e37-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3e37-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c3e37-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3e37-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Adobe 簽署應用程式中。</span><span class="sxs-lookup"><span data-stu-id="c3e37-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="c3e37-150">**tooconfigure Azure AD 單一登入以 Adobe 符號，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c3e37-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3e37-151">在 Azure 入口網站上 hello hello **Adobe 登**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c3e37-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c3e37-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="c3e37-155">在 hello **Adobe 登網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c3e37-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="c3e37-157">a.</span><span class="sxs-lookup"><span data-stu-id="c3e37-157">a.</span></span> <span data-ttu-id="c3e37-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="c3e37-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="c3e37-159">b.</span><span class="sxs-lookup"><span data-stu-id="c3e37-159">b.</span></span> <span data-ttu-id="c3e37-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="c3e37-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c3e37-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c3e37-161">These values are not real.</span></span> <span data-ttu-id="c3e37-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="c3e37-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c3e37-163">請連絡[Adobe 簽署用戶端支援小組](https://helpx.adobe.com/in/contact/support.html)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="c3e37-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="c3e37-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="c3e37-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="c3e37-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c3e37-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3e37-168">在 hello **Adobe 簽署設定**區段中，按一下**設定 Adobe 登**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="c3e37-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c3e37-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="c3e37-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="c3e37-171">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Adobe 登公司網站。</span><span class="sxs-lookup"><span data-stu-id="c3e37-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="c3e37-172">在 hello 最上層顯示 hello 功能表上，按一下**帳戶**，然後 hello hello 左側瀏覽窗格中按一下**SAML 設定**下**帳戶設定**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="c3e37-173">![帳戶](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "帳戶")</span><span class="sxs-lookup"><span data-stu-id="c3e37-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="c3e37-174">在 hello SAML 設定 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c3e37-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="c3e37-175">![SAML 設定](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="c3e37-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="c3e37-176">a.</span><span class="sxs-lookup"><span data-stu-id="c3e37-176">a.</span></span> <span data-ttu-id="c3e37-177">針對 [SAML 模式]，選取 [SAML 強制]。</span><span class="sxs-lookup"><span data-stu-id="c3e37-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="c3e37-178">b.</span><span class="sxs-lookup"><span data-stu-id="c3e37-178">b.</span></span> <span data-ttu-id="c3e37-179">選取**中使用其 EchoSign 認證允許 EchoSign 帳戶系統管理員 toolog**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="c3e37-180">c.</span><span class="sxs-lookup"><span data-stu-id="c3e37-180">c.</span></span> <span data-ttu-id="c3e37-181">針對 [使用者建立]，選取 [透過 SAML 自動新增已驗證的使用者]。</span><span class="sxs-lookup"><span data-stu-id="c3e37-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="c3e37-182">繼續執行，執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c3e37-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="c3e37-183">![SAML 設定](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="c3e37-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="c3e37-184">a.</span><span class="sxs-lookup"><span data-stu-id="c3e37-184">a.</span></span> <span data-ttu-id="c3e37-185">貼上**SAML 實體識別碼**，其中您從 Azure 入口網站複製到 hello **IdP 實體識別碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c3e37-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="c3e37-186">b.</span><span class="sxs-lookup"><span data-stu-id="c3e37-186">b.</span></span> <span data-ttu-id="c3e37-187">貼上**SAML 單一登入服務 URL**，其中您從 Azure 入口網站複製到 hello **IdP 登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c3e37-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="c3e37-188">c.</span><span class="sxs-lookup"><span data-stu-id="c3e37-188">c.</span></span> <span data-ttu-id="c3e37-189">貼上**登出 URL**，其中您從 Azure 入口網站複製到 hello **IdP 登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c3e37-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="c3e37-190">d.</span><span class="sxs-lookup"><span data-stu-id="c3e37-190">d.</span></span> <span data-ttu-id="c3e37-191">開啟您下載**Certificate(Base64)** [記事本]，複製 hello 到剪貼簿，它的內容中，然後將它貼入 toohello **IdP 憑證**文字方塊</span><span class="sxs-lookup"><span data-stu-id="c3e37-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="c3e37-192">e.</span><span class="sxs-lookup"><span data-stu-id="c3e37-192">e.</span></span> <span data-ttu-id="c3e37-193">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="c3e37-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="c3e37-194">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="c3e37-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c3e37-195">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="c3e37-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c3e37-196">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3e37-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3e37-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c3e37-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3e37-198">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c3e37-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c3e37-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c3e37-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3e37-201">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c3e37-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3e37-203">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3e37-205">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="c3e37-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3e37-207">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c3e37-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3e37-209">a.</span><span class="sxs-lookup"><span data-stu-id="c3e37-209">a.</span></span> <span data-ttu-id="c3e37-210">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3e37-211">b.</span><span class="sxs-lookup"><span data-stu-id="c3e37-211">b.</span></span> <span data-ttu-id="c3e37-212">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c3e37-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3e37-213">c.</span><span class="sxs-lookup"><span data-stu-id="c3e37-213">c.</span></span> <span data-ttu-id="c3e37-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c3e37-215">d.</span><span class="sxs-lookup"><span data-stu-id="c3e37-215">d.</span></span> <span data-ttu-id="c3e37-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c3e37-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="c3e37-217">建立 Adobe Sign 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c3e37-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="c3e37-218">tooenable Azure AD 使用者 toolog 中 tooAdobe 符號，它們必須佈建到 Adobe 符號。</span><span class="sxs-lookup"><span data-stu-id="c3e37-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="c3e37-219">在 Adobe 正負號的 hello 情況下，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="c3e37-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="c3e37-220">您可以使用任何其他 Adobe 登使用者帳戶建立工具或 Api 提供 Adobe 登 tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3e37-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="c3e37-221">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c3e37-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3e37-222">登入 tooyour **Adobe 登**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="c3e37-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="c3e37-223">在 hello 最上層顯示 hello 功能表上，按一下**帳戶**，然後 hello hello 左側瀏覽窗格中按一下**使用者和群組**，然後按一下 **建立新的使用者**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="c3e37-224">![帳戶](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "帳戶")</span><span class="sxs-lookup"><span data-stu-id="c3e37-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="c3e37-225">在 hello**建立新的使用者**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c3e37-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="c3e37-226">![建立使用者](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="c3e37-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="c3e37-227">a.</span><span class="sxs-lookup"><span data-stu-id="c3e37-227">a.</span></span> <span data-ttu-id="c3e37-228">型別 hello**電子郵件地址**，**名字**，和**姓氏**的想成 hello tooprovision 的有效 AAD 帳戶相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c3e37-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="c3e37-229">b.</span><span class="sxs-lookup"><span data-stu-id="c3e37-229">b.</span></span> <span data-ttu-id="c3e37-230">按一下 [建立使用者] 。</span><span class="sxs-lookup"><span data-stu-id="c3e37-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="c3e37-231">hello Azure Active Directory 帳戶持有者會收到電子郵件，其中包含連結 tooconfirm hello 帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="c3e37-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c3e37-232">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="c3e37-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c3e37-233">在本節中，您可以授與存取 tooAdobe 登啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c3e37-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![指派使用者][200] 

<span data-ttu-id="c3e37-235">**tooassign 許 Simon tooAdobe 符號，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c3e37-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="c3e37-236">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c3e37-238">在 [hello] 應用程式清單中，選取**Adobe 登**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="c3e37-240">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c3e37-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c3e37-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c3e37-242">Click **Add** button.</span></span> <span data-ttu-id="c3e37-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c3e37-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c3e37-245">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="c3e37-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c3e37-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c3e37-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3e37-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c3e37-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3e37-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c3e37-248">Testing single sign-on</span></span>

<span data-ttu-id="c3e37-249">當您按一下的 hello Adobe 登磚 hello 存取面板中時，您應該取得自動登入 tooyour Adobe 簽署應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3e37-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="c3e37-250">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="c3e37-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c3e37-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="c3e37-251">Additional resources</span></span>

* [<span data-ttu-id="c3e37-252">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3e37-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3e37-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c3e37-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

