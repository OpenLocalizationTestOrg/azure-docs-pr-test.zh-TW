---
title: "教學課程：Azure Active Directory 與 Jobscience 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Jobscience 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="93852-103">教學課程：Azure Active Directory 與 Jobscience 整合</span><span class="sxs-lookup"><span data-stu-id="93852-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="93852-104">在此教學課程中，您學會如何 toointegrate Jobscience 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="93852-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93852-105">整合 Azure AD 與 Jobscience 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="93852-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="93852-106">您可以控制存取 tooJobscience Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="93852-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="93852-107">您可以啟用您的使用者 tooautomatically get 登入 tooJobscience （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="93852-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93852-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="93852-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="93852-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="93852-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93852-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="93852-110">Prerequisites</span></span>

<span data-ttu-id="93852-111">tooconfigure Azure AD 與 Jobscience 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="93852-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="93852-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="93852-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93852-113">啟用 Jobscience 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="93852-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93852-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="93852-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93852-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="93852-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93852-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="93852-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93852-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="93852-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93852-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="93852-118">Scenario description</span></span>
<span data-ttu-id="93852-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="93852-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93852-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="93852-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93852-121">從 hello 圖庫加入 Jobscience</span><span class="sxs-lookup"><span data-stu-id="93852-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="93852-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="93852-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="93852-123">從 hello 圖庫加入 Jobscience</span><span class="sxs-lookup"><span data-stu-id="93852-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="93852-124">tooconfigure hello 整合 Jobscience 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Jobscience。</span><span class="sxs-lookup"><span data-stu-id="93852-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="93852-125">**tooadd Jobscience 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="93852-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="93852-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="93852-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="93852-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="93852-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="93852-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="93852-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="93852-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="93852-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="93852-133">在 [hello] 搜尋方塊中，輸入**Jobscience**。</span><span class="sxs-lookup"><span data-stu-id="93852-133">In hello search box, type **Jobscience**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="93852-135">在 hello 結果 窗格中，選取  **Jobscience**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="93852-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93852-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="93852-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93852-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Jobscience 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="93852-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="93852-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Jobscience 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="93852-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="93852-140">換句話說，Azure AD 使用者與 Jobscience 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="93852-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="93852-141">在 Jobscience 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="93852-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="93852-142">tooconfigure 和測試 Azure AD 單一登入與 Jobscience，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="93852-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="93852-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="93852-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="93852-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="93852-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93852-145">**[建立測試使用者 Jobscience](#creating-a-jobscience-test-user)**  -toohave 許 Simon Jobscience 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="93852-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="93852-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="93852-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93852-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="93852-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93852-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="93852-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93852-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Jobscience 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="93852-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="93852-150">**tooconfigure Azure AD 單一登入 Jobscience 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="93852-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="93852-151">在 Azure 入口網站上 hello hello **Jobscience**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="93852-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="93852-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="93852-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="93852-155">在 hello **Jobscience 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="93852-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="93852-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="93852-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="93852-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="93852-158">This value is not real.</span></span> <span data-ttu-id="93852-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="93852-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="93852-160">取得此值[Jobscience 用戶端支援小組](https://www.jobscience.com/support)或 hello SSO 設定檔從您將建立在 hello 教學課程後面的說明。</span><span class="sxs-lookup"><span data-stu-id="93852-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="93852-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="93852-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="93852-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="93852-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="93852-165">在 hello **Jobscience 組態**區段中，按一下**設定 Jobscience** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="93852-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="93852-166">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="93852-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="93852-168">登入 tooyour Jobscience 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="93852-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="93852-169">跳過**安裝**。</span><span class="sxs-lookup"><span data-stu-id="93852-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="93852-170">![設定](./media/active-directory-saas-jobscience-tutorial/IC784358.png "設定")</span><span class="sxs-lookup"><span data-stu-id="93852-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="93852-171">在 hello 左側瀏覽窗格中，在 hello**管理**區段中，按一下**定義域管理**tooexpand hello 相關的區段，然後按一下**我的網域**tooopen hello **我的網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="93852-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="93852-172">![我的網域](./media/active-directory-saas-jobscience-tutorial/ic767825.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="93852-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="93852-173">tooverify，您的網域是否已正確設定，請確定它是在 「**步驟 4 部署 tooUsers**」，並檢閱您"**我的網域設定**"。</span><span class="sxs-lookup"><span data-stu-id="93852-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="93852-174">![網域部署 tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "網域部署 tooUser")</span><span class="sxs-lookup"><span data-stu-id="93852-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="93852-175">Hello Jobscience 公司網站上，按一下 **安全性控制**，然後按一下**單一登入設定**。</span><span class="sxs-lookup"><span data-stu-id="93852-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="93852-176">![安全性控制項](./media/active-directory-saas-jobscience-tutorial/ic784364.png "安全性控制項")</span><span class="sxs-lookup"><span data-stu-id="93852-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="93852-177">在 hello**單一登入設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="93852-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="93852-178">![單一登入設定](./media/active-directory-saas-jobscience-tutorial/ic781026.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="93852-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="93852-179">a.</span><span class="sxs-lookup"><span data-stu-id="93852-179">a.</span></span> <span data-ttu-id="93852-180">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="93852-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="93852-181">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="93852-181">b.</span></span> <span data-ttu-id="93852-182">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="93852-182">Click **New**.</span></span>

13. <span data-ttu-id="93852-183">在 [hello **SAML 單一登入設定編輯**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="93852-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="93852-184">![SAML 單一登入設定](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML 單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="93852-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="93852-185">a.</span><span class="sxs-lookup"><span data-stu-id="93852-185">a.</span></span> <span data-ttu-id="93852-186">在 hello**名稱**文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="93852-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="93852-187">b.</span><span class="sxs-lookup"><span data-stu-id="93852-187">b.</span></span> <span data-ttu-id="93852-188">在**簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="93852-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="93852-189">c.</span><span class="sxs-lookup"><span data-stu-id="93852-189">c.</span></span> <span data-ttu-id="93852-190">在 hello**實體識別碼**文字方塊中，輸入`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="93852-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="93852-191">d.</span><span class="sxs-lookup"><span data-stu-id="93852-191">d.</span></span> <span data-ttu-id="93852-192">按一下**瀏覽**tooupload 您 Azure AD 的憑證。</span><span class="sxs-lookup"><span data-stu-id="93852-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="93852-193">e.</span><span class="sxs-lookup"><span data-stu-id="93852-193">e.</span></span> <span data-ttu-id="93852-194">做為**SAML 識別類型**，選取**判斷提示包含從 hello 使用者物件的同盟識別碼 hello**。</span><span class="sxs-lookup"><span data-stu-id="93852-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="93852-195">f.</span><span class="sxs-lookup"><span data-stu-id="93852-195">f.</span></span> <span data-ttu-id="93852-196">做為**SAML 識別位置**，選取**身分識別位於 Subject 陳述式 hello hello NameIdentfier 元素**。</span><span class="sxs-lookup"><span data-stu-id="93852-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="93852-197">g.</span><span class="sxs-lookup"><span data-stu-id="93852-197">g.</span></span> <span data-ttu-id="93852-198">在**身分識別提供者登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="93852-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="93852-199">h.</span><span class="sxs-lookup"><span data-stu-id="93852-199">h.</span></span> <span data-ttu-id="93852-200">在**身分識別提供者登出 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="93852-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="93852-201">i.</span><span class="sxs-lookup"><span data-stu-id="93852-201">i.</span></span> <span data-ttu-id="93852-202">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="93852-202">Click **Save**.</span></span>

14. <span data-ttu-id="93852-203">在 hello 左側瀏覽窗格中，在 hello**管理**區段中，按一下**定義域管理**tooexpand hello 相關的區段，然後按一下**我的網域**tooopen hello **我的網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="93852-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="93852-204">![我的網域](./media/active-directory-saas-jobscience-tutorial/ic767825.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="93852-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="93852-205">在 [hello**我的網域**] 頁面的 hello**登入頁面品牌**區段中，按一下**編輯**。</span><span class="sxs-lookup"><span data-stu-id="93852-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="93852-206">![登入頁面商標](./media/active-directory-saas-jobscience-tutorial/ic767826.png "登入頁面商標")</span><span class="sxs-lookup"><span data-stu-id="93852-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="93852-207">在 hello**登入頁面品牌** 頁面的 hello**驗證服務**區段、 hello 名稱您**SAML SSO 設定**隨即出現。</span><span class="sxs-lookup"><span data-stu-id="93852-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="93852-208">請選取該名稱，然後按一下儲存 。</span><span class="sxs-lookup"><span data-stu-id="93852-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="93852-209">![登入頁面商標](./media/active-directory-saas-jobscience-tutorial/ic784366.png "登入頁面商標")</span><span class="sxs-lookup"><span data-stu-id="93852-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="93852-210">tooget hello 預存程序會初始化單一登入 URL，請按一下上 hello**單一登入設定**在 hello**安全性控制**功能表區段。</span><span class="sxs-lookup"><span data-stu-id="93852-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="93852-211">![安全性控制項](./media/active-directory-saas-jobscience-tutorial/ic784368.png "安全性控制項")</span><span class="sxs-lookup"><span data-stu-id="93852-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="93852-212">按一下您已建立 hello 上述步驟中的 hello SSO 設定檔。</span><span class="sxs-lookup"><span data-stu-id="93852-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="93852-213">此頁面會顯示 hello 單一登入 URL 公司 (例如， [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid)。</span><span class="sxs-lookup"><span data-stu-id="93852-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="93852-214">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="93852-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="93852-215">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="93852-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="93852-216">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93852-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93852-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="93852-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="93852-218">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="93852-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="93852-220">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="93852-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="93852-221">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="93852-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93852-223">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="93852-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93852-225">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="93852-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93852-227">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="93852-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93852-229">a.</span><span class="sxs-lookup"><span data-stu-id="93852-229">a.</span></span> <span data-ttu-id="93852-230">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="93852-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93852-231">b.</span><span class="sxs-lookup"><span data-stu-id="93852-231">b.</span></span> <span data-ttu-id="93852-232">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="93852-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93852-233">c.</span><span class="sxs-lookup"><span data-stu-id="93852-233">c.</span></span> <span data-ttu-id="93852-234">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="93852-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="93852-235">d.</span><span class="sxs-lookup"><span data-stu-id="93852-235">d.</span></span> <span data-ttu-id="93852-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="93852-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="93852-237">建立 Jobscience 測試使用者</span><span class="sxs-lookup"><span data-stu-id="93852-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="93852-238">在訂單 tooenable Azure AD 使用者 toolog tooJobscience 中，您必須是佈建到 Jobscience。</span><span class="sxs-lookup"><span data-stu-id="93852-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="93852-239">在 Jobscience 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="93852-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="93852-240">您可以使用任何其他 Jobscience 使用者帳戶建立工具或 Api 提供 Jobscience tooprovision Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="93852-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="93852-241">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="93852-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="93852-242">登入 tooyour **Jobscience**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="93852-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="93852-243">移 tooSetup。</span><span class="sxs-lookup"><span data-stu-id="93852-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="93852-244">![設定](./media/active-directory-saas-jobscience-tutorial/ic784358.png "設定")</span><span class="sxs-lookup"><span data-stu-id="93852-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="93852-245">跳過**管理使用者\>使用者**。</span><span class="sxs-lookup"><span data-stu-id="93852-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="93852-246">![使用者](./media/active-directory-saas-jobscience-tutorial/ic784369.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="93852-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="93852-247">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="93852-247">Click **New User**.</span></span>
   
   <span data-ttu-id="93852-248">![所有使用者](./media/active-directory-saas-jobscience-tutorial/ic784370.png "所有使用者")</span><span class="sxs-lookup"><span data-stu-id="93852-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="93852-249">在 [hello**編輯使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="93852-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="93852-250">![使用者編輯](./media/active-directory-saas-jobscience-tutorial/ic784371.png "使用者編輯")</span><span class="sxs-lookup"><span data-stu-id="93852-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="93852-251">a.</span><span class="sxs-lookup"><span data-stu-id="93852-251">a.</span></span> <span data-ttu-id="93852-252">在 hello**名字**文字方塊中，輸入像許 hello 使用者的名字。</span><span class="sxs-lookup"><span data-stu-id="93852-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="93852-253">b.</span><span class="sxs-lookup"><span data-stu-id="93852-253">b.</span></span> <span data-ttu-id="93852-254">在 hello**姓氏**文字方塊中，輸入像 Simon hello 使用者的姓氏。</span><span class="sxs-lookup"><span data-stu-id="93852-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="93852-255">c.</span><span class="sxs-lookup"><span data-stu-id="93852-255">c.</span></span> <span data-ttu-id="93852-256">在 hello**別名**文字方塊中，輸入像 brittas hello 使用者的別名。</span><span class="sxs-lookup"><span data-stu-id="93852-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="93852-257">d.</span><span class="sxs-lookup"><span data-stu-id="93852-257">d.</span></span> <span data-ttu-id="93852-258">在 hello**電子郵件**文字方塊中，輸入 hello 電子郵件地址的使用者喜歡Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="93852-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="93852-259">e.</span><span class="sxs-lookup"><span data-stu-id="93852-259">e.</span></span> <span data-ttu-id="93852-260">在 hello**使用者名**使用者的使用者名稱文字方塊中，輸入要Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="93852-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="93852-261">f.</span><span class="sxs-lookup"><span data-stu-id="93852-261">f.</span></span> <span data-ttu-id="93852-262">在 hello**別名**文字方塊中，輸入 nick 名稱，Simon 類似使用者。</span><span class="sxs-lookup"><span data-stu-id="93852-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="93852-263">g.</span><span class="sxs-lookup"><span data-stu-id="93852-263">g.</span></span> <span data-ttu-id="93852-264">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="93852-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="93852-265">hello Azure Active Directory 帳戶持有者會收到一封電子郵件，並且遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="93852-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="93852-266">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="93852-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="93852-267">在本節中，您可以授與存取 tooJobscience 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="93852-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![指派使用者][200] 

<span data-ttu-id="93852-269">**tooassign 許 Simon tooJobscience，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="93852-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="93852-270">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="93852-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="93852-272">在 [hello] 應用程式清單中，選取**Jobscience**。</span><span class="sxs-lookup"><span data-stu-id="93852-272">In hello applications list, select **Jobscience**.</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="93852-274">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="93852-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="93852-276">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="93852-276">Click **Add** button.</span></span> <span data-ttu-id="93852-277">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="93852-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="93852-279">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="93852-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="93852-280">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="93852-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93852-281">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="93852-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="93852-282">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="93852-282">Testing single sign-on</span></span>

<span data-ttu-id="93852-283">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="93852-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="93852-284">當您按一下 hello Jobscience 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Jobscience 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="93852-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="93852-285">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="93852-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93852-286">其他資源</span><span class="sxs-lookup"><span data-stu-id="93852-286">Additional resources</span></span>

* [<span data-ttu-id="93852-287">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93852-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93852-288">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="93852-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

