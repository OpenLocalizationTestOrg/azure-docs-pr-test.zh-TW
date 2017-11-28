---
title: "教學課程：Azure Active Directory 與 EverBridge 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 EverBridge 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="5c709-103">教學課程：Azure Active Directory 與 EverBridge 整合</span><span class="sxs-lookup"><span data-stu-id="5c709-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="5c709-104">在此教學課程中，您學會如何 toointegrate EverBridge 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5c709-104">In this tutorial, you learn how toointegrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c709-105">與 Azure AD 整合 EverBridge 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="5c709-105">Integrating EverBridge with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5c709-106">您可以控制存取 tooEverBridge Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="5c709-106">You can control in Azure AD who has access tooEverBridge</span></span>
- <span data-ttu-id="5c709-107">您可以啟用您的使用者 tooautomatically get 登入 tooEverBridge （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="5c709-107">You can enable your users tooautomatically get signed-on tooEverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c709-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5c709-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5c709-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5c709-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c709-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c709-110">Prerequisites</span></span>

<span data-ttu-id="5c709-111">tooconfigure EverBridge 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="5c709-111">tooconfigure Azure AD integration with EverBridge, you need hello following items:</span></span>

- <span data-ttu-id="5c709-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5c709-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c709-113">已啟用 EverBridge 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5c709-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c709-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="5c709-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c709-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5c709-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c709-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5c709-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c709-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5c709-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c709-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5c709-118">Scenario description</span></span>
<span data-ttu-id="5c709-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c709-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c709-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5c709-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c709-121">從 hello 圖庫加入 EverBridge</span><span class="sxs-lookup"><span data-stu-id="5c709-121">Adding EverBridge from hello gallery</span></span>
2. <span data-ttu-id="5c709-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5c709-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-hello-gallery"></a><span data-ttu-id="5c709-123">從 hello 圖庫加入 EverBridge</span><span class="sxs-lookup"><span data-stu-id="5c709-123">Adding EverBridge from hello gallery</span></span>
<span data-ttu-id="5c709-124">tooconfigure hello 整合 EverBridge 到 Azure AD，您需要 tooadd EverBridge hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c709-124">tooconfigure hello integration of EverBridge into Azure AD, you need tooadd EverBridge from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5c709-125">**tooadd EverBridge 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5c709-125">**tooadd EverBridge from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c709-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="5c709-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c709-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5c709-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5c709-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5c709-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5c709-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c709-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5c709-133">在 [hello] 搜尋方塊中，輸入**EverBridge**。</span><span class="sxs-lookup"><span data-stu-id="5c709-133">In hello search box, type **EverBridge**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="5c709-135">在 hello 結果 窗格中，選取  **EverBridge**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c709-135">In hello results panel, select **EverBridge**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c709-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5c709-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c709-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 EverBridge 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c709-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5c709-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 EverBridge 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="5c709-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EverBridge is tooa user in Azure AD.</span></span> <span data-ttu-id="5c709-140">換句話說，Azure AD 使用者與 hello EverBridge 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="5c709-140">In other words, a link relationship between an Azure AD user and hello related user in EverBridge needs toobe established.</span></span>

<span data-ttu-id="5c709-141">EverBridge 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5c709-141">In EverBridge, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5c709-142">tooconfigure 及 EverBridge 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="5c709-142">tooconfigure and test Azure AD single sign-on with EverBridge, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5c709-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="5c709-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5c709-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="5c709-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c709-145">**[建立測試使用者 EverBridge](#creating-an-everbridge-test-user)**  -toohave 許 Simon EverBridge 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="5c709-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - toohave a counterpart of Britta Simon in EverBridge that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c709-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c709-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c709-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="5c709-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c709-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5c709-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c709-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 EverBridge 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c709-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="5c709-150">**tooconfigure Azure AD 單一登入與 EverBridge，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5c709-150">**tooconfigure Azure AD single sign-on with EverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c709-151">在 Azure 入口網站上 hello hello **EverBridge**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="5c709-151">In hello Azure portal, on hello **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5c709-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c709-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="5c709-155">在 hello **EverBridge 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5c709-155">On hello **EverBridge Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="5c709-157">a.</span><span class="sxs-lookup"><span data-stu-id="5c709-157">a.</span></span> <span data-ttu-id="5c709-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="5c709-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="5c709-159">b.</span><span class="sxs-lookup"><span data-stu-id="5c709-159">b.</span></span> <span data-ttu-id="5c709-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="5c709-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c709-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="5c709-161">These values are not real.</span></span> <span data-ttu-id="5c709-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="5c709-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="5c709-163">請連絡[EverBridge 支援小組](mailto:support@everbridge.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="5c709-163">Contact [EverBridge support team](mailto:support@everbridge.com) tooget these values.</span></span>
 
4. <span data-ttu-id="5c709-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="5c709-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="5c709-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c709-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c709-168">在 hello **EverBridge 組態**區段中，按一下**設定 EverBridge** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="5c709-168">On hello **EverBridge Configuration** section, click **Configure EverBridge** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5c709-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="5c709-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="5c709-171">tooget SSO 設定應用程式，您需要 toosign 上 tooyour Everbridge 租用戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="5c709-171">tooget SSO configured for your application, you need toosign-on tooyour Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="5c709-172">在 hello 最上層顯示 hello 功能表上，按一下 hello**設定**索引標籤並選取**單一登入**下**安全性**。</span><span class="sxs-lookup"><span data-stu-id="5c709-172">In hello menu on hello top, click hello **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="5c709-174">a.</span><span class="sxs-lookup"><span data-stu-id="5c709-174">a.</span></span> <span data-ttu-id="5c709-175">在 hello**名稱**文字方塊中，識別提供者類型 hello 名稱 (例如： 您的公司名稱)。</span><span class="sxs-lookup"><span data-stu-id="5c709-175">In hello **Name** textbox, type hello name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="5c709-176">b.</span><span class="sxs-lookup"><span data-stu-id="5c709-176">b.</span></span> <span data-ttu-id="5c709-177">在 hello **API 名稱**文字方塊中，應用程式開發介面的型別 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="5c709-177">In hello **API Name** textbox, type hello name of API.</span></span>
   
    <span data-ttu-id="5c709-178">c.</span><span class="sxs-lookup"><span data-stu-id="5c709-178">c.</span></span> <span data-ttu-id="5c709-179">按一下**選擇檔案**按鈕 tooupload hello 中繼資料檔從 Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="5c709-179">Click **Choose File** button tooupload hello metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="5c709-180">d.</span><span class="sxs-lookup"><span data-stu-id="5c709-180">d.</span></span> <span data-ttu-id="5c709-181">在 hello SAML 識別位置，選取  **hello 的 hello Subject 陳述式的 NameIdentifier 元素中的識別是**。</span><span class="sxs-lookup"><span data-stu-id="5c709-181">In hello SAML Identity Location, select **Identity is in hello NameIdentifier element of hello Subject statement**.</span></span>
   
    <span data-ttu-id="5c709-182">e.</span><span class="sxs-lookup"><span data-stu-id="5c709-182">e.</span></span> <span data-ttu-id="5c709-183">在 hello**身分識別提供者登入 URL**文字方塊中，貼上來自 Azure AD SAML SSO URL hello 值。</span><span class="sxs-lookup"><span data-stu-id="5c709-183">In hello **Identity Provider Login URL** textbox, paste hello value of SAML SSO URL from Azure AD.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="5c709-185">f.</span><span class="sxs-lookup"><span data-stu-id="5c709-185">f.</span></span> <span data-ttu-id="5c709-186">在 服務提供者起始的要求繫結的 hello，選取**HTTP 重新導向**。</span><span class="sxs-lookup"><span data-stu-id="5c709-186">In hello Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="5c709-187">g.</span><span class="sxs-lookup"><span data-stu-id="5c709-187">g.</span></span> <span data-ttu-id="5c709-188">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="5c709-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="5c709-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="5c709-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5c709-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="5c709-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5c709-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c709-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c709-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5c709-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c709-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5c709-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5c709-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5c709-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c709-196">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="5c709-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c709-198">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="5c709-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c709-200">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="5c709-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c709-202">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5c709-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c709-204">a.</span><span class="sxs-lookup"><span data-stu-id="5c709-204">a.</span></span> <span data-ttu-id="5c709-205">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5c709-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c709-206">b.</span><span class="sxs-lookup"><span data-stu-id="5c709-206">b.</span></span> <span data-ttu-id="5c709-207">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="5c709-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c709-208">c.</span><span class="sxs-lookup"><span data-stu-id="5c709-208">c.</span></span> <span data-ttu-id="5c709-209">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="5c709-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5c709-210">d.</span><span class="sxs-lookup"><span data-stu-id="5c709-210">d.</span></span> <span data-ttu-id="5c709-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5c709-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="5c709-212">建立 EverBridge 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5c709-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="5c709-213">在本節中，您會在 Everbridge 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5c709-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="5c709-214">使用[EverBridge 支援小組](mailto:support@everbridge.com)tooadd hello hello Everbridge 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="5c709-214">Work with [EverBridge support team](mailto:support@everbridge.com) tooadd hello users in hello Everbridge platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5c709-215">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="5c709-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5c709-216">在本節中，您可以授與存取 tooEverBridge 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c709-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEverBridge.</span></span>

![指派使用者][200] 

<span data-ttu-id="5c709-218">**tooassign 許 Simon tooEverBridge，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5c709-218">**tooassign Britta Simon tooEverBridge, perform hello following steps:**</span></span>

1. <span data-ttu-id="5c709-219">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5c709-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5c709-221">在 [hello] 應用程式清單中，選取**EverBridge**。</span><span class="sxs-lookup"><span data-stu-id="5c709-221">In hello applications list, select **EverBridge**.</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="5c709-223">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="5c709-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5c709-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c709-225">Click **Add** button.</span></span> <span data-ttu-id="5c709-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5c709-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5c709-228">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="5c709-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5c709-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c709-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c709-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c709-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c709-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5c709-231">Testing single sign-on</span></span>

<span data-ttu-id="5c709-232">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="5c709-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5c709-233">當您按一下 hello Everbridge 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Everbridge 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c709-233">When you click hello Everbridge tile in hello Access Panel, you should get automatically signed-on tooyour Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c709-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="5c709-234">Additional resources</span></span>

* [<span data-ttu-id="5c709-235">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c709-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c709-236">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5c709-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

