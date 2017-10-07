---
title: "教學課程：Azure Active Directory 與 SpringCM 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SpringCM 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="9e1bc-103">教學課程：Azure Active Directory 與 SpringCM 整合</span><span class="sxs-lookup"><span data-stu-id="9e1bc-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="9e1bc-104">在此教學課程中，您學會如何 toointegrate SpringCM 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e1bc-105">與 Azure AD 整合 SpringCM 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="9e1bc-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9e1bc-106">您可以控制存取 tooSpringCM Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="9e1bc-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="9e1bc-107">您可以啟用您的使用者 tooautomatically get 登入 tooSpringCM （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="9e1bc-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e1bc-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9e1bc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9e1bc-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e1bc-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9e1bc-110">Prerequisites</span></span>

<span data-ttu-id="9e1bc-111">tooconfigure 與 SpringCM 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="9e1bc-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="9e1bc-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9e1bc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e1bc-113">啟用 SpringCM 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9e1bc-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e1bc-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e1bc-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9e1bc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e1bc-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e1bc-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e1bc-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9e1bc-118">Scenario description</span></span>
<span data-ttu-id="9e1bc-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e1bc-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="9e1bc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e1bc-121">從 hello 圖庫加入 SpringCM</span><span class="sxs-lookup"><span data-stu-id="9e1bc-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="9e1bc-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9e1bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="9e1bc-123">從 hello 圖庫加入 SpringCM</span><span class="sxs-lookup"><span data-stu-id="9e1bc-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="9e1bc-124">tooconfigure hello 整合 SpringCM 的 Azure AD，您需要 tooadd SpringCM hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9e1bc-125">**tooadd SpringCM 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9e1bc-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e1bc-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9e1bc-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9e1bc-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="9e1bc-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="9e1bc-133">在 [hello] 搜尋方塊中，輸入**SpringCM**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-133">In hello search box, type **SpringCM**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="9e1bc-135">在 hello 結果 窗格中，選取  **SpringCM**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e1bc-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9e1bc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e1bc-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 SpringCM 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9e1bc-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 SpringCM 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="9e1bc-140">換句話說，Azure AD 使用者與 hello SpringCM 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="9e1bc-141">在 SpringCM 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9e1bc-142">tooconfigure 及測試 Azure AD 單一登入 SpringCM，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="9e1bc-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9e1bc-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9e1bc-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e1bc-145">**[建立測試使用者 SpringCM](#creating-a-springcm-test-user)**  -toohave 許 Simon SpringCM 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e1bc-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e1bc-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e1bc-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9e1bc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e1bc-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 SpringCM 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="9e1bc-150">**tooconfigure Azure AD 單一登入 SpringCM，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9e1bc-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e1bc-151">在 Azure 入口網站上 hello hello **SpringCM**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9e1bc-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="9e1bc-155">在 hello **SpringCM 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e1bc-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="9e1bc-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="9e1bc-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9e1bc-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-158">This value is not real.</span></span> <span data-ttu-id="9e1bc-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="9e1bc-160">請連絡[SpringCM 用戶端支援小組](https://knowledge.springcm.com/support)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="9e1bc-161">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Raw)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="9e1bc-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9e1bc-165">在 hello **SpringCM 組態**區段中，按一下**設定 SpringCM** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9e1bc-166">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="9e1bc-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="9e1bc-168">在不同的網頁瀏覽器視窗中，登入 tooyour **SpringCM**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="9e1bc-169">在 hello 最上層顯示 hello 功能表上，按一下**移至**，按一下**喜好設定**，然後在 hello**帳號喜好設定**區段中，按一下**SAML SSO**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="9e1bc-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span><span class="sxs-lookup"><span data-stu-id="9e1bc-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="9e1bc-171">在 hello 身分識別提供者組態 區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e1bc-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="9e1bc-172">![識別提供者組態](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "識別提供者組態")</span><span class="sxs-lookup"><span data-stu-id="9e1bc-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="9e1bc-173">a.</span><span class="sxs-lookup"><span data-stu-id="9e1bc-173">a.</span></span> <span data-ttu-id="9e1bc-174">tooupload 下載的 Azure Active Directory 憑證、 按一下**選取簽發者憑證**或**變更簽發者憑證**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="9e1bc-175">b.</span><span class="sxs-lookup"><span data-stu-id="9e1bc-175">b.</span></span> <span data-ttu-id="9e1bc-176">貼上**SAML 實體識別碼**值，您從 Azure 入口網站複製到 hello**簽發者**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="9e1bc-177">c.</span><span class="sxs-lookup"><span data-stu-id="9e1bc-177">c.</span></span> <span data-ttu-id="9e1bc-178">貼上**SAML 單一登入服務 URL**值，您從 hello Azure 入口網站複製到 hello**服務提供者 (SP) 起始端點**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="9e1bc-179">d.</span><span class="sxs-lookup"><span data-stu-id="9e1bc-179">d.</span></span> <span data-ttu-id="9e1bc-180">針對 [已啟用 SAML] 選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="9e1bc-181">e.</span><span class="sxs-lookup"><span data-stu-id="9e1bc-181">e.</span></span> <span data-ttu-id="9e1bc-182">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="9e1bc-183">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="9e1bc-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9e1bc-184">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9e1bc-185">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e1bc-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e1bc-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9e1bc-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e1bc-187">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="9e1bc-189">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9e1bc-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e1bc-190">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e1bc-192">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e1bc-194">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e1bc-196">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e1bc-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e1bc-198">a.</span><span class="sxs-lookup"><span data-stu-id="9e1bc-198">a.</span></span> <span data-ttu-id="9e1bc-199">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e1bc-200">b.</span><span class="sxs-lookup"><span data-stu-id="9e1bc-200">b.</span></span> <span data-ttu-id="9e1bc-201">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e1bc-202">c.</span><span class="sxs-lookup"><span data-stu-id="9e1bc-202">c.</span></span> <span data-ttu-id="9e1bc-203">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9e1bc-204">d.</span><span class="sxs-lookup"><span data-stu-id="9e1bc-204">d.</span></span> <span data-ttu-id="9e1bc-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="9e1bc-206">建立 SpringCM 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9e1bc-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="9e1bc-207">tooenable Azure Active Directory 使用者 toolog 中 tooSpringCM，它們必須佈建到 SpringCM。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="9e1bc-208">在 SpringCM 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="9e1bc-209">如需詳細資訊，請參閱[建立和編輯 SpringCM 使用者](http://knowledge.springcm.com/create-and-edit-a-springcm-user) (英文)。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="9e1bc-210">**tooprovision 使用者帳戶 tooSpringCM，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9e1bc-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e1bc-211">登入 tooyour **SpringCM**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="9e1bc-212">按一下 移至，然後按一下通訊錄。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="9e1bc-213">![建立使用者](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="9e1bc-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="9e1bc-214">按一下 [建立使用者] 。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-214">Click **Create User**.</span></span>

4. <span data-ttu-id="9e1bc-215">選取 [使用者角色] 。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="9e1bc-216">選取 [傳送啟用電子郵件] 。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="9e1bc-217">型別 hello 名字、 姓氏和電子郵件地址想成 hello tooprovision 之有效 Azure Active Directory 使用者帳戶相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="9e1bc-218">新增 hello 使用者 tooa**安全性群組**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="9e1bc-219">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="9e1bc-220">您可以使用任何其他 SpringCM 使用者帳戶建立工具或 Api 提供 SpringCM tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9e1bc-221">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="9e1bc-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9e1bc-222">在本節中，您可以授與存取 tooSpringCM 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![指派使用者][200] 

<span data-ttu-id="9e1bc-224">**tooassign 許 Simon tooSpringCM，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9e1bc-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="9e1bc-225">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9e1bc-227">在 [hello] 應用程式清單中，選取**SpringCM**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-227">In hello applications list, select **SpringCM**.</span></span>

    ![設定單一登入](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="9e1bc-229">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="9e1bc-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-231">Click **Add** button.</span></span> <span data-ttu-id="9e1bc-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="9e1bc-234">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9e1bc-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e1bc-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e1bc-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9e1bc-237">Testing single sign-on</span></span>

<span data-ttu-id="9e1bc-238">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="9e1bc-239">當您按一下 hello SpringCM 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 SpringCM 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="9e1bc-240">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="9e1bc-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9e1bc-241">其他資源</span><span class="sxs-lookup"><span data-stu-id="9e1bc-241">Additional resources</span></span>

* [<span data-ttu-id="9e1bc-242">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e1bc-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e1bc-243">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9e1bc-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

