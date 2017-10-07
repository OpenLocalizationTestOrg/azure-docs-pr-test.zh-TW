---
title: "教學課程：Azure Active Directory 與 Expensify 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Expensify 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: 141513ef27c90dae2d77a52ecab2f89c4e5a55ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="a57e0-103">教學課程：Azure Active Directory 與 Expensify 整合</span><span class="sxs-lookup"><span data-stu-id="a57e0-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="a57e0-104">在此教學課程中，您學會如何 toointegrate Expensify 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a57e0-104">In this tutorial, you learn how toointegrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a57e0-105">與 Azure AD 整合 Expensify 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a57e0-105">Integrating Expensify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a57e0-106">您可以控制存取 tooExpensify Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="a57e0-106">You can control in Azure AD who has access tooExpensify</span></span>
- <span data-ttu-id="a57e0-107">您可以啟用您的使用者 tooautomatically get 登入 tooExpensify （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a57e0-107">You can enable your users tooautomatically get signed-on tooExpensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a57e0-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a57e0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a57e0-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a57e0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a57e0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a57e0-110">Prerequisites</span></span>

<span data-ttu-id="a57e0-111">tooconfigure Expensify 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a57e0-111">tooconfigure Azure AD integration with Expensify, you need hello following items:</span></span>

- <span data-ttu-id="a57e0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a57e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a57e0-113">已啟用 Expensify 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a57e0-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a57e0-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a57e0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a57e0-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a57e0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a57e0-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a57e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a57e0-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a57e0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a57e0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a57e0-118">Scenario description</span></span>
<span data-ttu-id="a57e0-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a57e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a57e0-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a57e0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a57e0-121">從 hello 圖庫加入 Expensify</span><span class="sxs-lookup"><span data-stu-id="a57e0-121">Adding Expensify from hello gallery</span></span>
2. <span data-ttu-id="a57e0-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a57e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-hello-gallery"></a><span data-ttu-id="a57e0-123">從 hello 圖庫加入 Expensify</span><span class="sxs-lookup"><span data-stu-id="a57e0-123">Adding Expensify from hello gallery</span></span>
<span data-ttu-id="a57e0-124">tooconfigure hello 整合 Expensify 到 Azure AD，您需要 tooadd Expensify hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a57e0-124">tooconfigure hello integration of Expensify into Azure AD, you need tooadd Expensify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a57e0-125">**tooadd Expensify 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a57e0-125">**tooadd Expensify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a57e0-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a57e0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a57e0-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a57e0-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a57e0-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a57e0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a57e0-133">在 [hello] 搜尋方塊中，輸入**Expensify**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-133">In hello search box, type **Expensify**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="a57e0-135">在 hello 結果 窗格中，選取  **Expensify**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a57e0-135">In hello results panel, select **Expensify**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a57e0-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a57e0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a57e0-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Expensify 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a57e0-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a57e0-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Expensify 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a57e0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Expensify is tooa user in Azure AD.</span></span> <span data-ttu-id="a57e0-140">換句話說，Azure AD 使用者與 hello Expensify 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a57e0-140">In other words, a link relationship between an Azure AD user and hello related user in Expensify needs toobe established.</span></span>

<span data-ttu-id="a57e0-141">Expensify 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a57e0-141">In Expensify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a57e0-142">tooconfigure 及 Expensify 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a57e0-142">tooconfigure and test Azure AD single sign-on with Expensify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a57e0-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a57e0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a57e0-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a57e0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a57e0-145">**[建立測試使用者 Expensify](#creating-an-expensify-test-user)**  -toohave 許 Simon Expensify 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a57e0-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - toohave a counterpart of Britta Simon in Expensify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a57e0-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a57e0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a57e0-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a57e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a57e0-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a57e0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a57e0-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Expensify 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a57e0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="a57e0-150">**tooconfigure Azure AD 單一登入與 Expensify，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a57e0-150">**tooconfigure Azure AD single sign-on with Expensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="a57e0-151">在 Azure 入口網站上 hello hello **Expensify**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-151">In hello Azure portal, on hello **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a57e0-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a57e0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="a57e0-155">在 hello **Expensify 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a57e0-155">On hello **Expensify Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="a57e0-157">a.</span><span class="sxs-lookup"><span data-stu-id="a57e0-157">a.</span></span> <span data-ttu-id="a57e0-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="a57e0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="a57e0-159">b.</span><span class="sxs-lookup"><span data-stu-id="a57e0-159">b.</span></span> <span data-ttu-id="a57e0-160">在 hello**識別項 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="a57e0-160">In hello **Identifier URL** textbox, type a URL using hello following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="a57e0-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a57e0-161">These values are not real.</span></span> <span data-ttu-id="a57e0-162">更新這些值與 hello 實際的登入 URL 和識別項 URL。</span><span class="sxs-lookup"><span data-stu-id="a57e0-162">Update these values with hello actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="a57e0-163">請連絡[Expensify 用戶端支援小組](mailto:help@expensify.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="a57e0-163">Contact [Expensify Client support team](mailto:help@expensify.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="a57e0-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="a57e0-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="a57e0-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a57e0-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a57e0-168">tooenable SSO Expensify 中，您必須先 tooenable**控制**hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="a57e0-168">tooenable SSO in Expensify, you first need tooenable **Domain Control** in hello application.</span></span> <span data-ttu-id="a57e0-169">您可以在透過所列的 hello 步驟 hello 應用程式中啟用網域控制[這裡](http://help.expensify.com/domain-control)。</span><span class="sxs-lookup"><span data-stu-id="a57e0-169">You can enable Domain Control in hello application through hello steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="a57e0-170">如需其他支援，請與 [Expensify 用戶端支援小組](mailto:help@expensify.com)合作。</span><span class="sxs-lookup"><span data-stu-id="a57e0-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="a57e0-171">一旦啟用了 [網域控制]，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a57e0-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="a57e0-173">a.</span><span class="sxs-lookup"><span data-stu-id="a57e0-173">a.</span></span> <span data-ttu-id="a57e0-174">登入 tooyour Expensify 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a57e0-174">Sign on tooyour Expensify application.</span></span>
    
    <span data-ttu-id="a57e0-175">b.</span><span class="sxs-lookup"><span data-stu-id="a57e0-175">b.</span></span> <span data-ttu-id="a57e0-176">在 hello hello 上方的工具列中按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-176">In hello toolbar on hello top, click **Admin**.</span></span>
    
    <span data-ttu-id="a57e0-177">c.</span><span class="sxs-lookup"><span data-stu-id="a57e0-177">c.</span></span> <span data-ttu-id="a57e0-178">在 hello 左面板中，按一下 **網域**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-178">In hello left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="a57e0-179">d.</span><span class="sxs-lookup"><span data-stu-id="a57e0-179">d.</span></span> <span data-ttu-id="a57e0-180">按一下已驗證的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="a57e0-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="a57e0-181">e.</span><span class="sxs-lookup"><span data-stu-id="a57e0-181">e.</span></span> <span data-ttu-id="a57e0-182">在 hello 左面板中，按一下  **SAML**，然後選取**啟用**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-182">In hello left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="a57e0-183">f.</span><span class="sxs-lookup"><span data-stu-id="a57e0-183">f.</span></span> <span data-ttu-id="a57e0-184">開啟 hello 下載同盟中繼資料從 Azure AD 在記事本中，複製 hello 內容，並貼到 hello**身分識別提供者中繼資料**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a57e0-184">Open hello downloaded Federation Metadata from Azure AD in notepad, copy hello content, and then paste it into hello **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="a57e0-185">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a57e0-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a57e0-186">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a57e0-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a57e0-187">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a57e0-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a57e0-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a57e0-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="a57e0-189">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a57e0-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a57e0-191">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a57e0-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a57e0-192">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a57e0-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a57e0-194">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a57e0-196">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="a57e0-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a57e0-198">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a57e0-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a57e0-200">a.</span><span class="sxs-lookup"><span data-stu-id="a57e0-200">a.</span></span> <span data-ttu-id="a57e0-201">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a57e0-202">b.</span><span class="sxs-lookup"><span data-stu-id="a57e0-202">b.</span></span> <span data-ttu-id="a57e0-203">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="a57e0-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a57e0-204">c.</span><span class="sxs-lookup"><span data-stu-id="a57e0-204">c.</span></span> <span data-ttu-id="a57e0-205">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a57e0-206">d.</span><span class="sxs-lookup"><span data-stu-id="a57e0-206">d.</span></span> <span data-ttu-id="a57e0-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a57e0-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="a57e0-208">建立 Expensify 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a57e0-208">Creating an Expensify test user</span></span>

<span data-ttu-id="a57e0-209">在本節中，您會在 Expensify 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a57e0-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="a57e0-210">使用[Expensify 用戶端支援小組](mailto:help@expensify.com)tooadd hello hello Expensify 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="a57e0-210">Work with [Expensify Client support team](mailto:help@expensify.com) tooadd hello users in hello Expensify platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a57e0-211">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a57e0-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a57e0-212">在本節中，您可以授與存取 tooExpensify 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a57e0-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooExpensify.</span></span>

![指派使用者][200] 

<span data-ttu-id="a57e0-214">**tooassign 許 Simon tooExpensify，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a57e0-214">**tooassign Britta Simon tooExpensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="a57e0-215">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a57e0-217">在 [hello] 應用程式清單中，選取**Expensify**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-217">In hello applications list, select **Expensify**.</span></span>

    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="a57e0-219">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a57e0-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a57e0-221">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a57e0-221">Click **Add** button.</span></span> <span data-ttu-id="a57e0-222">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a57e0-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a57e0-224">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a57e0-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a57e0-225">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a57e0-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a57e0-226">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a57e0-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a57e0-227">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a57e0-227">Testing single sign-on</span></span>

<span data-ttu-id="a57e0-228">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a57e0-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="a57e0-229">當您按一下 hello Expensify 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Expensify 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a57e0-229">When you click hello Expensify tile in hello Access Panel, you should get automatically signed-on tooyour Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a57e0-230">其他資源</span><span class="sxs-lookup"><span data-stu-id="a57e0-230">Additional resources</span></span>

* [<span data-ttu-id="a57e0-231">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a57e0-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a57e0-232">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a57e0-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

