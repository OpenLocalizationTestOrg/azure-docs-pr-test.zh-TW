---
title: "教學課程：Azure Active Directory 與 Rightscale 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Rightscale 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 53b927804a1e0f895778a164386459a4ea816f98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="dcd6e-103">教學課程：Azure Active Directory 與 Rightscale 整合</span><span class="sxs-lookup"><span data-stu-id="dcd6e-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="dcd6e-104">在此教學課程中，您學會如何 toointegrate Rightscale 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-104">In this tutorial, you learn how toointegrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dcd6e-105">與 Azure AD 整合 Rightscale 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="dcd6e-105">Integrating Rightscale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dcd6e-106">您可以控制存取 tooRightscale Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="dcd6e-106">You can control in Azure AD who has access tooRightscale</span></span>
- <span data-ttu-id="dcd6e-107">您可以啟用您的使用者 tooautomatically get 登入 tooRightscale （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="dcd6e-107">You can enable your users tooautomatically get signed-on tooRightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dcd6e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dcd6e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dcd6e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcd6e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="dcd6e-110">Prerequisites</span></span>

<span data-ttu-id="dcd6e-111">tooconfigure Rightscale 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="dcd6e-111">tooconfigure Azure AD integration with Rightscale, you need hello following items:</span></span>

- <span data-ttu-id="dcd6e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dcd6e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dcd6e-113">啟用 RightScale 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dcd6e-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dcd6e-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dcd6e-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="dcd6e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dcd6e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dcd6e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dcd6e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="dcd6e-118">Scenario description</span></span>
<span data-ttu-id="dcd6e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dcd6e-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="dcd6e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dcd6e-121">從 hello 圖庫加入 Rightscale</span><span class="sxs-lookup"><span data-stu-id="dcd6e-121">Adding Rightscale from hello gallery</span></span>
2. <span data-ttu-id="dcd6e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dcd6e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-hello-gallery"></a><span data-ttu-id="dcd6e-123">從 hello 圖庫加入 Rightscale</span><span class="sxs-lookup"><span data-stu-id="dcd6e-123">Adding Rightscale from hello gallery</span></span>
<span data-ttu-id="dcd6e-124">tooconfigure hello 整合 Rightscale 到 Azure AD，您需要 tooadd Rightscale hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-124">tooconfigure hello integration of Rightscale into Azure AD, you need tooadd Rightscale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dcd6e-125">**tooadd Rightscale 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dcd6e-125">**tooadd Rightscale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcd6e-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dcd6e-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dcd6e-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="dcd6e-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="dcd6e-133">在 [hello] 搜尋方塊中，輸入**Rightscale**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-133">In hello search box, type **Rightscale**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="dcd6e-135">在 hello 結果 窗格中，選取  **Rightscale**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-135">In hello results panel, select **Rightscale**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dcd6e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dcd6e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dcd6e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Rightscale 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dcd6e-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Rightscale 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Rightscale is tooa user in Azure AD.</span></span> <span data-ttu-id="dcd6e-140">換句話說，Azure AD 使用者與 hello Rightscale 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-140">In other words, a link relationship between an Azure AD user and hello related user in Rightscale needs toobe established.</span></span>

<span data-ttu-id="dcd6e-141">Rightscale 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-141">In Rightscale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dcd6e-142">tooconfigure 及 Rightscale 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="dcd6e-142">tooconfigure and test Azure AD single sign-on with Rightscale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dcd6e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dcd6e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dcd6e-145">**[建立測試使用者 Rightscale](#creating-a-rightscale-test-user)**  -toohave 許 Simon Rightscale 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - toohave a counterpart of Britta Simon in Rightscale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dcd6e-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dcd6e-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dcd6e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dcd6e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dcd6e-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Rightscale 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="dcd6e-150">**tooconfigure Azure AD 單一登入與 Rightscale，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dcd6e-150">**tooconfigure Azure AD single sign-on with Rightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcd6e-151">在 Azure 入口網站上 hello hello **Rightscale**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-151">In hello Azure portal, on hello **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="dcd6e-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="dcd6e-155">在 hello **Rightscale 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP 初始化模式**您不需要 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-155">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **IDP initiated mode** you do not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="dcd6e-157">在 hello **Rightscale 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**SP 初始模式**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dcd6e-157">On hello **Rightscale Domain and URLs** section, if you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="dcd6e-159">a.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-159">a.</span></span> <span data-ttu-id="dcd6e-160">按一下 hello**顯示進階的 URL 設定**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-160">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="dcd6e-161">b.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-161">b.</span></span> <span data-ttu-id="dcd6e-162">在 hello**登入 URL**文字方塊中，型別 hello URL:`https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="dcd6e-162">In hello **Sign On URL** textbox, type hello URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="dcd6e-163">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-163">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="dcd6e-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-165">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="dcd6e-167">在 hello **Rightscale 組態**區段中，按一下**設定 Rightscale** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-167">On hello **Rightscale Configuration** section, click **Configure Rightscale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dcd6e-168">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="dcd6e-168">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="dcd6e-169">![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="dcd6e-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="dcd6e-170">tooget SSO 設定應用程式，您需要 toosign 上 tooyour RightScale 租用戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-170">tooget SSO configured for your application, you need toosign-on tooyour RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="dcd6e-171">a.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-171">a.</span></span> <span data-ttu-id="dcd6e-172">在 hello 最上層顯示 hello 功能表上，按一下 hello**設定**索引標籤並選取**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="dcd6e-174">b.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-174">b.</span></span> <span data-ttu-id="dcd6e-175">按一下 hello"**新**」 按鈕 tooadd**您的 SAML 身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-175">Click hello "**new**" button tooadd **Your SAML Identity Providers**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="dcd6e-177">c.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-177">c.</span></span> <span data-ttu-id="dcd6e-178">中的 hello 文字方塊**顯示名稱**，輸入您的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-178">In hello textbox of **Display Name**, input your company name.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="dcd6e-180">d.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-180">d.</span></span> <span data-ttu-id="dcd6e-181">選取**允許 RightScale 初始化的 SSO 使用探索提示**並輸入您**網域名稱**hello 下方的文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in hello below textbox.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="dcd6e-183">e.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-183">e.</span></span> <span data-ttu-id="dcd6e-184">貼上的 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站將複製其中**SAML SSO 端點**RightScale 中。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-184">Paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="dcd6e-186">f.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-186">f.</span></span> <span data-ttu-id="dcd6e-187">貼上的 hello 值**SAML 實體識別碼**您從 Azure 入口網站將複製其中**SAML EntityID** RightScale 中。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-187">Paste hello value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="dcd6e-189">g.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-189">g.</span></span> <span data-ttu-id="dcd6e-190">按一下**瀏覽器**按鈕 tooupload hello 憑證，您從 Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-190">Click **Browser** button tooupload hello certificate which you downloaded from Azure portal.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="dcd6e-192">h.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-192">h.</span></span> <span data-ttu-id="dcd6e-193">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="dcd6e-194">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="dcd6e-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dcd6e-195">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dcd6e-196">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dcd6e-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dcd6e-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dcd6e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="dcd6e-198">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="dcd6e-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dcd6e-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcd6e-201">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dcd6e-203">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dcd6e-205">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dcd6e-207">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dcd6e-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dcd6e-209">a.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-209">a.</span></span> <span data-ttu-id="dcd6e-210">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dcd6e-211">b.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-211">b.</span></span> <span data-ttu-id="dcd6e-212">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dcd6e-213">c.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-213">c.</span></span> <span data-ttu-id="dcd6e-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dcd6e-215">d.</span><span class="sxs-lookup"><span data-stu-id="dcd6e-215">d.</span></span> <span data-ttu-id="dcd6e-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="dcd6e-217">建立 Rightscale 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dcd6e-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="dcd6e-218">在本節中，您會在 RightScale 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="dcd6e-219">使用[Rightscale 用戶端支援小組](mailto:support@rightscale.com)tooadd hello hello RightScale 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) tooadd hello users in hello RightScale platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dcd6e-220">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="dcd6e-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dcd6e-221">在本節中，您可以授與存取 tooRightscale 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRightscale.</span></span>

![指派使用者][200] 

<span data-ttu-id="dcd6e-223">**tooassign 許 Simon tooRightscale，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dcd6e-223">**tooassign Britta Simon tooRightscale, perform hello following steps:**</span></span>

1. <span data-ttu-id="dcd6e-224">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="dcd6e-226">在 [hello] 應用程式清單中，選取**Rightscale**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-226">In hello applications list, select **Rightscale**.</span></span>

    ![設定單一登入](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="dcd6e-228">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="dcd6e-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-230">Click **Add** button.</span></span> <span data-ttu-id="dcd6e-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="dcd6e-233">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dcd6e-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dcd6e-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dcd6e-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="dcd6e-236">Testing single sign-on</span></span>

<span data-ttu-id="dcd6e-237">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-237">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="dcd6e-238">當您按一下 hello RightScale 磚 hello 存取面板中的時，您應該取得自動登入 tooyour RightScale 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dcd6e-238">When you click hello RightScale tile in hello Access Panel, you should get automatically signed-on tooyour RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dcd6e-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="dcd6e-239">Additional resources</span></span>

* [<span data-ttu-id="dcd6e-240">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcd6e-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dcd6e-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="dcd6e-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

