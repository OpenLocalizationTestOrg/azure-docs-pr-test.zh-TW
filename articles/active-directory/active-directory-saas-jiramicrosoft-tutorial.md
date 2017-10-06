---
title: "教學課程：Azure Active Directory 與 JIRA SAML SSO by Microsoft 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和 microsoft JIRA SAML SSO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="b32b8-103">教學課程：Azure Active Directory 與 JIRA SAML SSO by Microsoft 整合</span><span class="sxs-lookup"><span data-stu-id="b32b8-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="b32b8-104">在此教學課程中，您學會如何 toointegrate JIRA SAML SSO 由 Microsoft Azure Active directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b32b8-104">In this tutorial, you learn how toointegrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b32b8-105">與 Azure AD 整合 microsoft JIRA SAML SSO 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b32b8-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b32b8-106">您可以控制存取 tooJIRA SAML SSO 的 Microsoft Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="b32b8-106">You can control in Azure AD who has access tooJIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="b32b8-107">您可以啟用您的使用者 tooautomatically get 登入 tooJIRA SAML SSO （單一登入） 的 microsoft 使用他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="b32b8-107">You can enable your users tooautomatically get signed-on tooJIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b32b8-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b32b8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b32b8-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b32b8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b32b8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b32b8-110">Prerequisites</span></span>

<span data-ttu-id="b32b8-111">tooconfigure JIRA SAML SSO 的 Microsoft Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b32b8-111">tooconfigure Azure AD integration with JIRA SAML SSO by Microsoft, you need hello following items:</span></span>

- <span data-ttu-id="b32b8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b32b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b32b8-113">JIRA 伺服器應用程式安裝在 Windows 64 位元伺服器 （在內部部署或 hello 雲端 IaaS 基礎結構上）</span><span class="sxs-lookup"><span data-stu-id="b32b8-113">JIRA server application installed on a Windows 64-bit server (on premise or on hello cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="b32b8-114">JIRA 伺服器已啟用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="b32b8-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="b32b8-115">注意 hello 支援版本 JIRA 外掛程式 區段下方所述。</span><span class="sxs-lookup"><span data-stu-id="b32b8-115">Note hello supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="b32b8-116">JIRA 伺服器可連線網際網路上特別 tooAzure AD 登入頁面上進行驗證，應能 tooreceive hello 從 Azure AD 權杖</span><span class="sxs-lookup"><span data-stu-id="b32b8-116">JIRA server is reachable on internet particularly tooAzure AD Login page for authentication and should able tooreceive hello token from Azure AD</span></span>
- <span data-ttu-id="b32b8-117">JIRA 中已設定管理員認證</span><span class="sxs-lookup"><span data-stu-id="b32b8-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="b32b8-118">JIRA 中已停用 WebSudo</span><span class="sxs-lookup"><span data-stu-id="b32b8-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="b32b8-119">測試在 hello JIRA 伺服器應用程式中建立使用者</span><span class="sxs-lookup"><span data-stu-id="b32b8-119">Test user created in hello JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="b32b8-120">本教學課程中的步驟 tootest hello，不建議使用 JIRA 的實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b32b8-120">tootest hello steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="b32b8-121">開發，或預備環境的 hello 應用程式，然後使用 hello 實際執行環境中的第一次測試 hello 整合。</span><span class="sxs-lookup"><span data-stu-id="b32b8-121">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="b32b8-122">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b32b8-122">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b32b8-123">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b32b8-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b32b8-124">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b32b8-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="b32b8-125">支援的 JIRA 版本</span><span class="sxs-lookup"><span data-stu-id="b32b8-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="b32b8-126">目前支援下列 JIRA 版本：</span><span class="sxs-lookup"><span data-stu-id="b32b8-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="b32b8-127">JIRA 核心和軟體： 6.0 too7.2.0</span><span class="sxs-lookup"><span data-stu-id="b32b8-127">JIRA Core and Software: 6.0 too7.2.0</span></span>
- <span data-ttu-id="b32b8-128">JIRA 服務台： 3.0 too3.2</span><span class="sxs-lookup"><span data-stu-id="b32b8-128">JIRA Service Desk: 3.0 too3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b32b8-129">案例描述</span><span class="sxs-lookup"><span data-stu-id="b32b8-129">Scenario description</span></span>
<span data-ttu-id="b32b8-130">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b32b8-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b32b8-131">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b32b8-131">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b32b8-132">新增 microsoft JIRA SAML SSO 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="b32b8-132">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
2. <span data-ttu-id="b32b8-133">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b32b8-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a><span data-ttu-id="b32b8-134">新增 microsoft JIRA SAML SSO 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="b32b8-134">Adding JIRA SAML SSO by Microsoft from hello gallery</span></span>
<span data-ttu-id="b32b8-135">tooconfigure hello 整合 microsoft JIRA SAML SSO 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd microsoft JIRA SAML SSO。</span><span class="sxs-lookup"><span data-stu-id="b32b8-135">tooconfigure hello integration of JIRA SAML SSO by Microsoft into Azure AD, you need tooadd JIRA SAML SSO by Microsoft from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b32b8-136">**tooadd hello 庫、 microsoft JIRA SAML SSO 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b32b8-136">**tooadd JIRA SAML SSO by Microsoft from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b32b8-137">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b32b8-137">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b32b8-139">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-139">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b32b8-140">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-140">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b32b8-142">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b32b8-142">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b32b8-144">在 [hello] 搜尋方塊中，輸入**JIRA SAML SSO microsoft**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-144">In hello search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="b32b8-146">在 hello 結果 窗格中，選取**microsoft JIRA SAML SSO**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b32b8-146">In hello results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b32b8-148">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b32b8-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b32b8-149">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 JIRA SAML SSO by Microsoft 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b32b8-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b32b8-150">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中由 Microsoft JIRA SAML SSO 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b32b8-150">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in JIRA SAML SSO by Microsoft is tooa user in Azure AD.</span></span> <span data-ttu-id="b32b8-151">換句話說，Azure AD 使用者和 microsoft JIRA SAML SSO 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b32b8-151">In other words, a link relationship between an Azure AD user and hello related user in JIRA SAML SSO by Microsoft needs toobe established.</span></span>

<span data-ttu-id="b32b8-152">由 Microsoft JIRA SAML SSO 中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b32b8-152">In JIRA SAML SSO by Microsoft, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b32b8-153">tooconfigure 及測試 JIRA SAML SSO 的 Microsoft Azure AD 單一登入，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b32b8-153">tooconfigure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b32b8-154">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b32b8-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b32b8-155">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b32b8-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b32b8-156">**[建立由 Microsoft 測試使用者 JIRA SAML SSO](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave 許 Simon JIRA SAML SSO 由 Microsoft 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b32b8-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - toohave a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b32b8-157">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b32b8-157">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b32b8-158">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b32b8-158">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b32b8-159">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b32b8-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b32b8-160">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您 JIRA SAML SSO 中由 Microsoft 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b32b8-160">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="b32b8-161">**使用 JIRA SAML SSO 的 Microsoft Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b32b8-161">**tooconfigure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="b32b8-162">在 Azure 入口網站上 hello hello **microsoft JIRA SAML SSO**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-162">In hello Azure portal, on hello **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b32b8-164">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b32b8-164">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="b32b8-166">在 hello **JIRA SAML SSO 的 Microsoft 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b32b8-166">On hello **JIRA SAML SSO by Microsoft Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="b32b8-168">a.</span><span class="sxs-lookup"><span data-stu-id="b32b8-168">a.</span></span> <span data-ttu-id="b32b8-169">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="b32b8-169">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="b32b8-170">b.</span><span class="sxs-lookup"><span data-stu-id="b32b8-170">b.</span></span> <span data-ttu-id="b32b8-171">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="b32b8-171">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="b32b8-172">c.</span><span class="sxs-lookup"><span data-stu-id="b32b8-172">c.</span></span> <span data-ttu-id="b32b8-173">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="b32b8-173">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b32b8-174">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="b32b8-174">These values are not real.</span></span> <span data-ttu-id="b32b8-175">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="b32b8-175">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b32b8-176">如果連接埠是具名 URL，則為選擇性。</span><span class="sxs-lookup"><span data-stu-id="b32b8-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="b32b8-177">Hello Jira 外掛程式，在 hello 教學課程稍後會說明設定期間，會收到這些值。</span><span class="sxs-lookup"><span data-stu-id="b32b8-177">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="b32b8-178">toogenerate hello**中繼資料**url，請執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b32b8-178">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="b32b8-179">a.</span><span class="sxs-lookup"><span data-stu-id="b32b8-179">a.</span></span> <span data-ttu-id="b32b8-180">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="b32b8-180">Click **App registrations**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="b32b8-182">b.</span><span class="sxs-lookup"><span data-stu-id="b32b8-182">b.</span></span> <span data-ttu-id="b32b8-183">按一下**端點**tooopen**端點** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b32b8-183">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="b32b8-185">c.</span><span class="sxs-lookup"><span data-stu-id="b32b8-185">c.</span></span> <span data-ttu-id="b32b8-186">按一下 hello 複製按鈕 toocopy**同盟中繼資料文件**url 並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="b32b8-186">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="b32b8-188">d.</span><span class="sxs-lookup"><span data-stu-id="b32b8-188">d.</span></span> <span data-ttu-id="b32b8-189">現在請 toohello 屬性頁的**JIRA SAML SSO microsoft**和複製 hello**應用程式識別碼**使用**複製**按鈕，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="b32b8-189">Now go toohello property page of **JIRA SAML SSO by Microsoft** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="b32b8-191">e.</span><span class="sxs-lookup"><span data-stu-id="b32b8-191">e.</span></span> <span data-ttu-id="b32b8-192">產生 hello**中繼資料 URL**使用 hello 下列模式：`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`並將此值複製 [記事本] 中，因為它正使用更新版本的 hello 外掛程式 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="b32b8-192">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for hello configuration of hello plugin.</span></span>

5. <span data-ttu-id="b32b8-193">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b32b8-193">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b32b8-195">請連絡[Microsoft](mailto:waadpartners@microsoft.com)以 hello 下列 hello JIRA 外掛程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="b32b8-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with hello following information for hello JIRA plugin.</span></span>
    
    *   <span data-ttu-id="b32b8-196">客戶名稱：</span><span class="sxs-lookup"><span data-stu-id="b32b8-196">Customer Name:</span></span>
    *   <span data-ttu-id="b32b8-197">主要網域名稱：</span><span class="sxs-lookup"><span data-stu-id="b32b8-197">Primary domain name:</span></span>
    *   <span data-ttu-id="b32b8-198">Azure AD Premium： 是/否 （外掛程式將使用 tooall hello 客戶 Free、 Basic 和 Premium SKU）</span><span class="sxs-lookup"><span data-stu-id="b32b8-198">Azure AD Premium: Yes/No (Plugin will be available tooall     hello customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="b32b8-199">將會使用這項整合的使用者數目：</span><span class="sxs-lookup"><span data-stu-id="b32b8-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="b32b8-200">JIRA 版本：</span><span class="sxs-lookup"><span data-stu-id="b32b8-200">JIRA Version:</span></span>
    *   <span data-ttu-id="b32b8-201">註解：</span><span class="sxs-lookup"><span data-stu-id="b32b8-201">Comments:</span></span>

7. <span data-ttu-id="b32b8-202">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour JIRA 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b32b8-202">In a different web browser window, log in tooyour JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="b32b8-203">將滑鼠停留在齒輪，然後按一下 hello**附加元件**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-203">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="b32b8-205">在 [附加元件] 索引標籤區段下，按一下 [管理附加元件]。</span><span class="sxs-lookup"><span data-stu-id="b32b8-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="b32b8-207">手動上傳 hello 由 Microsoft 提供的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="b32b8-207">Manually upload hello plugin provided by Microsoft.</span></span> <span data-ttu-id="b32b8-208">Hello 外掛程式安裝之後，它會出現在**使用者安裝**附加元件區段**管理附加元件**> 一節。</span><span class="sxs-lookup"><span data-stu-id="b32b8-208">Once hello plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="b32b8-209">按一下**設定**tooconfigure hello 新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="b32b8-209">Click **Configure** tooconfigure hello new plugin.</span></span>

12. <span data-ttu-id="b32b8-210">在設定頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b32b8-210">Perform following steps on configuration page:</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="b32b8-212">a.</span><span class="sxs-lookup"><span data-stu-id="b32b8-212">a.</span></span> <span data-ttu-id="b32b8-213">在**中繼資料 URL**貼上 hello**中繼資料 URL**從 Azure AD 產生，並按一下 hello**解決** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b32b8-213">In **Metadata URL** paste hello **Metadata URL** generated from Azure AD and click hello **Resolve** button.</span></span> <span data-ttu-id="b32b8-214">它會讀取 hello IdP 中繼資料 URL，並於其中填入 hello 欄位的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="b32b8-214">It reads hello IdP metadata URL and populates all hello fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="b32b8-215">預設 SAML 使用者識別碼位置是名稱識別碼。</span><span class="sxs-lookup"><span data-stu-id="b32b8-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="b32b8-216">您可以變更這個 tooan 屬性選項，然後輸入 hello 適當的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="b32b8-216">You can change this tooan attribute option and enter hello appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="b32b8-217">確定只有一個對應 hello 應用程式，使其解析 hello 中繼資料中沒有任何錯誤的憑證。</span><span class="sxs-lookup"><span data-stu-id="b32b8-217">Ensure that there is only one certificate mapped against hello app so that there is no error in resolving hello metadata.</span></span> <span data-ttu-id="b32b8-218">如果有多個憑證，在解析 hello 中繼資料，系統管理員取得發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b32b8-218">If there are multiple certificates, upon resolving hello metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="b32b8-219">b.</span><span class="sxs-lookup"><span data-stu-id="b32b8-219">b.</span></span> <span data-ttu-id="b32b8-220">複製 hello**識別碼、 回覆 URL 和登入 URL**值並貼在**識別碼、 回覆 URL 和登入 URL**文字方塊分別以**JIRA SAML SSO 的 Microsoft 網域和 Url** Azure 入口網站上的一節。</span><span class="sxs-lookup"><span data-stu-id="b32b8-220">Copy hello **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="b32b8-221">c.</span><span class="sxs-lookup"><span data-stu-id="b32b8-221">c.</span></span> <span data-ttu-id="b32b8-222">在**登入按鈕名稱**類型 hello 名稱的按鈕，您的組織希望 hello 使用者 toosee 登入畫面上的。</span><span class="sxs-lookup"><span data-stu-id="b32b8-222">In **Login Button Name** type hello name of button your organization wants hello users toosee on login screen.</span></span>

    <span data-ttu-id="b32b8-223">d.</span><span class="sxs-lookup"><span data-stu-id="b32b8-223">d.</span></span> <span data-ttu-id="b32b8-224">在**SAML 使用者識別碼位置**選取**hello 的 hello Subject 陳述式的 NameIdentifier 元素中的使用者識別碼是**或**屬性項目中的使用者識別碼是**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-224">In **SAML User ID Locations** select either **User ID is in hello NameIdentifier element of hello Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="b32b8-225">此識別碼具有 toobe hello JIRA 使用者識別碼。如果不符合 hello 使用者識別碼，系統將不會允許使用者 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="b32b8-225">This ID has toobe hello JIRA user id. If hello user id is not matched, then system will not allow users toolog in.</span></span> 
    
    <span data-ttu-id="b32b8-226">e.</span><span class="sxs-lookup"><span data-stu-id="b32b8-226">e.</span></span> <span data-ttu-id="b32b8-227">如果您選取**屬性項目中的使用者識別碼是**選項，然後在**屬性名稱**文字方塊類型 hello 屬性名稱的 hello 卻使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="b32b8-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type hello name of hello attribute where User Id is expected.</span></span> 

    <span data-ttu-id="b32b8-228">f.</span><span class="sxs-lookup"><span data-stu-id="b32b8-228">f.</span></span> <span data-ttu-id="b32b8-229">如果您正在使用 Azure AD 的 hello （例如 ADFS 等等） 的同盟的網域，然後按一下 上 hello**啟用主領域探索**選項，並設定 hello**網域名稱**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-229">If you are using hello federated domain (like ADFS etc.) with Azure AD, then click on hello **Enable Home Realm Discovery** option and configure hello **Domain Name**.</span></span>
    
    <span data-ttu-id="b32b8-230">g.</span><span class="sxs-lookup"><span data-stu-id="b32b8-230">g.</span></span> <span data-ttu-id="b32b8-231">在**網域名稱**hello 網域在此輸入名稱發生 hello ADFS 為基礎的登入。</span><span class="sxs-lookup"><span data-stu-id="b32b8-231">In **Domain Name** type hello domain name here in case of hello ADFS-based login.</span></span>

    <span data-ttu-id="b32b8-232">h.</span><span class="sxs-lookup"><span data-stu-id="b32b8-232">h.</span></span> <span data-ttu-id="b32b8-233">請檢查**啟用單一登出**如果您想從 Azure AD，當使用者登出從 JIRA toolog 出。</span><span class="sxs-lookup"><span data-stu-id="b32b8-233">Check **Enable Single Sign out** if you wish toolog out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="b32b8-234">i.</span><span class="sxs-lookup"><span data-stu-id="b32b8-234">i.</span></span> <span data-ttu-id="b32b8-235">按一下**儲存**按鈕 toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="b32b8-235">Click **Save** button toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="b32b8-236">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b32b8-236">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b32b8-237">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b32b8-237">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b32b8-238">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b32b8-238">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b32b8-239">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b32b8-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="b32b8-240">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b32b8-240">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b32b8-242">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b32b8-242">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b32b8-243">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b32b8-243">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b32b8-245">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-245">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b32b8-247">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="b32b8-247">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b32b8-249">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b32b8-249">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b32b8-251">a.</span><span class="sxs-lookup"><span data-stu-id="b32b8-251">a.</span></span> <span data-ttu-id="b32b8-252">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-252">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b32b8-253">b.</span><span class="sxs-lookup"><span data-stu-id="b32b8-253">b.</span></span> <span data-ttu-id="b32b8-254">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="b32b8-254">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b32b8-255">c.</span><span class="sxs-lookup"><span data-stu-id="b32b8-255">c.</span></span> <span data-ttu-id="b32b8-256">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-256">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b32b8-257">d.</span><span class="sxs-lookup"><span data-stu-id="b32b8-257">d.</span></span> <span data-ttu-id="b32b8-258">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b32b8-258">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="b32b8-259">建立 JIRA SAML SSO by Microsoft 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b32b8-259">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="b32b8-260">tooenable Azure AD 使用者 toolog tooJIRA 在內部部署伺服器，您必須佈建到 JIRA SAML SSO microsoft。</span><span class="sxs-lookup"><span data-stu-id="b32b8-260">tooenable Azure AD users toolog in tooJIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="b32b8-261">對於 JIRA SAML SSO by Microsoft，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="b32b8-261">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="b32b8-262">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b32b8-262">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b32b8-263">登入 tooyour JIRA 在內部部署伺服器以系統管理員。</span><span class="sxs-lookup"><span data-stu-id="b32b8-263">Log in tooyour JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="b32b8-264">將滑鼠停留在齒輪，然後按一下 hello**使用者管理**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-264">Hover on cog and click hello **User management**.</span></span>

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="b32b8-266">您會重新導向的 tooAdministrator 存取頁面 tooenter**密碼**按一下**確認** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b32b8-266">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="b32b8-268">在 [使用者管理] 索引標籤區段下，按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="b32b8-268">Under **User management** tab section, click **create user**.</span></span>

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="b32b8-270">在 hello **「 建立新的使用者 」**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b32b8-270">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="b32b8-272">a.</span><span class="sxs-lookup"><span data-stu-id="b32b8-272">a.</span></span> <span data-ttu-id="b32b8-273">在 hello**電子郵件地址**文字方塊中，輸入 hello 電子郵件地址的使用者喜歡Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="b32b8-273">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="b32b8-274">b.</span><span class="sxs-lookup"><span data-stu-id="b32b8-274">b.</span></span> <span data-ttu-id="b32b8-275">在 hello**全名**文字方塊中，例如許 Simon 的 hello 使用者類型完整名稱。</span><span class="sxs-lookup"><span data-stu-id="b32b8-275">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="b32b8-276">c.</span><span class="sxs-lookup"><span data-stu-id="b32b8-276">c.</span></span> <span data-ttu-id="b32b8-277">在 hello **Username**文字方塊中，型別 hello 電子郵件的使用者要Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="b32b8-277">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="b32b8-278">d.</span><span class="sxs-lookup"><span data-stu-id="b32b8-278">d.</span></span> <span data-ttu-id="b32b8-279">在 hello**密碼**文字方塊中，輸入 hello 密碼的使用者。</span><span class="sxs-lookup"><span data-stu-id="b32b8-279">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="b32b8-280">e.</span><span class="sxs-lookup"><span data-stu-id="b32b8-280">e.</span></span> <span data-ttu-id="b32b8-281">按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="b32b8-281">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b32b8-282">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="b32b8-282">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b32b8-283">在本節中，您可以授與存取 tooJIRA SAML SSO 由 Microsoft 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b32b8-283">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJIRA SAML SSO by Microsoft.</span></span>

![指派使用者][200] 

<span data-ttu-id="b32b8-285">**tooassign 許 Simon tooJIRA microsoft SAML SSO 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b32b8-285">**tooassign Britta Simon tooJIRA SAML SSO by Microsoft, perform hello following steps:**</span></span>

1. <span data-ttu-id="b32b8-286">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-286">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b32b8-288">在 [hello] 應用程式清單中，選取**JIRA SAML SSO microsoft**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-288">In hello applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="b32b8-290">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b32b8-290">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b32b8-292">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b32b8-292">Click **Add** button.</span></span> <span data-ttu-id="b32b8-293">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b32b8-293">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b32b8-295">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b32b8-295">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b32b8-296">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b32b8-296">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b32b8-297">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b32b8-297">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b32b8-298">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b32b8-298">Testing single sign-on</span></span>

<span data-ttu-id="b32b8-299">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b32b8-299">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b32b8-300">當您按一下 hello JIRA SAML SSO 由 Microsoft 磚 hello 存取面板中時，您應該取得自動登入 tooyour JIRA SAML SSO 的 Microsoft 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b32b8-300">When you click hello JIRA SAML SSO by Microsoft tile in hello Access Panel, you should get automatically signed-on tooyour JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="b32b8-301">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b32b8-301">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b32b8-302">其他資源</span><span class="sxs-lookup"><span data-stu-id="b32b8-302">Additional resources</span></span>

* [<span data-ttu-id="b32b8-303">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b32b8-303">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b32b8-304">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b32b8-304">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

