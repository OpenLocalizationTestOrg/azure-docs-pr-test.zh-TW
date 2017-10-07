---
title: "教學課程：Azure Active Directory 與 LockPath Keylight 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 LockPath Keylight 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="189ea-103">教學課程：Azure Active Directory 與 LockPath Keylight 整合</span><span class="sxs-lookup"><span data-stu-id="189ea-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="189ea-104">在此教學課程中，您學會如何 toointegrate LockPath Keylight 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="189ea-104">In this tutorial, you learn how toointegrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="189ea-105">與 Azure AD 整合 LockPath Keylight 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="189ea-105">Integrating LockPath Keylight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="189ea-106">您可以控制存取 tooLockPath Keylight Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="189ea-106">You can control in Azure AD who has access tooLockPath Keylight</span></span>
- <span data-ttu-id="189ea-107">您可以啟用您的使用者 tooautomatically get 登入 tooLockPath Keylight （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="189ea-107">You can enable your users tooautomatically get signed-on tooLockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="189ea-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="189ea-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="189ea-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="189ea-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="189ea-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="189ea-110">Prerequisites</span></span>

<span data-ttu-id="189ea-111">tooconfigure LockPath Keylight 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="189ea-111">tooconfigure Azure AD integration with LockPath Keylight, you need hello following items:</span></span>

- <span data-ttu-id="189ea-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="189ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="189ea-113">啟用 LockPath Keylight 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="189ea-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="189ea-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="189ea-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="189ea-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="189ea-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="189ea-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="189ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="189ea-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="189ea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="189ea-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="189ea-118">Scenario description</span></span>
<span data-ttu-id="189ea-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="189ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="189ea-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="189ea-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="189ea-121">從 hello 圖庫加入 LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="189ea-121">Adding LockPath Keylight from hello gallery</span></span>
2. <span data-ttu-id="189ea-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="189ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-hello-gallery"></a><span data-ttu-id="189ea-123">從 hello 圖庫加入 LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="189ea-123">Adding LockPath Keylight from hello gallery</span></span>
<span data-ttu-id="189ea-124">tooconfigure hello 整合 LockPath Keylight 到 Azure AD，您需要 tooadd LockPath Keylight hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="189ea-124">tooconfigure hello integration of LockPath Keylight into Azure AD, you need tooadd LockPath Keylight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="189ea-125">**tooadd LockPath Keylight 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="189ea-125">**tooadd LockPath Keylight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="189ea-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="189ea-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="189ea-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="189ea-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="189ea-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="189ea-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="189ea-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="189ea-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="189ea-133">在 [hello] 搜尋方塊中，輸入**LockPath Keylight**。</span><span class="sxs-lookup"><span data-stu-id="189ea-133">In hello search box, type **LockPath Keylight**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="189ea-135">在 hello 結果 窗格中，選取  **LockPath Keylight**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="189ea-135">In hello results panel, select **LockPath Keylight**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="189ea-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="189ea-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="189ea-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 LockPath Keylight 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="189ea-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="189ea-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 LockPath Keylight 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="189ea-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LockPath Keylight is tooa user in Azure AD.</span></span> <span data-ttu-id="189ea-140">換句話說，Azure AD 使用者與 hello LockPath Keylight 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="189ea-140">In other words, a link relationship between an Azure AD user and hello related user in LockPath Keylight needs toobe established.</span></span>

<span data-ttu-id="189ea-141">LockPath Keylight 中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="189ea-141">In LockPath Keylight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="189ea-142">tooconfigure 及 LockPath Keylight 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="189ea-142">tooconfigure and test Azure AD single sign-on with LockPath Keylight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="189ea-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="189ea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="189ea-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="189ea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="189ea-145">**[建立測試使用者 LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave 許 Simon LockPath Keylight 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="189ea-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - toohave a counterpart of Britta Simon in LockPath Keylight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="189ea-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="189ea-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="189ea-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="189ea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="189ea-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="189ea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="189ea-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 LockPath Keylight 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="189ea-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="189ea-150">**tooconfigure Azure AD 單一登入與 LockPath Keylight，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="189ea-150">**tooconfigure Azure AD single sign-on with LockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="189ea-151">在 Azure 入口網站上 hello hello **LockPath Keylight**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="189ea-151">In hello Azure portal, on hello **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="189ea-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="189ea-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="189ea-155">在 hello **LockPath Keylight 網域和 Url**區段中，執行下列步驟的 hello::</span><span class="sxs-lookup"><span data-stu-id="189ea-155">On hello **LockPath Keylight Domain and URLs** section, perform hello following steps::</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="189ea-157">a.</span><span class="sxs-lookup"><span data-stu-id="189ea-157">a.</span></span> <span data-ttu-id="189ea-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="189ea-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="189ea-159">b.</span><span class="sxs-lookup"><span data-stu-id="189ea-159">b.</span></span> <span data-ttu-id="189ea-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="189ea-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="189ea-161">c.</span><span class="sxs-lookup"><span data-stu-id="189ea-161">c.</span></span> <span data-ttu-id="189ea-162">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="189ea-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="189ea-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="189ea-163">These values are not real.</span></span> <span data-ttu-id="189ea-164">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="189ea-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="189ea-165">請連絡[LockPath Keylight 用戶端支援小組](https://www.lockpath.com/contact/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="189ea-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) tooget these values.</span></span> 

4. <span data-ttu-id="189ea-166">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Raw)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="189ea-166">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="189ea-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="189ea-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="189ea-170">在 hello **LockPath Keylight 組態**區段中，按一下**設定 LockPath Keylight** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="189ea-170">On hello **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="189ea-171">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="189ea-171">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="189ea-173">tooenable SSO LockPath Keylight 中執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="189ea-173">tooenable SSO in LockPath Keylight, perform hello following steps:</span></span>
   
    <span data-ttu-id="189ea-174">a.</span><span class="sxs-lookup"><span data-stu-id="189ea-174">a.</span></span> <span data-ttu-id="189ea-175">登入 tooyour LockPath Keylight 以系統管理員身分的帳戶。</span><span class="sxs-lookup"><span data-stu-id="189ea-175">Sign-on tooyour LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="189ea-176">b.</span><span class="sxs-lookup"><span data-stu-id="189ea-176">b.</span></span> <span data-ttu-id="189ea-177">在 hello 最上層顯示 hello 功能表上，按一下**人員**，並選取**Keylight 安裝**。</span><span class="sxs-lookup"><span data-stu-id="189ea-177">In hello menu on hello top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="189ea-179">c.</span><span class="sxs-lookup"><span data-stu-id="189ea-179">c.</span></span> <span data-ttu-id="189ea-180">在 hello hello 左側樹狀檢視中按一下**SAML**。</span><span class="sxs-lookup"><span data-stu-id="189ea-180">In hello treeview on hello left, click **SAML**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="189ea-182">d.</span><span class="sxs-lookup"><span data-stu-id="189ea-182">d.</span></span> <span data-ttu-id="189ea-183">在 hello **SAML 設定** 對話方塊中，按一下 **編輯**。</span><span class="sxs-lookup"><span data-stu-id="189ea-183">On hello **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="189ea-185">在 hello**編輯 SAML 設定**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="189ea-185">On hello **Edit SAML Settings** dialog page, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="189ea-187">a.</span><span class="sxs-lookup"><span data-stu-id="189ea-187">a.</span></span> <span data-ttu-id="189ea-188">設定**SAML 驗證**太**Active**。</span><span class="sxs-lookup"><span data-stu-id="189ea-188">Set **SAML authentication** too**Active**.</span></span>

    <span data-ttu-id="189ea-189">b.</span><span class="sxs-lookup"><span data-stu-id="189ea-189">b.</span></span> <span data-ttu-id="189ea-190">貼上 hello **SAML 單一登入服務 URL**值，您從 hello Azure 入口網站複製到 hello**身分識別提供者登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="189ea-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="189ea-191">c.</span><span class="sxs-lookup"><span data-stu-id="189ea-191">c.</span></span> <span data-ttu-id="189ea-192">貼上 hello**單一登出服務 URL**值，您從 hello Azure 入口網站複製到 hello**身分識別提供者登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="189ea-192">Paste hello **Single Sign-Out Service URL** value which you have copied from hello Azure portal into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="189ea-193">d.</span><span class="sxs-lookup"><span data-stu-id="189ea-193">d.</span></span> <span data-ttu-id="189ea-194">按一下**選擇檔案**tooselect 下載的 LockPath Keylight 憑證，然後按一下**開啟**tooupload hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="189ea-194">Click **Choose File** tooselect your downloaded LockPath Keylight certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="189ea-195">e.</span><span class="sxs-lookup"><span data-stu-id="189ea-195">e.</span></span> <span data-ttu-id="189ea-196">設定**SAML 使用者識別碼位置**太**hello subject 陳述式的 NameIdentifier 元素**。</span><span class="sxs-lookup"><span data-stu-id="189ea-196">Set **SAML User Id location** too**NameIdentifier element of hello subject statement**.</span></span>
    
    <span data-ttu-id="189ea-197">f.</span><span class="sxs-lookup"><span data-stu-id="189ea-197">f.</span></span> <span data-ttu-id="189ea-198">提供 hello **Keylight 服務提供者**使用 hello 下列模式： **https://&lt;CompanyName&gt;。 keylightgrc.com**。</span><span class="sxs-lookup"><span data-stu-id="189ea-198">Provide hello **Keylight Service Provider** using hello following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="189ea-199">g.</span><span class="sxs-lookup"><span data-stu-id="189ea-199">g.</span></span> <span data-ttu-id="189ea-200">設定**使用者自動佈建**太**Active**。</span><span class="sxs-lookup"><span data-stu-id="189ea-200">Set **Auto-provision users** too**Active**.</span></span>

    <span data-ttu-id="189ea-201">h.</span><span class="sxs-lookup"><span data-stu-id="189ea-201">h.</span></span> <span data-ttu-id="189ea-202">設定**自動佈建帳戶類型**太**完整使用者**。</span><span class="sxs-lookup"><span data-stu-id="189ea-202">Set **Auto-provision account type** too**Full User**.</span></span>

    <span data-ttu-id="189ea-203">i.</span><span class="sxs-lookup"><span data-stu-id="189ea-203">i.</span></span> <span data-ttu-id="189ea-204">設定 [自動佈建安全性角色]，選取 [具備 SAML 的標準使用者]。</span><span class="sxs-lookup"><span data-stu-id="189ea-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="189ea-205">j.</span><span class="sxs-lookup"><span data-stu-id="189ea-205">j.</span></span> <span data-ttu-id="189ea-206">設定 [自動佈建安全性設定]，選取 [標準使用者設定]。</span><span class="sxs-lookup"><span data-stu-id="189ea-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="189ea-207">k.</span><span class="sxs-lookup"><span data-stu-id="189ea-207">k.</span></span> <span data-ttu-id="189ea-208">在 hello**電子郵件屬性**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="189ea-208">In hello **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="189ea-209">l.</span><span class="sxs-lookup"><span data-stu-id="189ea-209">l.</span></span> <span data-ttu-id="189ea-210">在 hello**名字屬性**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`。</span><span class="sxs-lookup"><span data-stu-id="189ea-210">In hello **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="189ea-211">m.</span><span class="sxs-lookup"><span data-stu-id="189ea-211">m.</span></span> <span data-ttu-id="189ea-212">在 hello**姓氏**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`。</span><span class="sxs-lookup"><span data-stu-id="189ea-212">In hello **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="189ea-213">n.</span><span class="sxs-lookup"><span data-stu-id="189ea-213">n.</span></span> <span data-ttu-id="189ea-214">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="189ea-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="189ea-215">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="189ea-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="189ea-216">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="189ea-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="189ea-217">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="189ea-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="189ea-218">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="189ea-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="189ea-219">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="189ea-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="189ea-221">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="189ea-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="189ea-222">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="189ea-222">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="189ea-224">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="189ea-224">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="189ea-226">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="189ea-226">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="189ea-228">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="189ea-228">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="189ea-230">a.</span><span class="sxs-lookup"><span data-stu-id="189ea-230">a.</span></span> <span data-ttu-id="189ea-231">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="189ea-231">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="189ea-232">b.</span><span class="sxs-lookup"><span data-stu-id="189ea-232">b.</span></span> <span data-ttu-id="189ea-233">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="189ea-233">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="189ea-234">c.</span><span class="sxs-lookup"><span data-stu-id="189ea-234">c.</span></span> <span data-ttu-id="189ea-235">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="189ea-235">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="189ea-236">d.</span><span class="sxs-lookup"><span data-stu-id="189ea-236">d.</span></span> <span data-ttu-id="189ea-237">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="189ea-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="189ea-238">建立 LockPath Keylight 測試使用者</span><span class="sxs-lookup"><span data-stu-id="189ea-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="189ea-239">在本節中，您要在 LockPath Keylight 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="189ea-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="189ea-240">LockPath Keylight 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="189ea-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="189ea-241">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="189ea-241">There is no action item for you in this section.</span></span> <span data-ttu-id="189ea-242">如果還不存在的 hello 使用者存取 LockPath Keylight 時，會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="189ea-242">A new user is created when accessing LockPath Keylight if hello user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="189ea-243">若要手動 toocreate 使用者，您需要 toocontact hello [LockPath Keylight 用戶端支援小組](https://www.lockpath.com/contact/)。</span><span class="sxs-lookup"><span data-stu-id="189ea-243">If you need toocreate a user manually, you need toocontact hello [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="189ea-244">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="189ea-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="189ea-245">在本節中，您可以授與存取 tooLockPath Keylight 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="189ea-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLockPath Keylight.</span></span>

![指派使用者][200] 

<span data-ttu-id="189ea-247">**tooassign 許 Simon tooLockPath Keylight，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="189ea-247">**tooassign Britta Simon tooLockPath Keylight, perform hello following steps:**</span></span>

1. <span data-ttu-id="189ea-248">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="189ea-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="189ea-250">在 [hello] 應用程式清單中，選取**LockPath Keylight**。</span><span class="sxs-lookup"><span data-stu-id="189ea-250">In hello applications list, select **LockPath Keylight**.</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="189ea-252">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="189ea-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="189ea-254">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="189ea-254">Click **Add** button.</span></span> <span data-ttu-id="189ea-255">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="189ea-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="189ea-257">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="189ea-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="189ea-258">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="189ea-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="189ea-259">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="189ea-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="189ea-260">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="189ea-260">Testing single sign-on</span></span>

<span data-ttu-id="189ea-261">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="189ea-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="189ea-262">當您按一下的 hello LockPath Keylight 磚 hello 存取面板中時，您應該取得自動登入 tooyour LockPath Keylight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="189ea-262">When you click hello LockPath Keylight tile in hello Access Panel, you should get automatically signed-on tooyour LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="189ea-263">其他資源</span><span class="sxs-lookup"><span data-stu-id="189ea-263">Additional resources</span></span>

* [<span data-ttu-id="189ea-264">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="189ea-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="189ea-265">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="189ea-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

