---
title: "教學課程：Azure Active Directory 與 Syncplicity 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Syncplicity 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="76086-103">教學課程：Azure Active Directory 與 Syncplicity 整合</span><span class="sxs-lookup"><span data-stu-id="76086-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="76086-104">在此教學課程中，您學會如何 toointegrate Syncplicity 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="76086-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76086-105">整合 Azure AD 與 Syncplicity 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="76086-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="76086-106">您可以控制存取 tooSyncplicity Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="76086-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="76086-107">您可以啟用您的使用者 tooautomatically get 登入 tooSyncplicity （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="76086-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="76086-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="76086-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="76086-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="76086-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76086-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="76086-110">Prerequisites</span></span>

<span data-ttu-id="76086-111">tooconfigure Azure AD 與 Syncplicity 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="76086-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="76086-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="76086-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76086-113">已啟用 Syncplicity 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="76086-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76086-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="76086-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="76086-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="76086-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76086-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="76086-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="76086-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="76086-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76086-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="76086-118">Scenario description</span></span>
<span data-ttu-id="76086-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76086-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76086-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="76086-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76086-121">從 hello 圖庫加入 Syncplicity</span><span class="sxs-lookup"><span data-stu-id="76086-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="76086-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="76086-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="76086-123">從 hello 圖庫加入 Syncplicity</span><span class="sxs-lookup"><span data-stu-id="76086-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="76086-124">tooconfigure hello 整合 Syncplicity 到 Azure AD，您需要 tooadd Syncplicity hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="76086-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="76086-125">**tooadd Syncplicity 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="76086-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="76086-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="76086-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="76086-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="76086-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="76086-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="76086-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="76086-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="76086-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="76086-133">在 [hello] 搜尋方塊中，輸入**Syncplicity**。</span><span class="sxs-lookup"><span data-stu-id="76086-133">In hello search box, type **Syncplicity**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="76086-135">在 hello 結果 窗格中，選取  **Syncplicity**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="76086-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="76086-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="76086-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="76086-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Syncplicity 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76086-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="76086-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Syncplicity 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="76086-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="76086-140">換句話說，Azure AD 使用者與 Syncplicity 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="76086-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="76086-141">在 Syncplicity，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="76086-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="76086-142">tooconfigure 及 Azure AD 單一登入與 Syncplicity 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="76086-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="76086-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="76086-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="76086-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="76086-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76086-145">**[建立測試使用者 Syncplicity](#creating-a-syncplicity-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Syncplicity 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="76086-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="76086-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76086-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76086-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="76086-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="76086-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="76086-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="76086-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Syncplicity 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="76086-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="76086-150">**tooconfigure Azure AD 單一登入與 Syncplicity，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="76086-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="76086-151">在 Azure 入口網站上 hello hello **Syncplicity**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="76086-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="76086-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76086-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="76086-155">在 hello **Syncplicity 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="76086-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="76086-157">a.</span><span class="sxs-lookup"><span data-stu-id="76086-157">a.</span></span> <span data-ttu-id="76086-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="76086-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="76086-159">b.</span><span class="sxs-lookup"><span data-stu-id="76086-159">b.</span></span> <span data-ttu-id="76086-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="76086-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="76086-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="76086-161">These values are not real.</span></span> <span data-ttu-id="76086-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="76086-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="76086-163">請連絡[Syncplicity 用戶端支援小組](https://www.syncplicity.com/contact-us)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="76086-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="76086-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="76086-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="76086-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="76086-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="76086-168">在 hello **Syncplicity 組態**區段中，按一下**設定 Syncplicity** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="76086-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="76086-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="76086-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="76086-171">登入 tooyour **Syncplicity**租用戶。</span><span class="sxs-lookup"><span data-stu-id="76086-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="76086-172">在 hello 最上層顯示 hello 功能表上，按一下**admin**，選取**設定**，然後按一下**自訂網域和單一登入**。</span><span class="sxs-lookup"><span data-stu-id="76086-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="76086-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="76086-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="76086-174">在 hello**單一登入 (SSO)**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="76086-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="76086-175">![單一登入 \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="76086-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="76086-176">a.</span><span class="sxs-lookup"><span data-stu-id="76086-176">a.</span></span> <span data-ttu-id="76086-177">在 hello**自訂網域**文字方塊中，您的網域類型 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="76086-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="76086-178">b.</span><span class="sxs-lookup"><span data-stu-id="76086-178">b.</span></span> <span data-ttu-id="76086-179">在 [單一登入狀態] 中選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="76086-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="76086-180">c.</span><span class="sxs-lookup"><span data-stu-id="76086-180">c.</span></span> <span data-ttu-id="76086-181">在 hello**實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="76086-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="76086-182">d.</span><span class="sxs-lookup"><span data-stu-id="76086-182">d.</span></span> <span data-ttu-id="76086-183">在 hello**登入頁面 URL**文字方塊中，貼上 hello **SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="76086-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="76086-184">e.</span><span class="sxs-lookup"><span data-stu-id="76086-184">e.</span></span> <span data-ttu-id="76086-185">在 hello**登出頁面 URL**文字方塊中，貼上 hello**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="76086-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="76086-186">f.</span><span class="sxs-lookup"><span data-stu-id="76086-186">f.</span></span> <span data-ttu-id="76086-187">在**身分識別提供者憑證**，按一下 **選擇檔案**，然後再上傳您從 hello Azure 入口網站下載 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="76086-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="76086-188">g.</span><span class="sxs-lookup"><span data-stu-id="76086-188">g.</span></span> <span data-ttu-id="76086-189">按一下 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="76086-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="76086-190">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="76086-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="76086-191">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="76086-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="76086-192">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="76086-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="76086-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="76086-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="76086-194">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="76086-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="76086-196">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="76086-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="76086-197">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="76086-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="76086-199">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="76086-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="76086-201">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="76086-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="76086-203">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="76086-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="76086-205">a.</span><span class="sxs-lookup"><span data-stu-id="76086-205">a.</span></span> <span data-ttu-id="76086-206">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="76086-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76086-207">b.</span><span class="sxs-lookup"><span data-stu-id="76086-207">b.</span></span> <span data-ttu-id="76086-208">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="76086-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="76086-209">c.</span><span class="sxs-lookup"><span data-stu-id="76086-209">c.</span></span> <span data-ttu-id="76086-210">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="76086-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="76086-211">d.</span><span class="sxs-lookup"><span data-stu-id="76086-211">d.</span></span> <span data-ttu-id="76086-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="76086-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="76086-213">建立 Syncplicity 測試使用者</span><span class="sxs-lookup"><span data-stu-id="76086-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="76086-214">AAD 使用者 toobe 無法 toosign 中，它們必須已佈建的 tooSyncplicity 應用程式。</span><span class="sxs-lookup"><span data-stu-id="76086-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="76086-215">本章節描述在 Syncplicity toocreate AAD 使用者帳戶的方式。</span><span class="sxs-lookup"><span data-stu-id="76086-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="76086-216">**tooprovision 使用者帳戶 tooSyncplicity，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="76086-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="76086-217">登入 tooyour **Syncplicity**租用戶 (例如： `https://company.Syncplicity.com`)。</span><span class="sxs-lookup"><span data-stu-id="76086-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="76086-218">按一下 [管理員]，然後選取 [使用者帳戶]。</span><span class="sxs-lookup"><span data-stu-id="76086-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="76086-219">按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="76086-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="76086-220">![管理使用者](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="76086-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="76086-221">型別 hello**經由電子郵件**您想要選取 tooprovision AAD 帳戶的**使用者**做為**角色**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="76086-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="76086-222">![帳戶資訊](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "帳戶資訊")</span><span class="sxs-lookup"><span data-stu-id="76086-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="76086-223">hello AAD 帳戶持有者取得包含連結 tooconfirm 的電子郵件，並啟用 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="76086-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="76086-224">選取要讓新使用者成為成員的公司群組，然後按一下下一步。</span><span class="sxs-lookup"><span data-stu-id="76086-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="76086-225">![群組成員資格](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "群組成員資格")</span><span class="sxs-lookup"><span data-stu-id="76086-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="76086-226">如果未列出群組，請按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="76086-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="76086-227">選取您想要 tooplace hello 使用者的電腦上的 Syncplicity 控制之下，然後按一下 hello 資料夾**下一步**。</span><span class="sxs-lookup"><span data-stu-id="76086-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="76086-228">![Syncplicity 資料夾](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity 資料夾")</span><span class="sxs-lookup"><span data-stu-id="76086-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="76086-229">您可以使用任何其他 Syncplicity 使用者帳戶建立工具或 Api 提供 Syncplicity tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="76086-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="76086-230">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="76086-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="76086-231">在本節中，您可以授與存取 tooSyncplicity 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="76086-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![指派使用者][200] 

<span data-ttu-id="76086-233">**tooassign 許 Simon tooSyncplicity，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="76086-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="76086-234">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="76086-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="76086-236">在 [hello] 應用程式清單中，選取**Syncplicity**。</span><span class="sxs-lookup"><span data-stu-id="76086-236">In hello applications list, select **Syncplicity**.</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="76086-238">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="76086-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="76086-240">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="76086-240">Click **Add** button.</span></span> <span data-ttu-id="76086-241">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="76086-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="76086-243">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="76086-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="76086-244">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="76086-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="76086-245">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="76086-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="76086-246">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="76086-246">Testing single sign-on</span></span>

<span data-ttu-id="76086-247">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="76086-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="76086-248">當您按一下 hello Syncplicity 的圖格 hello 存取面板中時，您應該取得 tooyour 自動登入 Syncplicity 應用程式。</span><span class="sxs-lookup"><span data-stu-id="76086-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="76086-249">其他資源</span><span class="sxs-lookup"><span data-stu-id="76086-249">Additional resources</span></span>

* [<span data-ttu-id="76086-250">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76086-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76086-251">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="76086-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

