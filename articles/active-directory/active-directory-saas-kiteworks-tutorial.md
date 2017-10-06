---
title: "教學課程：將 Azure Active Directory 與 Kiteworks 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Kiteworks 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 406417dd7f58cc3f1fa0d9e86b5cad0c1d7be750
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="bb653-103">教學課程：將 Azure Active Directory 與 Kiteworks 整合</span><span class="sxs-lookup"><span data-stu-id="bb653-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="bb653-104">在此教學課程中，您學會如何 toointegrate Kiteworks 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="bb653-104">In this tutorial, you learn how toointegrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb653-105">與 Azure AD 整合 Kiteworks 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="bb653-105">Integrating Kiteworks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bb653-106">您可以控制存取 tooKiteworks Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="bb653-106">You can control in Azure AD who has access tooKiteworks</span></span>
- <span data-ttu-id="bb653-107">您可以啟用您的使用者 tooautomatically get 登入 tooKiteworks （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="bb653-107">You can enable your users tooautomatically get signed-on tooKiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb653-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bb653-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bb653-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="bb653-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb653-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bb653-110">Prerequisites</span></span>

<span data-ttu-id="bb653-111">tooconfigure Kiteworks 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="bb653-111">tooconfigure Azure AD integration with Kiteworks, you need hello following items:</span></span>

- <span data-ttu-id="bb653-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bb653-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb653-113">已啟用 Kiteworks 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bb653-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb653-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="bb653-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb653-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="bb653-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb653-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="bb653-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb653-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="bb653-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb653-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="bb653-118">Scenario description</span></span>
<span data-ttu-id="bb653-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb653-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb653-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="bb653-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb653-121">從 hello 圖庫加入 Kiteworks</span><span class="sxs-lookup"><span data-stu-id="bb653-121">Adding Kiteworks from hello gallery</span></span>
2. <span data-ttu-id="bb653-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bb653-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-hello-gallery"></a><span data-ttu-id="bb653-123">從 hello 圖庫加入 Kiteworks</span><span class="sxs-lookup"><span data-stu-id="bb653-123">Adding Kiteworks from hello gallery</span></span>
<span data-ttu-id="bb653-124">tooconfigure hello 整合 Kiteworks 到 Azure AD，您需要 tooadd Kiteworks hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb653-124">tooconfigure hello integration of Kiteworks into Azure AD, you need tooadd Kiteworks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bb653-125">**tooadd Kiteworks 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bb653-125">**tooadd Kiteworks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb653-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="bb653-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bb653-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bb653-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bb653-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bb653-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="bb653-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb653-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="bb653-133">在 [hello] 搜尋方塊中，輸入**Kiteworks**。</span><span class="sxs-lookup"><span data-stu-id="bb653-133">In hello search box, type **Kiteworks**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="bb653-135">在 hello 結果 窗格中，選取  **Kiteworks**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb653-135">In hello results panel, select **Kiteworks**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb653-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bb653-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb653-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kiteworks 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb653-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bb653-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Kiteworks 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="bb653-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kiteworks is tooa user in Azure AD.</span></span> <span data-ttu-id="bb653-140">換句話說，Azure AD 使用者與 hello Kiteworks 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="bb653-140">In other words, a link relationship between an Azure AD user and hello related user in Kiteworks needs toobe established.</span></span>

<span data-ttu-id="bb653-141">Kiteworks 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="bb653-141">In Kiteworks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bb653-142">tooconfigure 及 Kiteworks 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="bb653-142">tooconfigure and test Azure AD single sign-on with Kiteworks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bb653-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="bb653-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bb653-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="bb653-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb653-145">**[建立測試使用者 Kiteworks](#creating-a-kiteworks-test-user)**  -toohave 許 Simon Kiteworks 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="bb653-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - toohave a counterpart of Britta Simon in Kiteworks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb653-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb653-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb653-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="bb653-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb653-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bb653-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb653-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Kiteworks 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb653-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="bb653-150">**tooconfigure Azure AD 單一登入與 Kiteworks，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bb653-150">**tooconfigure Azure AD single sign-on with Kiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb653-151">在 Azure 入口網站上 hello hello **Kiteworks**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="bb653-151">In hello Azure portal, on hello **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="bb653-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb653-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="bb653-155">在 hello **Kiteworks 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb653-155">On hello **Kiteworks Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="bb653-157">a.</span><span class="sxs-lookup"><span data-stu-id="bb653-157">a.</span></span> <span data-ttu-id="bb653-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="bb653-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="bb653-159">b.</span><span class="sxs-lookup"><span data-stu-id="bb653-159">b.</span></span> <span data-ttu-id="bb653-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="bb653-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb653-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="bb653-161">These values are not real.</span></span> <span data-ttu-id="bb653-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="bb653-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bb653-163">請連絡[Kiteworks 用戶端支援小組](http://accellion.com/support)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="bb653-163">Contact [Kiteworks Client support team](http://accellion.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="bb653-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="bb653-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="bb653-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb653-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb653-168">在 hello **Kiteworks 組態**區段中，按一下**設定 Kiteworks** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="bb653-168">On hello **Kiteworks Configuration** section, click **Configure Kiteworks** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bb653-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="bb653-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="bb653-171">登入 tooyour Kiteworks 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="bb653-171">Sign on tooyour Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="bb653-172">在 hello hello 上方的工具列中按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="bb653-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="bb653-174">在 hello**驗證和授權**區段中，按一下**SSO 安裝**。</span><span class="sxs-lookup"><span data-stu-id="bb653-174">In hello **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="bb653-176">在 hello SSO 安裝程式 頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb653-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="bb653-178">a.</span><span class="sxs-lookup"><span data-stu-id="bb653-178">a.</span></span> <span data-ttu-id="bb653-179">選取 [透過 SSO 驗證]。</span><span class="sxs-lookup"><span data-stu-id="bb653-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="bb653-180">b.</span><span class="sxs-lookup"><span data-stu-id="bb653-180">b.</span></span> <span data-ttu-id="bb653-181">選取 [起始 AuthnRequest]。</span><span class="sxs-lookup"><span data-stu-id="bb653-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="bb653-182">c.</span><span class="sxs-lookup"><span data-stu-id="bb653-182">c.</span></span> <span data-ttu-id="bb653-183">在 hello **IDP 實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="bb653-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="bb653-184">d.</span><span class="sxs-lookup"><span data-stu-id="bb653-184">d.</span></span> <span data-ttu-id="bb653-185">在 hello**單一登入服務 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="bb653-185">In hello **Single Sign-On Service URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bb653-186">e.</span><span class="sxs-lookup"><span data-stu-id="bb653-186">e.</span></span> <span data-ttu-id="bb653-187">在 hello**單一登出服務 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="bb653-187">In hello **Single Logout Service URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bb653-188">f.</span><span class="sxs-lookup"><span data-stu-id="bb653-188">f.</span></span> <span data-ttu-id="bb653-189">開啟 [記事本]，複製 hello 內容，您所下載的憑證，然後將它貼到 hello **RSA 公開金鑰憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="bb653-189">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="bb653-190">g.</span><span class="sxs-lookup"><span data-stu-id="bb653-190">g.</span></span> <span data-ttu-id="bb653-191">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="bb653-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="bb653-192">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="bb653-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bb653-193">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="bb653-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bb653-194">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb653-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb653-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bb653-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb653-196">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="bb653-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="bb653-198">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bb653-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb653-199">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="bb653-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb653-201">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="bb653-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb653-203">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="bb653-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb653-205">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="bb653-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb653-207">a.</span><span class="sxs-lookup"><span data-stu-id="bb653-207">a.</span></span> <span data-ttu-id="bb653-208">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="bb653-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb653-209">b.</span><span class="sxs-lookup"><span data-stu-id="bb653-209">b.</span></span> <span data-ttu-id="bb653-210">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="bb653-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb653-211">c.</span><span class="sxs-lookup"><span data-stu-id="bb653-211">c.</span></span> <span data-ttu-id="bb653-212">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="bb653-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bb653-213">d.</span><span class="sxs-lookup"><span data-stu-id="bb653-213">d.</span></span> <span data-ttu-id="bb653-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bb653-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="bb653-215">建立 Kiteworks 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bb653-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="bb653-216">hello 本節目標在於 toocreate Kiteworks 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="bb653-216">hello objective of this section is toocreate a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="bb653-217">Kiteworks 支援預設啟用的 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="bb653-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="bb653-218">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="bb653-218">There is no action item for you in this section.</span></span> <span data-ttu-id="bb653-219">如果尚未存在期間嘗試 tooaccess Kitewors，建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="bb653-219">A new user is created during an attempt tooaccess Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="bb653-220">若要手動 toocreate 使用者，您需要 toocontact hello [Kiteworks 支援小組](http://accellion.com/support)。</span><span class="sxs-lookup"><span data-stu-id="bb653-220">If you need toocreate a user manually, you need toocontact hello [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bb653-221">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="bb653-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bb653-222">在本節中，您可以授與存取 tooKiteworks 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bb653-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKiteworks.</span></span>

![指派使用者][200] 

<span data-ttu-id="bb653-224">**tooassign 許 Simon tooKiteworks，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="bb653-224">**tooassign Britta Simon tooKiteworks, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb653-225">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="bb653-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="bb653-227">在 [hello] 應用程式清單中，選取**Kiteworks**。</span><span class="sxs-lookup"><span data-stu-id="bb653-227">In hello applications list, select **Kiteworks**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="bb653-229">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="bb653-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="bb653-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb653-231">Click **Add** button.</span></span> <span data-ttu-id="bb653-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="bb653-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="bb653-234">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="bb653-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bb653-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb653-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb653-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bb653-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb653-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="bb653-237">Testing single sign-on</span></span>

<span data-ttu-id="bb653-238">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="bb653-238">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="bb653-239">當您按一下的 hello Kiteworks 磚 hello 存取面板中時，您應該取得自動登入 tooyour Kiteworks 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bb653-239">When you click hello Kiteworks tile in hello Access Panel, you should get automatically signed-on tooyour Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb653-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="bb653-240">Additional resources</span></span>

* [<span data-ttu-id="bb653-241">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb653-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb653-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="bb653-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

