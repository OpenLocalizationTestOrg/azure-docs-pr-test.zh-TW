---
title: "教學課程：Azure Active Directory 與 DocuSign 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 DocuSign 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="0b83a-103">教學課程：Azure Active Directory 與 DocuSign 整合</span><span class="sxs-lookup"><span data-stu-id="0b83a-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="0b83a-104">在此教學課程中，您學會如何 toointegrate DocuSign 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0b83a-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b83a-105">整合 Azure AD 與 DocuSign 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="0b83a-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0b83a-106">您可以控制存取 tooDocuSign Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="0b83a-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="0b83a-107">您可以啟用您的使用者 tooautomatically get 登入 tooDocuSign （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="0b83a-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b83a-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0b83a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0b83a-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0b83a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b83a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0b83a-110">Prerequisites</span></span>

<span data-ttu-id="0b83a-111">tooconfigure Azure AD 與 DocuSign 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="0b83a-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="0b83a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0b83a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b83a-113">已啟用 DocuSign 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0b83a-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b83a-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0b83a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b83a-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0b83a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b83a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0b83a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b83a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0b83a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b83a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0b83a-118">Scenario description</span></span>
<span data-ttu-id="0b83a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b83a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b83a-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0b83a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b83a-121">從 hello 圖庫加入 DocuSign</span><span class="sxs-lookup"><span data-stu-id="0b83a-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="0b83a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0b83a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="0b83a-123">從 hello 圖庫加入 DocuSign</span><span class="sxs-lookup"><span data-stu-id="0b83a-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="0b83a-124">tooconfigure hello 整合 DocuSign 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd DocuSign。</span><span class="sxs-lookup"><span data-stu-id="0b83a-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0b83a-125">**tooadd DocuSign hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0b83a-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b83a-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0b83a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b83a-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0b83a-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0b83a-131">按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b83a-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0b83a-133">在 [hello] 搜尋方塊中，輸入**DocuSign**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-133">In hello search box, type **DocuSign**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="0b83a-135">在 [hello [結果] 窗格中，選取 [ **DocuSign**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b83a-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b83a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0b83a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b83a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 DocuSign 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b83a-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0b83a-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 docusign 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0b83a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="0b83a-140">換句話說，Azure AD 使用者與 docusign 的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="0b83a-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="0b83a-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** docusign。</span><span class="sxs-lookup"><span data-stu-id="0b83a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="0b83a-142">tooconfigure 及 Azure AD 單一登入與 DocuSign 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="0b83a-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0b83a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="0b83a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0b83a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="0b83a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b83a-145">**[建立測試使用者 DocuSign](#creating-a-docusign-test-user) ** -toohave 許 Simon docusign 連結的 toohello Azure AD 使用者表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="0b83a-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b83a-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b83a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b83a-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="0b83a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b83a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0b83a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b83a-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 DocuSign 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="0b83a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="0b83a-150">**tooconfigure Azure AD 單一登入與 DocuSign，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0b83a-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b83a-151">在 Azure 入口網站上 hello hello **DocuSign**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0b83a-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b83a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="0b83a-155">在 [hello **SAML 簽章憑證**區段中，按一下**憑證 (base-64)**然後儲存憑證檔案儲存在您的電腦。</span><span class="sxs-lookup"><span data-stu-id="0b83a-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="0b83a-157">在 hello **DocuSign 組態**> 一節的 Azure 入口網站中，按一下**設定 DocuSign** tooopen 設定登入視窗。</span><span class="sxs-lookup"><span data-stu-id="0b83a-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="0b83a-158">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="0b83a-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="0b83a-160">在不同的網頁瀏覽器視窗中，登入 tooyour **DocuSign 管理員入口網站**身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="0b83a-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="0b83a-161">在 [hello hello 左側的導覽功能表上，按一下 [**網域**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![設定單一登入][51]

7. <span data-ttu-id="0b83a-163">在 [hello 右窗格中，按一下 [**宣告網域**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![設定單一登入][52]

8. <span data-ttu-id="0b83a-165">在 [hello**宣告網域**對話方塊中的，在 [hello**網域名稱**文字方塊中，輸入您公司的網域，然後再按一下**宣告**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="0b83a-166">請確定您確認 hello 網域，而且 hello 狀態為使用中。</span><span class="sxs-lookup"><span data-stu-id="0b83a-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![設定單一登入][53]

9. <span data-ttu-id="0b83a-168">在 [hello 左側功能表中，按一下 [**身分識別提供者**</span><span class="sxs-lookup"><span data-stu-id="0b83a-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![設定單一登入][54]
10. <span data-ttu-id="0b83a-170">Hello 右窗格中，按一下 [**新增身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![設定單一登入][55]

11. <span data-ttu-id="0b83a-172">在 [hello**身分識別提供者設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0b83a-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![設定單一登入][56]

    <span data-ttu-id="0b83a-174">a.</span><span class="sxs-lookup"><span data-stu-id="0b83a-174">a.</span></span> <span data-ttu-id="0b83a-175">在 [hello**名稱**文字方塊中，輸入您的組態的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="0b83a-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="0b83a-176">請勿使用空格。</span><span class="sxs-lookup"><span data-stu-id="0b83a-176">Do not use spaces.</span></span>

    <span data-ttu-id="0b83a-177">b.</span><span class="sxs-lookup"><span data-stu-id="0b83a-177">b.</span></span> <span data-ttu-id="0b83a-178">貼上**SAML 實體識別碼**到 hello**身分識別提供者簽發者**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0b83a-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="0b83a-179">c.</span><span class="sxs-lookup"><span data-stu-id="0b83a-179">c.</span></span> <span data-ttu-id="0b83a-180">貼上**SAML 單一登入服務 URL**到 hello**身分識別提供者登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0b83a-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="0b83a-181">d.</span><span class="sxs-lookup"><span data-stu-id="0b83a-181">d.</span></span> <span data-ttu-id="0b83a-182">貼上**登出 URL**到 hello**身分識別提供者登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0b83a-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="0b83a-183">e.</span><span class="sxs-lookup"><span data-stu-id="0b83a-183">e.</span></span> <span data-ttu-id="0b83a-184">選取 [登入驗證要求]。</span><span class="sxs-lookup"><span data-stu-id="0b83a-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="0b83a-185">f.</span><span class="sxs-lookup"><span data-stu-id="0b83a-185">f.</span></span> <span data-ttu-id="0b83a-186">選取 [POST] 做為 [驗證要求傳送方式]。</span><span class="sxs-lookup"><span data-stu-id="0b83a-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="0b83a-187">g.</span><span class="sxs-lookup"><span data-stu-id="0b83a-187">g.</span></span> <span data-ttu-id="0b83a-188">選取 [GET] 作為 [登出要求傳送方式]。</span><span class="sxs-lookup"><span data-stu-id="0b83a-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="0b83a-189">在 [hello**自訂屬性對應**區段中，選擇 hello 欄位想 toomap 與 Azure AD 的宣告。</span><span class="sxs-lookup"><span data-stu-id="0b83a-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="0b83a-190">在此範例中，hello **emailaddress** hello 值是對應宣告**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="0b83a-191">它是從 Azure AD 電子郵件宣告 hello 預設宣告的名稱。</span><span class="sxs-lookup"><span data-stu-id="0b83a-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="0b83a-192">使用適當的 hello**使用者識別碼**toomap hello 使用者從 Azure AD tooDocuSign 使用者對應。</span><span class="sxs-lookup"><span data-stu-id="0b83a-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="0b83a-193">選取 hello 適當欄位，然後輸入 hello 取決於您的組織設定適當的值。</span><span class="sxs-lookup"><span data-stu-id="0b83a-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![設定單一登入][57]

13. <span data-ttu-id="0b83a-195">在 [hello**身分識別提供者憑證**區段中，按一下**加入憑證**，然後再上傳您從 Azure AD 入口網站下載的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="0b83a-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![設定單一登入][58]

14. <span data-ttu-id="0b83a-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0b83a-197">Click **Save**.</span></span>

15. <span data-ttu-id="0b83a-198">在 [hello**身分識別提供者**區段中，按一下**動作**，然後按一下 [**端點**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![設定單一登入][59]
 
16. <span data-ttu-id="0b83a-200">在 [hello**檢視 SAML 2.0 端點**區段**DocuSign 管理員入口網站**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0b83a-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![設定單一登入][60]
   
    <span data-ttu-id="0b83a-202">a.</span><span class="sxs-lookup"><span data-stu-id="0b83a-202">a.</span></span> <span data-ttu-id="0b83a-203">複製 hello**服務提供者簽發者 URL**，然後貼入 hello**識別碼**上的文字方塊**DocuSign 網域和 Url** hello Azure 入口網站的下列 hello 區段模式： `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`。</span><span class="sxs-lookup"><span data-stu-id="0b83a-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="0b83a-204">b.</span><span class="sxs-lookup"><span data-stu-id="0b83a-204">b.</span></span> <span data-ttu-id="0b83a-205">複製 hello**服務提供者登入 URL**，然後貼入 hello**登入 URL**上的文字方塊**DocuSign 網域和 Url** hello Azure 入口網站的下列 hello 區段模式： `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`。</span><span class="sxs-lookup"><span data-stu-id="0b83a-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="0b83a-207">c.</span><span class="sxs-lookup"><span data-stu-id="0b83a-207">c.</span></span>  <span data-ttu-id="0b83a-208">按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="0b83a-208">Click **Close**</span></span>
    
17. <span data-ttu-id="0b83a-209">在 [hello Azure 入口網站，按一下 [**儲存**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-209">On hello Azure portal, click **Save**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="0b83a-211">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="0b83a-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0b83a-212">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="0b83a-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0b83a-213">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0b83a-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b83a-214">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0b83a-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b83a-215">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0b83a-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0b83a-217">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0b83a-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b83a-218">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0b83a-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b83a-220">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b83a-222">在 [hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0b83a-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b83a-224">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0b83a-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b83a-226">a.</span><span class="sxs-lookup"><span data-stu-id="0b83a-226">a.</span></span> <span data-ttu-id="0b83a-227">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b83a-228">b.</span><span class="sxs-lookup"><span data-stu-id="0b83a-228">b.</span></span> <span data-ttu-id="0b83a-229">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="0b83a-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b83a-230">c.</span><span class="sxs-lookup"><span data-stu-id="0b83a-230">c.</span></span> <span data-ttu-id="0b83a-231">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0b83a-232">d.</span><span class="sxs-lookup"><span data-stu-id="0b83a-232">d.</span></span> <span data-ttu-id="0b83a-233">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0b83a-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="0b83a-234">建立 DocuSign 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0b83a-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="0b83a-235">應用程式支援**即時使用者佈建恰好**和之後自動建立 hello 應用程式中驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="0b83a-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0b83a-236">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="0b83a-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0b83a-237">在本節中，您可以授與他們存取 tooDocuSign 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0b83a-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![指派使用者][200] 

<span data-ttu-id="0b83a-239">**tooassign 許 Simon tooDocuSign，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0b83a-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="0b83a-240">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0b83a-242">在 [hello] 應用程式清單中，選取**DocuSign**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-242">In hello applications list, select **DocuSign**.</span></span>

    ![設定單一登入](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="0b83a-244">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="0b83a-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0b83a-246">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b83a-246">Click **Add** button.</span></span> <span data-ttu-id="0b83a-247">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0b83a-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0b83a-249">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="0b83a-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0b83a-250">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b83a-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b83a-251">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0b83a-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b83a-252">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0b83a-252">Testing single sign-on</span></span>

<span data-ttu-id="0b83a-253">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="0b83a-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0b83a-254">當您按一下 hello DocuSign 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 DocuSign 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b83a-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="0b83a-255">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="0b83a-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0b83a-256">其他資源</span><span class="sxs-lookup"><span data-stu-id="0b83a-256">Additional resources</span></span>

* [<span data-ttu-id="0b83a-257">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b83a-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b83a-258">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0b83a-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0b83a-259">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="0b83a-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

