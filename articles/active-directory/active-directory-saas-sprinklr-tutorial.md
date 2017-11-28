---
title: "教學課程：Azure Active Directory 與 Sprinklr 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Sprinklr 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a><span data-ttu-id="a43b7-103">教學課程：Azure Active Directory 與 Sprinklr 整合</span><span class="sxs-lookup"><span data-stu-id="a43b7-103">Tutorial: Azure Active Directory integration with Sprinklr</span></span>

<span data-ttu-id="a43b7-104">在此教學課程中，您學會如何 toointegrate Sprinklr 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a43b7-104">In this tutorial, you learn how toointegrate Sprinklr with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a43b7-105">整合 Azure AD 與 Sprinklr 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a43b7-105">Integrating Sprinklr with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a43b7-106">您可以控制存取 tooSprinklr Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="a43b7-106">You can control in Azure AD who has access tooSprinklr</span></span>
- <span data-ttu-id="a43b7-107">您可以啟用您的使用者 tooautomatically get 登入 tooSprinklr （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a43b7-107">You can enable your users tooautomatically get signed-on tooSprinklr (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a43b7-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a43b7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a43b7-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a43b7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a43b7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a43b7-110">Prerequisites</span></span>

<span data-ttu-id="a43b7-111">tooconfigure Azure AD 與 Sprinklr 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a43b7-111">tooconfigure Azure AD integration with Sprinklr, you need hello following items:</span></span>

- <span data-ttu-id="a43b7-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a43b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a43b7-113">已啟用 Sprinklr 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a43b7-113">A Sprinklr single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a43b7-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a43b7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a43b7-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a43b7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a43b7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a43b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a43b7-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a43b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a43b7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a43b7-118">Scenario description</span></span>
<span data-ttu-id="a43b7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a43b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a43b7-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a43b7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a43b7-121">從 hello 圖庫加入 Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a43b7-121">Adding Sprinklr from hello gallery</span></span>
2. <span data-ttu-id="a43b7-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a43b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sprinklr-from-hello-gallery"></a><span data-ttu-id="a43b7-123">從 hello 圖庫加入 Sprinklr</span><span class="sxs-lookup"><span data-stu-id="a43b7-123">Adding Sprinklr from hello gallery</span></span>
<span data-ttu-id="a43b7-124">tooconfigure hello 整合 Sprinklr 的 Azure AD，您需要 tooadd Sprinklr hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a43b7-124">tooconfigure hello integration of Sprinklr into Azure AD, you need tooadd Sprinklr from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a43b7-125">**tooadd Sprinklr 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a43b7-125">**tooadd Sprinklr from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a43b7-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a43b7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a43b7-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a43b7-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a43b7-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a43b7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a43b7-133">在 [hello] 搜尋方塊中，輸入**Sprinklr**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-133">In hello search box, type **Sprinklr**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. <span data-ttu-id="a43b7-135">在 hello 結果 窗格中，選取  **Sprinklr**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a43b7-135">In hello results panel, select **Sprinklr**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a43b7-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a43b7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a43b7-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Sprinklr 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a43b7-138">In this section, you configure and test Azure AD single sign-on with Sprinklr based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a43b7-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Sprinklr 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a43b7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sprinklr is tooa user in Azure AD.</span></span> <span data-ttu-id="a43b7-140">換句話說，Azure AD 使用者與 Sprinklr 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a43b7-140">In other words, a link relationship between an Azure AD user and hello related user in Sprinklr needs toobe established.</span></span>

<span data-ttu-id="a43b7-141">在 Sprinklr，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a43b7-141">In Sprinklr, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a43b7-142">tooconfigure 及 Azure AD 單一登入與 Sprinklr 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a43b7-142">tooconfigure and test Azure AD single sign-on with Sprinklr, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a43b7-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a43b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a43b7-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a43b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a43b7-145">**[建立測試使用者 Sprinklr](#creating-a-sprinklr-test-user)**  -toohave 許 Simon Sprinklr 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a43b7-145">**[Creating a Sprinklr test user](#creating-a-sprinklr-test-user)** - toohave a counterpart of Britta Simon in Sprinklr that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a43b7-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a43b7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a43b7-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a43b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a43b7-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a43b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a43b7-149">在本節中，您要啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Sprinklr 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="a43b7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sprinklr application.</span></span>

<span data-ttu-id="a43b7-150">**tooconfigure Azure AD 單一登入與 Sprinklr，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a43b7-150">**tooconfigure Azure AD single sign-on with Sprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="a43b7-151">在 Azure 入口網站上 hello hello **Sprinklr**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-151">In hello Azure portal, on hello **Sprinklr** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a43b7-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a43b7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. <span data-ttu-id="a43b7-155">在 hello **Sprinklr 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a43b7-155">On hello **Sprinklr Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    <span data-ttu-id="a43b7-157">a.</span><span class="sxs-lookup"><span data-stu-id="a43b7-157">a.</span></span> <span data-ttu-id="a43b7-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="a43b7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    <span data-ttu-id="a43b7-159">b.</span><span class="sxs-lookup"><span data-stu-id="a43b7-159">b.</span></span> <span data-ttu-id="a43b7-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.sprinklr.com`</span><span class="sxs-lookup"><span data-stu-id="a43b7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sprinklr.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a43b7-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a43b7-161">These values are not real.</span></span> <span data-ttu-id="a43b7-162">更新 hello 值 hello 與實際的登入 URL 和識別碼。</span><span class="sxs-lookup"><span data-stu-id="a43b7-162">Update hello value with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a43b7-163">請連絡[Sprinklr 用戶端支援小組](https://www.sprinklr.com/contact-us/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="a43b7-163">Contact [Sprinklr Client support team](https://www.sprinklr.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a43b7-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="a43b7-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. <span data-ttu-id="a43b7-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a43b7-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a43b7-168">在 hello **Sprinklr 組態**區段中，按一下**設定 Sprinklr** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="a43b7-168">On hello **Sprinklr Configuration** section, click **Configure Sprinklr** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a43b7-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="a43b7-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

7. <span data-ttu-id="a43b7-170">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Sprinklr 公司網站。</span><span class="sxs-lookup"><span data-stu-id="a43b7-170">In a different web browser window, log in tooyour Sprinklr company site as an administrator.</span></span>

8. <span data-ttu-id="a43b7-171">跳過**管理\>設定**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-171">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a43b7-172">![管理](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "管理")</span><span class="sxs-lookup"><span data-stu-id="a43b7-172">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

9. <span data-ttu-id="a43b7-173">跳過**管理夥伴\>Single Sign**上從 hello 左窗格。</span><span class="sxs-lookup"><span data-stu-id="a43b7-173">Go too**Manage Partner \> Single Sign** on from hello left pane.</span></span>
   
    <span data-ttu-id="a43b7-174">![管理夥伴](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "管理夥伴")</span><span class="sxs-lookup"><span data-stu-id="a43b7-174">![Manage Partner](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Manage Partner")</span></span>

10. <span data-ttu-id="a43b7-175">按一下 [新增單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="a43b7-175">Click **+Add Single Sign Ons**.</span></span>
   
    <span data-ttu-id="a43b7-176">![單一登入](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="a43b7-176">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Single Sign-Ons")</span></span>

11. <span data-ttu-id="a43b7-177">在 hello**單一登入**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a43b7-177">On hello **Single Sign on** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="a43b7-178">![單一登入](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="a43b7-178">![Single Sign-Ons](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Single Sign-Ons")</span></span>

    <span data-ttu-id="a43b7-179">a.</span><span class="sxs-lookup"><span data-stu-id="a43b7-179">a.</span></span> <span data-ttu-id="a43b7-180">在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： *WAADSSOTest*)。</span><span class="sxs-lookup"><span data-stu-id="a43b7-180">In hello **Name** textbox, type a name for your configuration (for example: *WAADSSOTest*).</span></span>

    <span data-ttu-id="a43b7-181">b.</span><span class="sxs-lookup"><span data-stu-id="a43b7-181">b.</span></span> <span data-ttu-id="a43b7-182">選取 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="a43b7-182">Select **Enabled**.</span></span>

    <span data-ttu-id="a43b7-183">c.</span><span class="sxs-lookup"><span data-stu-id="a43b7-183">c.</span></span> <span data-ttu-id="a43b7-184">選取 [使用新的 SSO 憑證] 。</span><span class="sxs-lookup"><span data-stu-id="a43b7-184">Select **Use new SSO Certificate**.</span></span>
             
    <span data-ttu-id="a43b7-185">e.</span><span class="sxs-lookup"><span data-stu-id="a43b7-185">e.</span></span> <span data-ttu-id="a43b7-186">在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼入 toohello**身分識別提供者憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a43b7-186">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="a43b7-187">f.</span><span class="sxs-lookup"><span data-stu-id="a43b7-187">f.</span></span> <span data-ttu-id="a43b7-188">貼上 hello **SAML 實體識別碼**值，您從 Azure 入口網站複製到 hello**實體識別碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a43b7-188">Paste hello **SAML Entity ID** value which you have copied from Azure Portal into hello **Entity Id** textbox.</span></span>

    <span data-ttu-id="a43b7-189">g.</span><span class="sxs-lookup"><span data-stu-id="a43b7-189">g.</span></span> <span data-ttu-id="a43b7-190">貼上 hello **SAML 單一登入服務 URL**值，您從 Azure 入口網站複製到 hello**身分識別提供者登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a43b7-190">Paste hello **SAML Single Sign-On Service URL** value which you have copied from Azure Portal into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="a43b7-191">h.</span><span class="sxs-lookup"><span data-stu-id="a43b7-191">h.</span></span> <span data-ttu-id="a43b7-192">貼上 hello**登出 URL**值，您從 Azure 入口網站複製到 hello**身分識別提供者登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a43b7-192">Paste hello **Sign-Out URL** value which you have copied from Azure Portal into hello **Identity Provider Logout URL** textbox.</span></span>
     
    <span data-ttu-id="a43b7-193">i.</span><span class="sxs-lookup"><span data-stu-id="a43b7-193">i.</span></span> <span data-ttu-id="a43b7-194">在 [SAML 使用者識別碼類型] 選取 [判斷提示包含使用者的 sprinklr.com 使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="a43b7-194">As **SAML User ID Type**, select **Assertion contains User”s sprinklr.com username**.</span></span>

    <span data-ttu-id="a43b7-195">j.</span><span class="sxs-lookup"><span data-stu-id="a43b7-195">j.</span></span> <span data-ttu-id="a43b7-196">做為**SAML 使用者識別碼位置**，選取**使用者識別碼位於 Subject 陳述式 hello hello 名稱識別碼元素中**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-196">As **SAML User ID Location**, select **User ID is in hello Name Identifier element of hello Subject statement**.</span></span>

    <span data-ttu-id="a43b7-197">k.</span><span class="sxs-lookup"><span data-stu-id="a43b7-197">k.</span></span> <span data-ttu-id="a43b7-198">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a43b7-198">Click **Save**.</span></span>
       
    <span data-ttu-id="a43b7-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="a43b7-199">![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")</span></span>

> [!TIP]
> <span data-ttu-id="a43b7-200">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a43b7-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a43b7-201">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a43b7-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a43b7-202">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a43b7-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a43b7-203">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a43b7-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="a43b7-204">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a43b7-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a43b7-206">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a43b7-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a43b7-207">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a43b7-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a43b7-209">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a43b7-211">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="a43b7-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a43b7-213">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a43b7-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a43b7-215">a.</span><span class="sxs-lookup"><span data-stu-id="a43b7-215">a.</span></span> <span data-ttu-id="a43b7-216">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a43b7-217">b.</span><span class="sxs-lookup"><span data-stu-id="a43b7-217">b.</span></span> <span data-ttu-id="a43b7-218">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="a43b7-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a43b7-219">c.</span><span class="sxs-lookup"><span data-stu-id="a43b7-219">c.</span></span> <span data-ttu-id="a43b7-220">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a43b7-221">d.</span><span class="sxs-lookup"><span data-stu-id="a43b7-221">d.</span></span> <span data-ttu-id="a43b7-222">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a43b7-222">Click **Create**.</span></span>
 
### <a name="creating-a-sprinklr-test-user"></a><span data-ttu-id="a43b7-223">建立 Sprinklr 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a43b7-223">Creating a Sprinklr test user</span></span>

1. <span data-ttu-id="a43b7-224">登入 tooyour Sprinklr 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="a43b7-224">Log in tooyour Sprinklr company site as an administrator.</span></span>

2. <span data-ttu-id="a43b7-225">跳過**管理\>設定**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-225">Go too**Administration \> Settings**.</span></span>
   
    <span data-ttu-id="a43b7-226">![管理](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "管理")</span><span class="sxs-lookup"><span data-stu-id="a43b7-226">![Administration](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Administration")</span></span>

3. <span data-ttu-id="a43b7-227">跳過**管理用戶端\>使用者**hello 左窗格中。</span><span class="sxs-lookup"><span data-stu-id="a43b7-227">Go too**Manage Client \> Users** from hello left pane.</span></span>
   
    <span data-ttu-id="a43b7-228">![設定](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "設定")</span><span class="sxs-lookup"><span data-stu-id="a43b7-228">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Settings")</span></span>

4. <span data-ttu-id="a43b7-229">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="a43b7-229">Click **Add User**.</span></span>
   
    <span data-ttu-id="a43b7-230">![設定](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "設定")</span><span class="sxs-lookup"><span data-stu-id="a43b7-230">![Settings](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Settings")</span></span>

5. <span data-ttu-id="a43b7-231">在 [hello**編輯使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a43b7-231">On hello **Edit user** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="a43b7-232">![編輯使用者](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "編輯使用者")</span><span class="sxs-lookup"><span data-stu-id="a43b7-232">![Edit user](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Edit user")</span></span> 

    <span data-ttu-id="a43b7-233">a.</span><span class="sxs-lookup"><span data-stu-id="a43b7-233">a.</span></span> <span data-ttu-id="a43b7-234">在 hello**電子郵件**，**名字**和**姓氏**想 tooprovision Azure AD 使用者帳戶的型別 hello 資訊的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a43b7-234">In hello **Email**, **First Name** and **Last Name** textboxes, type hello information of an Azure AD user account you want tooprovision.</span></span>

    <span data-ttu-id="a43b7-235">b.</span><span class="sxs-lookup"><span data-stu-id="a43b7-235">b.</span></span> <span data-ttu-id="a43b7-236">選取 [密碼已停用] 。</span><span class="sxs-lookup"><span data-stu-id="a43b7-236">Select **Password Disabled**.</span></span>

    <span data-ttu-id="a43b7-237">c.</span><span class="sxs-lookup"><span data-stu-id="a43b7-237">c.</span></span> <span data-ttu-id="a43b7-238">選取 [語言]。</span><span class="sxs-lookup"><span data-stu-id="a43b7-238">Select **Language**.</span></span>

    <span data-ttu-id="a43b7-239">d.</span><span class="sxs-lookup"><span data-stu-id="a43b7-239">d.</span></span> <span data-ttu-id="a43b7-240">選取 [使用者類型]。</span><span class="sxs-lookup"><span data-stu-id="a43b7-240">Select **User Type**.</span></span>

    <span data-ttu-id="a43b7-241">e.</span><span class="sxs-lookup"><span data-stu-id="a43b7-241">e.</span></span> <span data-ttu-id="a43b7-242">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="a43b7-242">Click **Update**.</span></span>
   
     >[!IMPORTANT]
     ><span data-ttu-id="a43b7-243">**密碼停用**必須是所選的 tooenable 中的使用者 toolog 透過身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="a43b7-243">**Password Disabled** must be selected tooenable a user toolog in via an Identity provider.</span></span> 
     
6. <span data-ttu-id="a43b7-244">跳過**角色**，然後執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a43b7-244">Go too**Role**, and then perform hello following steps:</span></span>
   
    <span data-ttu-id="a43b7-245">![夥伴角色](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "夥伴角色")</span><span class="sxs-lookup"><span data-stu-id="a43b7-245">![Partner Roles](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Partner Roles")</span></span>

    <span data-ttu-id="a43b7-246">a.</span><span class="sxs-lookup"><span data-stu-id="a43b7-246">a.</span></span> <span data-ttu-id="a43b7-247">從 hello **Global**清單中，選取**所有\_權限**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-247">From hello **Global** list, select **ALL\_Permissions**.</span></span>  

    <span data-ttu-id="a43b7-248">b.</span><span class="sxs-lookup"><span data-stu-id="a43b7-248">b.</span></span> <span data-ttu-id="a43b7-249">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="a43b7-249">Click **Update**.</span></span>

>[!NOTE]
><span data-ttu-id="a43b7-250">您可以使用任何其他 Sprinklr 使用者帳戶建立工具或 Api 提供 Sprinklr tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a43b7-250">You can use any other Sprinklr user account creation tools or APIs provided by Sprinklr tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a43b7-251">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a43b7-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a43b7-252">在本節中，您可以授與存取 tooSprinklr 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a43b7-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSprinklr.</span></span>

![指派使用者][200] 

<span data-ttu-id="a43b7-254">**tooassign 許 Simon tooSprinklr，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a43b7-254">**tooassign Britta Simon tooSprinklr, perform hello following steps:**</span></span>

1. <span data-ttu-id="a43b7-255">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a43b7-257">在 [hello] 應用程式清單中，選取**Sprinklr**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-257">In hello applications list, select **Sprinklr**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. <span data-ttu-id="a43b7-259">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a43b7-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a43b7-261">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a43b7-261">Click **Add** button.</span></span> <span data-ttu-id="a43b7-262">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a43b7-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a43b7-264">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a43b7-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a43b7-265">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a43b7-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a43b7-266">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a43b7-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a43b7-267">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a43b7-267">Testing single sign-on</span></span>

<span data-ttu-id="a43b7-268">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a43b7-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a43b7-269">當您按一下 hello Sprinklr 磚 hello 存取面板中的時，您應該取得 Sprinklr 應用程式會自動登入 tooyour hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a43b7-269">When you click hello Sprinklr tile in hello Access Panel, you should get automatically signed-on tooyour Sprinklr application For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a43b7-270">其他資源</span><span class="sxs-lookup"><span data-stu-id="a43b7-270">Additional resources</span></span>

* [<span data-ttu-id="a43b7-271">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a43b7-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a43b7-272">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a43b7-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

