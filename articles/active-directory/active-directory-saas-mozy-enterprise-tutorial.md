---
title: "教學課程：Azure Active Directory 與 Mozy Enterprise 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Mozy Enterprise 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="55245-103">教學課程：Azure Active Directory 與 Mozy Enterprise 整合</span><span class="sxs-lookup"><span data-stu-id="55245-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="55245-104">在此教學課程中，您學會如何 toointegrate Mozy Enterprise 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="55245-104">In this tutorial, you learn how toointegrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55245-105">整合 Azure AD 與 Mozy Enterprise 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="55245-105">Integrating Mozy Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="55245-106">您可以控制存取 tooMozy Enterprise 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="55245-106">You can control in Azure AD who has access tooMozy Enterprise</span></span>
- <span data-ttu-id="55245-107">您可以啟用您的使用者 tooautomatically get 登入 tooMozy （單一登入） 的企業使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="55245-107">You can enable your users tooautomatically get signed-on tooMozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55245-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="55245-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="55245-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="55245-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55245-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="55245-110">Prerequisites</span></span>

<span data-ttu-id="55245-111">tooconfigure Azure AD 與 Mozy Enterprise 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="55245-111">tooconfigure Azure AD integration with Mozy Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="55245-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="55245-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55245-113">已啟用 Mozy Enterprise 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="55245-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55245-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="55245-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55245-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="55245-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55245-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="55245-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55245-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="55245-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55245-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="55245-118">Scenario description</span></span>
<span data-ttu-id="55245-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55245-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55245-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="55245-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55245-121">從 hello 圖庫加入 Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="55245-121">Adding Mozy Enterprise from hello gallery</span></span>
2. <span data-ttu-id="55245-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="55245-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-hello-gallery"></a><span data-ttu-id="55245-123">從 hello 圖庫加入 Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="55245-123">Adding Mozy Enterprise from hello gallery</span></span>
<span data-ttu-id="55245-124">tooconfigure hello 整合 Mozy Enterprise 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Mozy Enterprise。</span><span class="sxs-lookup"><span data-stu-id="55245-124">tooconfigure hello integration of Mozy Enterprise into Azure AD, you need tooadd Mozy Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="55245-125">**tooadd Mozy Enterprise 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="55245-125">**tooadd Mozy Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="55245-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="55245-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="55245-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="55245-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="55245-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="55245-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="55245-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="55245-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="55245-133">在 [hello] 搜尋方塊中，輸入**Mozy Enterprise**。</span><span class="sxs-lookup"><span data-stu-id="55245-133">In hello search box, type **Mozy Enterprise**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="55245-135">在 hello 結果 窗格中，選取  **Mozy Enterprise**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55245-135">In hello results panel, select **Mozy Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="55245-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="55245-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="55245-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Mozy Enterprise 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55245-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55245-139">單一登入 toowork，Azure AD 需要 tooknow Mozy Enterprise 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="55245-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mozy Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="55245-140">換句話說，Azure AD 使用者與 Mozy Enterprise 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="55245-140">In other words, a link relationship between an Azure AD user and hello related user in Mozy Enterprise needs toobe established.</span></span>

<span data-ttu-id="55245-141">在 Mozy Enterprise 中，指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="55245-141">In Mozy Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="55245-142">tooconfigure 及 Azure AD 單一登入與 Mozy Enterprise 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="55245-142">tooconfigure and test Azure AD single sign-on with Mozy Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="55245-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="55245-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="55245-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="55245-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55245-145">**[建立 Mozy Enterprise 的測試使用者](#creating-a-mozy-enterprise-test-user)** -toohave 許 Simon Mozy Enterprise 是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="55245-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - toohave a counterpart of Britta Simon in Mozy Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="55245-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55245-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55245-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="55245-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="55245-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="55245-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="55245-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Mozy Enterprise 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="55245-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="55245-150">**tooconfigure Azure AD 單一登入與 Mozy Enterprise，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="55245-150">**tooconfigure Azure AD single sign-on with Mozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="55245-151">在 Azure 入口網站上 hello hello **Mozy Enterprise**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="55245-151">In hello Azure portal, on hello **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="55245-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55245-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="55245-155">在 hello **Mozy Enterprise 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="55245-155">On hello **Mozy Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="55245-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="55245-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55245-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="55245-158">This value is not real.</span></span> <span data-ttu-id="55245-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="55245-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="55245-160">請連絡[Mozy Enterprise 的用戶端支援小組](http://support.mozy.com/)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="55245-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) tooget this value.</span></span>

4. <span data-ttu-id="55245-161">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="55245-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="55245-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="55245-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="55245-165">在 hello **Mozy Enterprise 設定**區段中，按一下**設定 Mozy Enterprise** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="55245-165">On hello **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="55245-166">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="55245-166">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="55245-168">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Mozy Enterprise 公司網站。</span><span class="sxs-lookup"><span data-stu-id="55245-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="55245-169">在 hello**組態**區段中，按一下**驗證原則**。</span><span class="sxs-lookup"><span data-stu-id="55245-169">In hello **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="55245-170">![驗證原則](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "驗證原則")</span><span class="sxs-lookup"><span data-stu-id="55245-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="55245-171">在 hello**驗證原則**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="55245-171">On hello **Authentication Policy** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="55245-172">![驗證原則](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "驗證原則")</span><span class="sxs-lookup"><span data-stu-id="55245-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="55245-173">a.</span><span class="sxs-lookup"><span data-stu-id="55245-173">a.</span></span> <span data-ttu-id="55245-174">選取 [目錄服務] 做為**提供者**。</span><span class="sxs-lookup"><span data-stu-id="55245-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="55245-175">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="55245-175">b.</span></span> <span data-ttu-id="55245-176">選取 [使用 LDAP 推送] 。</span><span class="sxs-lookup"><span data-stu-id="55245-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="55245-177">c.</span><span class="sxs-lookup"><span data-stu-id="55245-177">c.</span></span> <span data-ttu-id="55245-178">按一下 hello **SAML 驗證** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="55245-178">Click hello **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="55245-179">d.</span><span class="sxs-lookup"><span data-stu-id="55245-179">d.</span></span> <span data-ttu-id="55245-180">貼上**SAML 單一登入服務 URL**，其中您從 hello Azure 入口網站複製到 hello**驗證 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="55245-180">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="55245-181">e.</span><span class="sxs-lookup"><span data-stu-id="55245-181">e.</span></span> <span data-ttu-id="55245-182">貼上**SAML 實體識別碼**，其中您從 hello Azure 入口網站複製到 hello **SAML 端點**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="55245-182">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="55245-183">f.</span><span class="sxs-lookup"><span data-stu-id="55245-183">f.</span></span> <span data-ttu-id="55245-184">在 [記事本]，複製到剪貼簿，其內容的 hello 中開啟您已下載的 base-64 編碼的憑證，然後貼上 hello 整個憑證**SAML 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="55245-184">Open your downloaded base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="55245-185">g.</span><span class="sxs-lookup"><span data-stu-id="55245-185">g.</span></span> <span data-ttu-id="55245-186">選取**啟用 SSO 供系統管理員使用其網路認證的 toolog**。</span><span class="sxs-lookup"><span data-stu-id="55245-186">Select **Enable SSO for Admins toolog in with their network credentials**.</span></span>
   
   <span data-ttu-id="55245-187">h.</span><span class="sxs-lookup"><span data-stu-id="55245-187">h.</span></span> <span data-ttu-id="55245-188">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="55245-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="55245-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="55245-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="55245-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="55245-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="55245-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55245-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="55245-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="55245-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="55245-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="55245-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="55245-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="55245-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="55245-196">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="55245-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="55245-198">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="55245-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="55245-200">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="55245-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="55245-202">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="55245-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="55245-204">a.</span><span class="sxs-lookup"><span data-stu-id="55245-204">a.</span></span> <span data-ttu-id="55245-205">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="55245-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55245-206">b.</span><span class="sxs-lookup"><span data-stu-id="55245-206">b.</span></span> <span data-ttu-id="55245-207">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="55245-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55245-208">c.</span><span class="sxs-lookup"><span data-stu-id="55245-208">c.</span></span> <span data-ttu-id="55245-209">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="55245-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="55245-210">d.</span><span class="sxs-lookup"><span data-stu-id="55245-210">d.</span></span> <span data-ttu-id="55245-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="55245-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="55245-212">建立 Mozy Enterprise 測試使用者</span><span class="sxs-lookup"><span data-stu-id="55245-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="55245-213">在訂單 tooenable Azure AD 使用者 toolog 到 Mozy Enterprise，它們必須佈建到 Mozy Enterprise。</span><span class="sxs-lookup"><span data-stu-id="55245-213">In order tooenable Azure AD users toolog into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="55245-214">在 Mozy Enterprise 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="55245-214">In hello case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="55245-215">您可以使用任何其他 Mozy Enterprise 使用者帳戶建立工具或 Api 提供 Mozy Enterprise tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="55245-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise tooprovision AAD user accounts.</span></span>

<span data-ttu-id="55245-216">**tooprovision 使用者帳戶，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="55245-216">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="55245-217">登入 tooyour **Mozy Enterprise**租用戶。</span><span class="sxs-lookup"><span data-stu-id="55245-217">Log in tooyour **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="55245-218">按一下 使用者，然後按一下新增使用者。</span><span class="sxs-lookup"><span data-stu-id="55245-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="55245-219">![使用者](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="55245-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="55245-220">hello**新增使用者**選項只會顯示只有當**Mozy**當做 hello 提供者下**驗證原則**。</span><span class="sxs-lookup"><span data-stu-id="55245-220">hello **Add New User** option is only displayed only if **Mozy** is selected as hello provider under **Authentication policy**.</span></span> <span data-ttu-id="55245-221">如果 SAML 驗證設定，然後 hello 使用者會自動加入其第一個登透過單一登入上。</span><span class="sxs-lookup"><span data-stu-id="55245-221">If SAML Authentication is configured, then hello users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="55245-222">Hello 新使用者在對話方塊上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="55245-222">On hello new user dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="55245-223">![新增使用者](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="55245-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="55245-224">a.</span><span class="sxs-lookup"><span data-stu-id="55245-224">a.</span></span> <span data-ttu-id="55245-225">從 hello**選擇群組**清單中，選取群組。</span><span class="sxs-lookup"><span data-stu-id="55245-225">From hello **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="55245-226">b.</span><span class="sxs-lookup"><span data-stu-id="55245-226">b.</span></span> <span data-ttu-id="55245-227">從 hello**的使用者類型**清單中，選取類型。</span><span class="sxs-lookup"><span data-stu-id="55245-227">From hello **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="55245-228">c.</span><span class="sxs-lookup"><span data-stu-id="55245-228">c.</span></span> <span data-ttu-id="55245-229">在 hello **Username**文字方塊中，型別 hello hello Azure AD 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="55245-229">In hello **Username** textbox, type hello name of hello Azure AD user.</span></span>
   
   <span data-ttu-id="55245-230">d.</span><span class="sxs-lookup"><span data-stu-id="55245-230">d.</span></span> <span data-ttu-id="55245-231">在 [hello**電子郵件**hello Azure AD 使用者輸入 hello 電子郵件地址] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="55245-231">In hello **Email** textbox, type hello email address of hello Azure AD user.</span></span>
   
   <span data-ttu-id="55245-232">e.</span><span class="sxs-lookup"><span data-stu-id="55245-232">e.</span></span> <span data-ttu-id="55245-233">選取 [傳送使用者指示電子郵件] 。</span><span class="sxs-lookup"><span data-stu-id="55245-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="55245-234">f.</span><span class="sxs-lookup"><span data-stu-id="55245-234">f.</span></span> <span data-ttu-id="55245-235">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="55245-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="55245-236">建立 hello 使用者之後, 一封電子郵件將傳送 toohello 包含連結 tooconfirm hello 帳戶之前它會變成作用中的 Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="55245-236">After creating hello user, an email will be sent toohello Azure AD user that includes a link tooconfirm hello account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="55245-237">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="55245-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="55245-238">在本節中，您可以授與存取 tooMozy 企業啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55245-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMozy Enterprise.</span></span>

![指派使用者][200] 

<span data-ttu-id="55245-240">**tooassign 許 Simon tooMozy 企業中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="55245-240">**tooassign Britta Simon tooMozy Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="55245-241">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="55245-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="55245-243">在 [hello] 應用程式清單中，選取**Mozy Enterprise**。</span><span class="sxs-lookup"><span data-stu-id="55245-243">In hello applications list, select **Mozy Enterprise**.</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="55245-245">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="55245-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="55245-247">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55245-247">Click **Add** button.</span></span> <span data-ttu-id="55245-248">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="55245-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="55245-250">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="55245-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="55245-251">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55245-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55245-252">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55245-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="55245-253">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="55245-253">Testing single sign-on</span></span>

<span data-ttu-id="55245-254">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="55245-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="55245-255">當您按一下的 hello Mozy Enterprise 磚 hello 存取面板中時，您應該取得 Mozy Enterprise 的應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="55245-255">When you click hello Mozy Enterprise tile in hello Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="55245-256">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="55245-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55245-257">其他資源</span><span class="sxs-lookup"><span data-stu-id="55245-257">Additional resources</span></span>

* [<span data-ttu-id="55245-258">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55245-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55245-259">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="55245-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

