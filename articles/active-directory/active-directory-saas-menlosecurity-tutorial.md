---
title: "教學課程：Azure Active Directory 與 Menlo Security 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Menlo 安全性之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="d00d4-103">教學課程：Azure Active Directory 與 Menlo Security 整合</span><span class="sxs-lookup"><span data-stu-id="d00d4-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="d00d4-104">在此教學課程中，您學會如何 toointegrate Menlo 安全性與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d00d4-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d00d4-105">使用 Azure AD 整合 Menlo 安全性可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="d00d4-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d00d4-106">您可以在 Azure AD 中擁有存取 tooMenlo 安全性控制</span><span class="sxs-lookup"><span data-stu-id="d00d4-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="d00d4-107">您可以啟用您的使用者 tooautomatically get 登入 tooMenlo （單一登入） 的安全性與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="d00d4-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d00d4-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d00d4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d00d4-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。</span><span class="sxs-lookup"><span data-stu-id="d00d4-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="d00d4-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d00d4-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d00d4-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="d00d4-111">Prerequisites</span></span>

<span data-ttu-id="d00d4-112">tooconfigure Menlo 安全性與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d00d4-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="d00d4-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d00d4-113">An Azure AD subscription</span></span>
- <span data-ttu-id="d00d4-114">已啟用 Menlo Security 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d00d4-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d00d4-115">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="d00d4-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d00d4-116">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d00d4-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d00d4-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d00d4-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d00d4-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d00d4-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d00d4-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="d00d4-119">Scenario description</span></span>
<span data-ttu-id="d00d4-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d00d4-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d00d4-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d00d4-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d00d4-122">從 hello 組件庫中加入 Menlo 安全性</span><span class="sxs-lookup"><span data-stu-id="d00d4-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="d00d4-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d00d4-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="d00d4-124">從 hello 組件庫中加入 Menlo 安全性</span><span class="sxs-lookup"><span data-stu-id="d00d4-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="d00d4-125">tooconfigure hello Menlo 安全性整合至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Menlo 安全性。</span><span class="sxs-lookup"><span data-stu-id="d00d4-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d00d4-126">**tooadd Menlo 安全性從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d00d4-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d00d4-127">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d00d4-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d00d4-129">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d00d4-130">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-130">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d00d4-132">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d00d4-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d00d4-134">在 [hello] 搜尋方塊中，輸入**Menlo 安全性**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-134">In hello search box, type **Menlo Security**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="d00d4-136">在 hello 結果 窗格中，選取  **Menlo 安全性**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d00d4-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d00d4-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d00d4-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d00d4-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Menlo Security 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d00d4-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d00d4-140">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Menlo 安全性是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="d00d4-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="d00d4-141">換句話說，Azure AD 使用者與 hello Menlo 安全性相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="d00d4-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="d00d4-142">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Menlo 安全性。</span><span class="sxs-lookup"><span data-stu-id="d00d4-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="d00d4-143">tooconfigure 和測試 Azure AD 單一登入具有 Menlo 安全性，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="d00d4-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d00d4-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="d00d4-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d00d4-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="d00d4-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d00d4-146">**[建立測試使用者 Menlo 安全性](#creating-a-menlo-security-test-user)** -toohave 許 Simon Menlo 安全性連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="d00d4-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d00d4-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d00d4-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d00d4-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="d00d4-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d00d4-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d00d4-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d00d4-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Menlo 安全性應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d00d4-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="d00d4-151">**tooconfigure Azure AD 單一登入具有 Menlo 安全性，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d00d4-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="d00d4-152">在 Azure 入口網站上 hello hello **Menlo 安全性**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d00d4-154">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d00d4-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="d00d4-156">在 hello **Menlo 安全性網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d00d4-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="d00d4-158">a.</span><span class="sxs-lookup"><span data-stu-id="d00d4-158">a.</span></span> <span data-ttu-id="d00d4-159">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="d00d4-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="d00d4-160">b.</span><span class="sxs-lookup"><span data-stu-id="d00d4-160">b.</span></span> <span data-ttu-id="d00d4-161">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="d00d4-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d00d4-162">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="d00d4-162">These values are not hello real.</span></span> <span data-ttu-id="d00d4-163">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="d00d4-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d00d4-164">請連絡[Menlo 安全性用戶端支援小組](https://www.menlosecurity.com/menlo-contact)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="d00d4-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="d00d4-165">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="d00d4-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="d00d4-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d00d4-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d00d4-169">在 hello **Menlo 安全性組態**區段中，按一下**設定 Menlo 安全性**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="d00d4-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d00d4-170">複製 hello **SAML 實體識別碼**，和**SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="d00d4-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="d00d4-172">tooconfigure 單一登入上**Menlo 安全性**，登入 toohello **Menlo 安全性**身為系統管理員的網站。</span><span class="sxs-lookup"><span data-stu-id="d00d4-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="d00d4-173">在下**設定**太移**驗證**並執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d00d4-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="d00d4-175">a.</span><span class="sxs-lookup"><span data-stu-id="d00d4-175">a.</span></span> <span data-ttu-id="d00d4-176">刻度 hello 核取方塊**使用 SAML 啟用使用者驗證**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="d00d4-177">b.</span><span class="sxs-lookup"><span data-stu-id="d00d4-177">b.</span></span> <span data-ttu-id="d00d4-178">選取**允許外部存取**太**是**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="d00d4-179">c.</span><span class="sxs-lookup"><span data-stu-id="d00d4-179">c.</span></span> <span data-ttu-id="d00d4-180">在 [SAML 提供者] 下選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="d00d4-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="d00d4-181">d.</span><span class="sxs-lookup"><span data-stu-id="d00d4-181">d.</span></span> <span data-ttu-id="d00d4-182">**SAML 2.0 端點**： 貼上 hello **SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="d00d4-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d00d4-183">e.</span><span class="sxs-lookup"><span data-stu-id="d00d4-183">e.</span></span> <span data-ttu-id="d00d4-184">**服務識別元 （簽發者）** ： 貼上 hello **SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="d00d4-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d00d4-185">f.</span><span class="sxs-lookup"><span data-stu-id="d00d4-185">f.</span></span> <span data-ttu-id="d00d4-186">**X.509 憑證**： 開啟 hello**憑證 (Base64)**從 [記事本] 中的 hello Azure 入口網站下載，並將它貼入此方塊中。</span><span class="sxs-lookup"><span data-stu-id="d00d4-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="d00d4-187">g.</span><span class="sxs-lookup"><span data-stu-id="d00d4-187">g.</span></span> <span data-ttu-id="d00d4-188">按一下**儲存**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="d00d4-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="d00d4-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="d00d4-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d00d4-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="d00d4-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d00d4-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d00d4-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d00d4-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d00d4-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="d00d4-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d00d4-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d00d4-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d00d4-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d00d4-196">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d00d4-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d00d4-198">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d00d4-200">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="d00d4-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d00d4-202">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d00d4-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d00d4-204">a.</span><span class="sxs-lookup"><span data-stu-id="d00d4-204">a.</span></span> <span data-ttu-id="d00d4-205">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d00d4-206">b.</span><span class="sxs-lookup"><span data-stu-id="d00d4-206">b.</span></span> <span data-ttu-id="d00d4-207">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="d00d4-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d00d4-208">c.</span><span class="sxs-lookup"><span data-stu-id="d00d4-208">c.</span></span> <span data-ttu-id="d00d4-209">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d00d4-210">d.</span><span class="sxs-lookup"><span data-stu-id="d00d4-210">d.</span></span> <span data-ttu-id="d00d4-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d00d4-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="d00d4-212">建立 Menlo Security 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d00d4-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="d00d4-213">在本節中，您要在 Menlo Security 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="d00d4-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="d00d4-214">使用[Menlo 安全性用戶端支援小組](https://www.menlosecurity.com/menlo-contact)tooadd hello hello Menlo 安全性平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="d00d4-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="d00d4-215">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d00d4-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d00d4-216">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="d00d4-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d00d4-217">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooMenlo 安全性。</span><span class="sxs-lookup"><span data-stu-id="d00d4-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![指派使用者][200] 

<span data-ttu-id="d00d4-219">**tooassign 許 Simon tooMenlo 安全性，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d00d4-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="d00d4-220">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d00d4-222">在 [hello] 應用程式清單中，選取**Menlo 安全性**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-222">In hello applications list, select **Menlo Security**.</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="d00d4-224">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="d00d4-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d00d4-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d00d4-226">Click **Add** button.</span></span> <span data-ttu-id="d00d4-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d00d4-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d00d4-229">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="d00d4-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d00d4-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d00d4-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d00d4-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d00d4-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d00d4-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d00d4-232">Testing single sign-on</span></span>

<span data-ttu-id="d00d4-233">在本節中，您會測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="d00d4-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="d00d4-234">開啟瀏覽器視窗中 「 InPrivate"或"Incognito 」 模式 tootrigger 新的驗證。</span><span class="sxs-lookup"><span data-stu-id="d00d4-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="d00d4-235">在 Internet Explorer 中，使用 Ctrl+Shift+P。</span><span class="sxs-lookup"><span data-stu-id="d00d4-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="d00d4-236">在 Chrome 中，使用 Ctrl+Shift+N。</span><span class="sxs-lookup"><span data-stu-id="d00d4-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="d00d4-237">在 hello 私用瀏覽視窗中，瀏覽 tooa 受保護的資源並執行 Azure AD 登入。</span><span class="sxs-lookup"><span data-stu-id="d00d4-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="d00d4-238">成功登入，系統會採用的 toohello 要求站台隔離工作階段中。</span><span class="sxs-lookup"><span data-stu-id="d00d4-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d00d4-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="d00d4-239">Additional resources</span></span>

* [<span data-ttu-id="d00d4-240">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d00d4-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d00d4-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d00d4-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

