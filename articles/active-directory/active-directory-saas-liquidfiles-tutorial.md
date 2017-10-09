---
title: "教學課程：Azure Active Directory 與 LiquidFiles 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 LiquidFiles 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 67eb888090f81e0ceb791ed45d564b98fe1eb6d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="b09de-103">教學課程：Azure Active Directory 與 LiquidFiles 整合</span><span class="sxs-lookup"><span data-stu-id="b09de-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="b09de-104">在此教學課程中，您學會如何 toointegrate LiquidFiles 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b09de-104">In this tutorial, you learn how toointegrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b09de-105">與 Azure AD 整合 LiquidFiles 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b09de-105">Integrating LiquidFiles with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b09de-106">您可以控制存取 tooLiquidFiles Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="b09de-106">You can control in Azure AD who has access tooLiquidFiles</span></span>
- <span data-ttu-id="b09de-107">您可以啟用您的使用者 tooautomatically get 登入 tooLiquidFiles （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="b09de-107">You can enable your users tooautomatically get signed-on tooLiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b09de-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b09de-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b09de-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b09de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b09de-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b09de-110">Prerequisites</span></span>

<span data-ttu-id="b09de-111">tooconfigure LiquidFiles 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b09de-111">tooconfigure Azure AD integration with LiquidFiles, you need hello following items:</span></span>

- <span data-ttu-id="b09de-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b09de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b09de-113">啟用 LiquidFiles 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b09de-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b09de-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b09de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b09de-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b09de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b09de-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b09de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b09de-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b09de-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b09de-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b09de-118">Scenario description</span></span>
<span data-ttu-id="b09de-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b09de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b09de-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b09de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b09de-121">從 hello 圖庫加入 LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="b09de-121">Adding LiquidFiles from hello gallery</span></span>
2. <span data-ttu-id="b09de-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b09de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-hello-gallery"></a><span data-ttu-id="b09de-123">從 hello 圖庫加入 LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="b09de-123">Adding LiquidFiles from hello gallery</span></span>
<span data-ttu-id="b09de-124">tooconfigure hello 整合 LiquidFiles 到 Azure AD，您需要 tooadd LiquidFiles hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b09de-124">tooconfigure hello integration of LiquidFiles into Azure AD, you need tooadd LiquidFiles from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b09de-125">**tooadd LiquidFiles 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b09de-125">**tooadd LiquidFiles from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b09de-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b09de-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b09de-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b09de-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b09de-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b09de-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b09de-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b09de-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b09de-133">在 [hello] 搜尋方塊中，輸入**LiquidFiles**。</span><span class="sxs-lookup"><span data-stu-id="b09de-133">In hello search box, type **LiquidFiles**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="b09de-135">在 hello 結果 窗格中，選取  **LiquidFiles**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b09de-135">In hello results panel, select **LiquidFiles**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b09de-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b09de-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b09de-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 LiquidFiles 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b09de-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b09de-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 LiquidFiles 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b09de-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LiquidFiles is tooa user in Azure AD.</span></span> <span data-ttu-id="b09de-140">換句話說，Azure AD 使用者與 hello LiquidFiles 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b09de-140">In other words, a link relationship between an Azure AD user and hello related user in LiquidFiles needs toobe established.</span></span>

<span data-ttu-id="b09de-141">LiquidFiles 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b09de-141">In LiquidFiles, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b09de-142">tooconfigure 及 LiquidFiles 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b09de-142">tooconfigure and test Azure AD single sign-on with LiquidFiles, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b09de-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b09de-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b09de-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b09de-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b09de-145">**[建立測試使用者 LiquidFiles](#creating-a-liquidfiles-test-user)**  -toohave 許 Simon LiquidFiles 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b09de-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - toohave a counterpart of Britta Simon in LiquidFiles that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b09de-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b09de-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b09de-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b09de-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b09de-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b09de-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b09de-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 LiquidFiles 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b09de-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="b09de-150">**tooconfigure Azure AD 單一登入與 LiquidFiles，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b09de-150">**tooconfigure Azure AD single sign-on with LiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="b09de-151">在 Azure 入口網站上 hello hello **LiquidFiles**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b09de-151">In hello Azure portal, on hello **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b09de-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b09de-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="b09de-155">在 hello **LiquidFiles 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b09de-155">On hello **LiquidFiles Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="b09de-157">a.</span><span class="sxs-lookup"><span data-stu-id="b09de-157">a.</span></span> <span data-ttu-id="b09de-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="b09de-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="b09de-159">b.</span><span class="sxs-lookup"><span data-stu-id="b09de-159">b.</span></span> <span data-ttu-id="b09de-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="b09de-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="b09de-161">c.</span><span class="sxs-lookup"><span data-stu-id="b09de-161">c.</span></span> <span data-ttu-id="b09de-162">b.</span><span class="sxs-lookup"><span data-stu-id="b09de-162">b.</span></span> <span data-ttu-id="b09de-163">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="b09de-163">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b09de-164">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="b09de-164">These values are not real.</span></span> <span data-ttu-id="b09de-165">更新這些值與 hello 實際的登入 URL，識別項和回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="b09de-165">Update these values with hello actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="b09de-166">請連絡[LiquidFiles 用戶端支援小組](https://www.liquidfiles.com/support.html)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="b09de-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="b09de-167">在 hello **SAML 簽章憑證**區段，複製 hello**指紋**憑證值。</span><span class="sxs-lookup"><span data-stu-id="b09de-167">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="b09de-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b09de-169">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b09de-171">在 hello **LiquidFiles 組態**區段中，按一下**設定 LiquidFiles** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="b09de-171">On hello **LiquidFiles Configuration** section, click **Configure LiquidFiles** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b09de-172">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="b09de-172">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="b09de-174">以系統管理員身分登入 tooyour LiquidFiles 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b09de-174">Sign-on tooyour LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="b09de-175">按一下**單一登入**在 hello **Admin > 組態**hello 功能表。</span><span class="sxs-lookup"><span data-stu-id="b09de-175">Click **Single Sign-On** in hello **Admin > Configuration** from hello menu.</span></span>

9. <span data-ttu-id="b09de-176">在 hello**單一登入組態**頁面上，執行下列步驟的 hello</span><span class="sxs-lookup"><span data-stu-id="b09de-176">On hello **Single Sign-On Configuration** page, perform hello following steps</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="b09de-178">a.</span><span class="sxs-lookup"><span data-stu-id="b09de-178">a.</span></span> <span data-ttu-id="b09de-179">在 [單一登入方法] 中，選取 [SAML 2]。</span><span class="sxs-lookup"><span data-stu-id="b09de-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="b09de-180">b.</span><span class="sxs-lookup"><span data-stu-id="b09de-180">b.</span></span> <span data-ttu-id="b09de-181">在 hello **IDP 登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="b09de-181">In hello **IDP Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b09de-182">c.</span><span class="sxs-lookup"><span data-stu-id="b09de-182">c.</span></span> <span data-ttu-id="b09de-183">在 hello **IDP 登出 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="b09de-183">In hello **IDP Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b09de-184">d.</span><span class="sxs-lookup"><span data-stu-id="b09de-184">d.</span></span> <span data-ttu-id="b09de-185">在 hello **IDP 憑證指紋**文字方塊中，貼上 hello**指紋**您從 Azure 入口網站複製的值...</span><span class="sxs-lookup"><span data-stu-id="b09de-185">In hello **IDP Cert Fingerprint** textbox, paste hello **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="b09de-186">e.</span><span class="sxs-lookup"><span data-stu-id="b09de-186">e.</span></span> <span data-ttu-id="b09de-187">在 hello 名稱識別碼格式的文字方塊中，輸入 hello 值**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-: emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="b09de-187">In hello Name Identifier Format textbox, type hello value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="b09de-188">f.</span><span class="sxs-lookup"><span data-stu-id="b09de-188">f.</span></span> <span data-ttu-id="b09de-189">在 hello 驗證內容文字方塊中，輸入 hello 值**urn: oasis： 名稱： tc: SAML:2.0:ac:classes:PasswordProtectedTransport**。</span><span class="sxs-lookup"><span data-stu-id="b09de-189">In hello Authn Context textbox, type hello value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="b09de-190">g.</span><span class="sxs-lookup"><span data-stu-id="b09de-190">g.</span></span> <span data-ttu-id="b09de-191">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b09de-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="b09de-192">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b09de-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b09de-193">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b09de-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b09de-194">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b09de-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b09de-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b09de-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="b09de-196">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b09de-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b09de-198">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b09de-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b09de-199">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b09de-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b09de-201">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b09de-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b09de-203">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="b09de-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b09de-205">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b09de-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b09de-207">a.</span><span class="sxs-lookup"><span data-stu-id="b09de-207">a.</span></span> <span data-ttu-id="b09de-208">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b09de-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b09de-209">b.</span><span class="sxs-lookup"><span data-stu-id="b09de-209">b.</span></span> <span data-ttu-id="b09de-210">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="b09de-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b09de-211">c.</span><span class="sxs-lookup"><span data-stu-id="b09de-211">c.</span></span> <span data-ttu-id="b09de-212">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="b09de-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b09de-213">d.</span><span class="sxs-lookup"><span data-stu-id="b09de-213">d.</span></span> <span data-ttu-id="b09de-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b09de-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="b09de-215">建立 LiquidFiles 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b09de-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="b09de-216">hello 本節目標在於 toocreate LiquidFiles 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b09de-216">hello objective of this section is toocreate a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="b09de-217">使用您 LiquidFiles 伺服器系統管理員 tooget 自行新增的使用者身分登入 tooyour LiquidFiles 應用程式之前。</span><span class="sxs-lookup"><span data-stu-id="b09de-217">Work with your LiquidFiles server administrator tooget yourself added as a user before logging in tooyour LiquidFiles application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b09de-218">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="b09de-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b09de-219">在本節中，您可以授與存取 tooLiquidFiles 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b09de-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLiquidFiles.</span></span>

![指派使用者][200] 

<span data-ttu-id="b09de-221">**tooassign 許 Simon tooLiquidFiles，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b09de-221">**tooassign Britta Simon tooLiquidFiles, perform hello following steps:**</span></span>

1. <span data-ttu-id="b09de-222">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b09de-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b09de-224">在 [hello] 應用程式清單中，選取**LiquidFiles**。</span><span class="sxs-lookup"><span data-stu-id="b09de-224">In hello applications list, select **LiquidFiles**.</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="b09de-226">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b09de-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b09de-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b09de-228">Click **Add** button.</span></span> <span data-ttu-id="b09de-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b09de-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b09de-231">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b09de-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b09de-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b09de-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b09de-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b09de-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b09de-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b09de-234">Testing single sign-on</span></span>

<span data-ttu-id="b09de-235">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b09de-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b09de-236">當您按一下的 hello LiquidFiles 磚 hello 存取面板中時，您應該取得自動登入 tooyour LiquidFiles 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b09de-236">When you click hello LiquidFiles tile in hello Access Panel, you should get automatically signed-on tooyour LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b09de-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="b09de-237">Additional resources</span></span>

* [<span data-ttu-id="b09de-238">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b09de-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b09de-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b09de-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

