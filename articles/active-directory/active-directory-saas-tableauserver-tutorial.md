---
title: "教學課程：Azure Active Directory 與 Tableau Server 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Tableau 伺服器之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a><span data-ttu-id="70936-103">教學課程：Azure Active Directory 與 Tableau Server 整合</span><span class="sxs-lookup"><span data-stu-id="70936-103">Tutorial: Azure Active Directory integration with Tableau Server</span></span>

<span data-ttu-id="70936-104">在此教學課程中，您學會如何 toointegrate Tableau 伺服器與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="70936-104">In this tutorial, you learn how toointegrate Tableau Server with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70936-105">與 Azure AD 整合 Tableau 伺服器可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="70936-105">Integrating Tableau Server with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="70936-106">您可以控制存取 tooTableau 伺服器的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="70936-106">You can control in Azure AD who has access tooTableau Server</span></span>
- <span data-ttu-id="70936-107">您可以啟用您的使用者 tooautomatically get 登入 tooTableau （單一登入） 的伺服器使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="70936-107">You can enable your users tooautomatically get signed-on tooTableau Server (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70936-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="70936-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="70936-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="70936-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70936-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="70936-110">Prerequisites</span></span>

<span data-ttu-id="70936-111">tooconfigure Tableau 伺服器與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="70936-111">tooconfigure Azure AD integration with Tableau Server, you need hello following items:</span></span>

- <span data-ttu-id="70936-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="70936-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70936-113">已啟用 Tableau Server 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="70936-113">A Tableau Server single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70936-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="70936-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70936-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="70936-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70936-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="70936-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70936-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="70936-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70936-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="70936-118">Scenario description</span></span>
<span data-ttu-id="70936-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="70936-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70936-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="70936-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70936-121">新增 Tableau 伺服器從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="70936-121">Adding Tableau Server from hello gallery</span></span>
2. <span data-ttu-id="70936-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="70936-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-server-from-hello-gallery"></a><span data-ttu-id="70936-123">新增 Tableau 伺服器從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="70936-123">Adding Tableau Server from hello gallery</span></span>
<span data-ttu-id="70936-124">tooconfigure hello 整合 Tableau 伺服器到 Azure AD，您需要 tooadd Tableau 伺服器 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70936-124">tooconfigure hello integration of Tableau Server into Azure AD, you need tooadd Tableau Server from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="70936-125">**tooadd Tableau 伺服器 hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="70936-125">**tooadd Tableau Server from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="70936-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="70936-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70936-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="70936-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="70936-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="70936-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="70936-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="70936-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="70936-133">在 [hello] 搜尋方塊中，輸入**Tableau 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="70936-133">In hello search box, type **Tableau Server**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. <span data-ttu-id="70936-135">在 [hello [結果] 窗格中，選取 [ **Tableau 伺服器**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70936-135">In hello results panel, select **Tableau Server**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70936-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="70936-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70936-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Tableau Server 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="70936-138">In this section, you configure and test Azure AD single sign-on with Tableau Server based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70936-139">單一登入 toowork，Azure AD 需要 tooknow Tableau Server 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="70936-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Server is tooa user in Azure AD.</span></span> <span data-ttu-id="70936-140">換句話說，Azure AD 使用者與 hello Tableau 伺服器中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="70936-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Server needs toobe established.</span></span>

<span data-ttu-id="70936-141">Tableau Server 中指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="70936-141">In Tableau Server, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="70936-142">tooconfigure 及 Tableau 伺服器與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="70936-142">tooconfigure and test Azure AD single sign-on with Tableau Server, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="70936-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="70936-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="70936-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="70936-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70936-145">**[建立 Tableau 伺服器測試使用者](#creating-a-tableau-server-test-user)** -toohave 許 Simon Tableau 伺服器是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="70936-145">**[Creating a Tableau Server test user](#creating-a-tableau-server-test-user)** - toohave a counterpart of Britta Simon in Tableau Server that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="70936-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="70936-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70936-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="70936-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70936-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="70936-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70936-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Tableau 伺服器應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="70936-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Server application.</span></span>

<span data-ttu-id="70936-150">**tooconfigure Azure AD 單一登入與 Tableau 伺服器，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="70936-150">**tooconfigure Azure AD single sign-on with Tableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="70936-151">在 Azure 入口網站上 hello hello **Tableau 伺服器**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="70936-151">In hello Azure portal, on hello **Tableau Server** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="70936-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="70936-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. <span data-ttu-id="70936-155">在 [hello **Tableau 伺服器網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="70936-155">On hello **Tableau Server Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    <span data-ttu-id="70936-157">a.</span><span class="sxs-lookup"><span data-stu-id="70936-157">a.</span></span> <span data-ttu-id="70936-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="70936-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>
    
    <span data-ttu-id="70936-159">b.</span><span class="sxs-lookup"><span data-stu-id="70936-159">b.</span></span> <span data-ttu-id="70936-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://azure.<domain name>.link`</span><span class="sxs-lookup"><span data-stu-id="70936-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link`</span></span>

    <span data-ttu-id="70936-161">c.</span><span class="sxs-lookup"><span data-stu-id="70936-161">c.</span></span> <span data-ttu-id="70936-162">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://azure.<domain name>.link/wg/saml/SSO/index.html`</span><span class="sxs-lookup"><span data-stu-id="70936-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://azure.<domain name>.link/wg/saml/SSO/index.html`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="70936-163">hello 上述值不是實際值。</span><span class="sxs-lookup"><span data-stu-id="70936-163">hello preceding values are not real values.</span></span> <span data-ttu-id="70936-164">更新版本中，您可以更新 hello 值有 hello 實際的 URL 和從 hello Tableau 伺服器組態] 頁面上的識別項。</span><span class="sxs-lookup"><span data-stu-id="70936-164">Later, you update hello values with hello actual URL and identifier from hello Tableau Server configuration page.</span></span> 

4. <span data-ttu-id="70936-165">Tableau 伺服器應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="70936-165">Tableau Server application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="70936-166">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="70936-166">Configure hello following claims for this application.</span></span> <span data-ttu-id="70936-167">您可以從 hello 管理這些屬性的 hello 值**使用者屬性 」**應用程式整合頁面上的一節。</span><span class="sxs-lookup"><span data-stu-id="70936-167">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span> <span data-ttu-id="70936-168">hello 下列螢幕擷取畫面顯示 hello 的範例相同。</span><span class="sxs-lookup"><span data-stu-id="70936-168">hello following screenshot shows an example for hello same.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. <span data-ttu-id="70936-170">在 hello**使用者屬性**區段 hello**單一登入**] 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="70936-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="70936-171">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="70936-171">Attribute Name</span></span> | <span data-ttu-id="70936-172">屬性值</span><span class="sxs-lookup"><span data-stu-id="70936-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="70936-173">username</span><span class="sxs-lookup"><span data-stu-id="70936-173">username</span></span> | <span data-ttu-id="70936-174">*user.displayname*</span><span class="sxs-lookup"><span data-stu-id="70936-174">*user.displayname*</span></span> |

    <span data-ttu-id="70936-175">a.</span><span class="sxs-lookup"><span data-stu-id="70936-175">a.</span></span> <span data-ttu-id="70936-176">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="70936-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    <span data-ttu-id="70936-179">b.</span><span class="sxs-lookup"><span data-stu-id="70936-179">b.</span></span> <span data-ttu-id="70936-180">在 [hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="70936-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="70936-181">c.</span><span class="sxs-lookup"><span data-stu-id="70936-181">c.</span></span> <span data-ttu-id="70936-182">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="70936-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="70936-183">d.</span><span class="sxs-lookup"><span data-stu-id="70936-183">d.</span></span> <span data-ttu-id="70936-184">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="70936-184">Click **Ok**</span></span>


6. <span data-ttu-id="70936-185">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="70936-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. <span data-ttu-id="70936-187">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="70936-187">Click **Save** button.</span></span>

    <span data-ttu-id="70936-188">![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="70936-188">![Configure Single Sign-On](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS></span></span>
8. <span data-ttu-id="70936-189">tooget SSO 設定應用程式，您需要 toosign 上 tooyour Tableau Server 租用戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="70936-189">tooget SSO configured for your application, you need toosign-on tooyour Tableau Server tenant as an administrator.</span></span>
   
   <span data-ttu-id="70936-190">a.</span><span class="sxs-lookup"><span data-stu-id="70936-190">a.</span></span> <span data-ttu-id="70936-191">在 [hello Tableau 伺服器組態中，按一下 [hello **SAML** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="70936-191">In hello Tableau Server configuration, click hello **SAML** tab.</span></span>
  
    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   <span data-ttu-id="70936-193">b.</span><span class="sxs-lookup"><span data-stu-id="70936-193">b.</span></span> <span data-ttu-id="70936-194">選取的 hello 核取方塊**使用 SAML 進行單一登入**。</span><span class="sxs-lookup"><span data-stu-id="70936-194">Select hello checkbox of **Use SAML for single sign-on**.</span></span>
   
   <span data-ttu-id="70936-195">c.</span><span class="sxs-lookup"><span data-stu-id="70936-195">c.</span></span> <span data-ttu-id="70936-196">Tableau 伺服器傳回的 URL: hello Tableau Server 使用者將用來存取，例如 http://tableau_server 的 URL。</span><span class="sxs-lookup"><span data-stu-id="70936-196">Tableau Server return URL—hello URL that Tableau Server users will be accessing, such as http://tableau_server.</span></span> <span data-ttu-id="70936-197">不建議使用 http://localhost。</span><span class="sxs-lookup"><span data-stu-id="70936-197">Using http://localhost is not recommended.</span></span> <span data-ttu-id="70936-198">不支援使用包含結尾斜線的 URL (例如，http://tableau_server/)。</span><span class="sxs-lookup"><span data-stu-id="70936-198">Using a URL with a trailing slash (for example, http://tableau_server/) is not supported.</span></span> <span data-ttu-id="70936-199">複製**Tableau 伺服器傳回的 URL**並將它貼 tooAzure AD**登入 URL** ] 文字方塊中的**Tableau 伺服器網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="70936-199">Copy **Tableau Server return URL** and paste it tooAzure AD **Sign On URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="70936-200">d.</span><span class="sxs-lookup"><span data-stu-id="70936-200">d.</span></span> <span data-ttu-id="70936-201">SAML 實體識別碼： hello 實體識別碼可唯一識別您 Tableau 伺服器安裝 toohello IdP。</span><span class="sxs-lookup"><span data-stu-id="70936-201">SAML entity ID—hello entity ID uniquely identifies your Tableau Server installation toohello IdP.</span></span> <span data-ttu-id="70936-202">您可以輸入 Tableau 伺服器 URL 一次，如果需要，但是它並沒有 toobe Tableau 伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="70936-202">You can enter your Tableau Server URL again here, if you like, but it does not have toobe your Tableau Server URL.</span></span> <span data-ttu-id="70936-203">複製**SAML 實體識別碼**並將它貼 tooAzure AD**識別碼**] 文字方塊中的**Tableau 伺服器網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="70936-203">Copy **SAML entity ID** and paste it tooAzure AD **Identifier** textbox in **Tableau Server Domain and URLs** section.</span></span>
     
   <span data-ttu-id="70936-204">e.</span><span class="sxs-lookup"><span data-stu-id="70936-204">e.</span></span> <span data-ttu-id="70936-205">按一下 hello**匯出中繼資料檔案**在 hello 文字編輯器應用程式中開啟它。</span><span class="sxs-lookup"><span data-stu-id="70936-205">Click hello **Export Metadata File** and open it in hello text editor application.</span></span> <span data-ttu-id="70936-206">找出判斷提示取用者服務 URL，Http Post 和索引 0 與複製 hello URL。</span><span class="sxs-lookup"><span data-stu-id="70936-206">Locate Assertion Consumer Service URL with Http Post and Index 0 and copy hello URL.</span></span> <span data-ttu-id="70936-207">現在將它貼入 tooAzure AD**回覆 URL** ] 文字方塊中的**Tableau 伺服器網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="70936-207">Now paste it tooAzure AD **Reply URL** textbox in **Tableau Server Domain and URLs** section.</span></span>
   
   <span data-ttu-id="70936-208">f.</span><span class="sxs-lookup"><span data-stu-id="70936-208">f.</span></span> <span data-ttu-id="70936-209">尋找您從 Azure 入口網站下載的同盟中繼資料檔案，然後將它上傳在 hello **SAML Idp 中繼資料檔案**。</span><span class="sxs-lookup"><span data-stu-id="70936-209">Locate your Federation Metadata file downloaded from Azure portal, and then upload it in hello **SAML Idp metadata file**.</span></span>
   
   <span data-ttu-id="70936-210">g.</span><span class="sxs-lookup"><span data-stu-id="70936-210">g.</span></span> <span data-ttu-id="70936-211">按一下 hello**確定**hello Tableau 伺服器組態] 頁面中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="70936-211">Click hello **OK** button in hello Tableau Server Configuration page.</span></span>
   
    >[!NOTE] 
    ><span data-ttu-id="70936-212">客戶有 tooupload 任何憑證 hello Tableau Server SAML SSO 設定中，它將會遭到忽略 hello SSO 資料流程中。</span><span class="sxs-lookup"><span data-stu-id="70936-212">Customer have tooupload any certificate in hello Tableau Server SAML SSO configuration and it will get ignored in hello SSO flow.</span></span>
    ><span data-ttu-id="70936-213">如果您需要協助 Tableau 伺服器上設定 SAML 則 toothis 發行項，請參閱[設定 SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm)。</span><span class="sxs-lookup"><span data-stu-id="70936-213">If you need help configuring SAML on Tableau Server then please refer toothis article [Configure SAML](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).</span></span>
    >
<CE>

> [!TIP]
> <span data-ttu-id="70936-214">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="70936-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="70936-215">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="70936-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="70936-216">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70936-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70936-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="70936-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="70936-218">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="70936-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="70936-220">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="70936-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="70936-221">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="70936-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70936-223">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="70936-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70936-225">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="70936-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70936-227">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="70936-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70936-229">a.</span><span class="sxs-lookup"><span data-stu-id="70936-229">a.</span></span> <span data-ttu-id="70936-230">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="70936-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70936-231">b.</span><span class="sxs-lookup"><span data-stu-id="70936-231">b.</span></span> <span data-ttu-id="70936-232">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="70936-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70936-233">c.</span><span class="sxs-lookup"><span data-stu-id="70936-233">c.</span></span> <span data-ttu-id="70936-234">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="70936-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="70936-235">d.</span><span class="sxs-lookup"><span data-stu-id="70936-235">d.</span></span> <span data-ttu-id="70936-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="70936-236">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-server-test-user"></a><span data-ttu-id="70936-237">建立 Tableau Server 測試使用者</span><span class="sxs-lookup"><span data-stu-id="70936-237">Creating a Tableau Server test user</span></span>

<span data-ttu-id="70936-238">hello 本節目標在於 toocreate 呼叫許 Simon Tableau Server 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="70936-238">hello objective of this section is toocreate a user called Britta Simon in Tableau Server.</span></span> <span data-ttu-id="70936-239">您需要 tooprovision hello Tableau 伺服器中的所有 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="70936-239">You need tooprovision all hello users in hello Tableau server.</span></span> 

<span data-ttu-id="70936-240">Hello 使用者的該使用者名稱應符合您已在 hello Azure AD 的自訂屬性中的 hello 值**username**。</span><span class="sxs-lookup"><span data-stu-id="70936-240">That username of hello user should match hello value which you have configured in hello Azure AD custom attribute of **username**.</span></span> <span data-ttu-id="70936-241">以正確對應 hello 整合應該會運作的 hello[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="70936-241">With hello correct mapping hello integration should work [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="70936-242">若要手動 toocreate 使用者，您會需要 toocontact hello Tableau 伺服器系統管理員，您組織中。</span><span class="sxs-lookup"><span data-stu-id="70936-242">If you need toocreate a user manually, you need toocontact hello Tableau Server administrator in your organization.</span></span>
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="70936-243">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="70936-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="70936-244">本節中，您可以授與存取 tooTableau 伺服器啟用了許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="70936-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Server.</span></span>

![指派使用者][200] 

<span data-ttu-id="70936-246">**tooassign 許 Simon tooTableau 伺服器上，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="70936-246">**tooassign Britta Simon tooTableau Server, perform hello following steps:**</span></span>

1. <span data-ttu-id="70936-247">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="70936-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="70936-249">在 [hello] 應用程式清單中，選取**Tableau 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="70936-249">In hello applications list, select **Tableau Server**.</span></span>

    ![設定單一登入](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. <span data-ttu-id="70936-251">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="70936-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="70936-253">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="70936-253">Click **Add** button.</span></span> <span data-ttu-id="70936-254">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="70936-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="70936-256">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="70936-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="70936-257">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="70936-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70936-258">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="70936-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70936-259">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="70936-259">Testing single sign-on</span></span>

<span data-ttu-id="70936-260">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="70936-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="70936-261">當您按一下 hello Tableau 伺服器] 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Tableau 伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="70936-261">When you click hello Tableau Server tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Server application.</span></span>
<span data-ttu-id="70936-262">如需存取面板的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="70936-262">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="70936-263">其他資源</span><span class="sxs-lookup"><span data-stu-id="70936-263">Additional resources</span></span>

* [<span data-ttu-id="70936-264">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70936-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70936-265">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="70936-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

