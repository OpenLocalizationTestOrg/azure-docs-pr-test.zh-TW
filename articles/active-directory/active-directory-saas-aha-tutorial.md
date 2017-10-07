---
title: "教學課程：Azure Active Directory 與 Aha! | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Aha ！。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: d844db3c0a035560e6fb275017215171743fba56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="e186c-104">教學課程：Azure Active Directory 與 Aha!</span><span class="sxs-lookup"><span data-stu-id="e186c-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="e186c-105">在此教學課程中，您學會如何 toointegrate Aha ！</span><span class="sxs-lookup"><span data-stu-id="e186c-105">In this tutorial, you learn how toointegrate Aha!</span></span> <span data-ttu-id="e186c-106">與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="e186c-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e186c-107">將 Aha!</span><span class="sxs-lookup"><span data-stu-id="e186c-107">Integrating Aha!</span></span> <span data-ttu-id="e186c-108">使用 Azure AD 提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="e186c-108">with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e186c-109">您可以控制存取 tooAha Azure AD 中 ！</span><span class="sxs-lookup"><span data-stu-id="e186c-109">You can control in Azure AD who has access tooAha!</span></span>
- <span data-ttu-id="e186c-110">您可以啟用您的使用者 tooautomatically get 登入 tooAha ！</span><span class="sxs-lookup"><span data-stu-id="e186c-110">You can enable your users tooautomatically get signed-on tooAha!</span></span> <span data-ttu-id="e186c-111">(單一登入)</span><span class="sxs-lookup"><span data-stu-id="e186c-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e186c-112">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e186c-112">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e186c-113">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e186c-113">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e186c-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="e186c-114">Prerequisites</span></span>

<span data-ttu-id="e186c-115">tooconfigure Azure AD 整合與 Aha ！，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="e186c-115">tooconfigure Azure AD integration with Aha!, you need hello following items:</span></span>

- <span data-ttu-id="e186c-116">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e186c-116">An Azure AD subscription</span></span>
- <span data-ttu-id="e186c-117">已啟用 Aha!</span><span class="sxs-lookup"><span data-stu-id="e186c-117">An Aha!</span></span> <span data-ttu-id="e186c-118">單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e186c-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e186c-119">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="e186c-119">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e186c-120">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e186c-120">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e186c-121">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e186c-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e186c-122">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e186c-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e186c-123">案例描述</span><span class="sxs-lookup"><span data-stu-id="e186c-123">Scenario description</span></span>
<span data-ttu-id="e186c-124">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e186c-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e186c-125">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e186c-125">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e186c-126">新增 Aha!</span><span class="sxs-lookup"><span data-stu-id="e186c-126">Adding Aha!</span></span> <span data-ttu-id="e186c-127">從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="e186c-127">from hello gallery</span></span>
2. <span data-ttu-id="e186c-128">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e186c-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-hello-gallery"></a><span data-ttu-id="e186c-129">新增 Aha!</span><span class="sxs-lookup"><span data-stu-id="e186c-129">Adding Aha!</span></span> <span data-ttu-id="e186c-130">從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="e186c-130">from hello gallery</span></span>
<span data-ttu-id="e186c-131">tooconfigure hello 整合的 Aha ！</span><span class="sxs-lookup"><span data-stu-id="e186c-131">tooconfigure hello integration of Aha!</span></span> <span data-ttu-id="e186c-132">到 Azure AD，您需要 tooadd Aha ！</span><span class="sxs-lookup"><span data-stu-id="e186c-132">into Azure AD, you need tooadd Aha!</span></span> <span data-ttu-id="e186c-133">從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單。</span><span class="sxs-lookup"><span data-stu-id="e186c-133">from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e186c-134">**tooadd Aha ！從 hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e186c-134">**tooadd Aha! from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e186c-135">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e186c-135">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e186c-137">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e186c-137">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e186c-138">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e186c-138">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e186c-140">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e186c-140">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e186c-142">在 [hello] 搜尋方塊中，輸入**Aha ！**。</span><span class="sxs-lookup"><span data-stu-id="e186c-142">In hello search box, type **Aha!**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="e186c-144">在 hello 結果 窗格中，選取  **Aha ！**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e186c-144">In hello results panel, select **Aha!**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e186c-146">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e186c-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e186c-147">在本節中，您會設定及測試與 Aha! 搭配運作的 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e186c-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="e186c-148">(以名為 "Britta Simon" 的測試使用者為基礎)。</span><span class="sxs-lookup"><span data-stu-id="e186c-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e186c-149">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Aha ！</span><span class="sxs-lookup"><span data-stu-id="e186c-149">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aha!</span></span> <span data-ttu-id="e186c-150">在 Azure AD 中為 tooa 使用者。</span><span class="sxs-lookup"><span data-stu-id="e186c-150">is tooa user in Azure AD.</span></span> <span data-ttu-id="e186c-151">換句話說，Azure AD 使用者與 hello 之間的連結關聯性相關的使用者在 Aha ！</span><span class="sxs-lookup"><span data-stu-id="e186c-151">In other words, a link relationship between an Azure AD user and hello related user in Aha!</span></span> <span data-ttu-id="e186c-152">需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="e186c-152">needs toobe established.</span></span>

<span data-ttu-id="e186c-153">在 Aha ！，hello hello 值指派**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e186c-153">In Aha!, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e186c-154">tooconfigure 和測試 Azure AD 單一登入與 Aha ！，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="e186c-154">tooconfigure and test Azure AD single sign-on with Aha!, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e186c-155">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="e186c-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e186c-156">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="e186c-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e186c-157">**[建立 Aha ！測試使用者](#creating-an-aha-test-user)** -toohave 對應項目許 Simon 中 Aha ！</span><span class="sxs-lookup"><span data-stu-id="e186c-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - toohave a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="e186c-158">這是連結的 toohello Azure AD 使用者表示法。</span><span class="sxs-lookup"><span data-stu-id="e186c-158">that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e186c-159">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e186c-159">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e186c-160">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="e186c-160">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e186c-161">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e186c-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e186c-162">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的 Aha ！</span><span class="sxs-lookup"><span data-stu-id="e186c-162">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="e186c-163">應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e186c-163">application.</span></span>

<span data-ttu-id="e186c-164">**Azure AD 單一登入的 tooconfigure 與 Aha ！，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e186c-164">**tooconfigure Azure AD single sign-on with Aha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="e186c-165">在 Azure 入口網站上 hello hello **Aha ！**</span><span class="sxs-lookup"><span data-stu-id="e186c-165">In hello Azure portal, on hello **Aha!**</span></span> <span data-ttu-id="e186c-166">應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e186c-166">application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e186c-168">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e186c-168">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="e186c-170">在 hello **Aha ！網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e186c-170">On hello **Aha! Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="e186c-172">a.</span><span class="sxs-lookup"><span data-stu-id="e186c-172">a.</span></span> <span data-ttu-id="e186c-173">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="e186c-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="e186c-174">b.</span><span class="sxs-lookup"><span data-stu-id="e186c-174">b.</span></span> <span data-ttu-id="e186c-175">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="e186c-175">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e186c-176">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="e186c-176">These values are not real.</span></span> <span data-ttu-id="e186c-177">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="e186c-177">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e186c-178">請連絡 [Aha!用戶端支援小組](https://www.aha.io/company/contact)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="e186c-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="e186c-179">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="e186c-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="e186c-181">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e186c-181">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e186c-183">在不同的網頁瀏覽器視窗中，登入 tooyour Aha ！</span><span class="sxs-lookup"><span data-stu-id="e186c-183">In a different web browser window, log in tooyour Aha!</span></span> <span data-ttu-id="e186c-184">公司網站。</span><span class="sxs-lookup"><span data-stu-id="e186c-184">company site as an administrator.</span></span>

7. <span data-ttu-id="e186c-185">在 hello 最上層顯示 hello 功能表上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="e186c-185">In hello menu on hello top, click **Settings**.</span></span>

    <span data-ttu-id="e186c-186">![設定](./media/active-directory-saas-aha-tutorial/IC798950.png "設定")</span><span class="sxs-lookup"><span data-stu-id="e186c-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="e186c-187">按一下 [帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="e186c-187">Click **Account**.</span></span>
   
    <span data-ttu-id="e186c-188">![設定檔](./media/active-directory-saas-aha-tutorial/IC798951.png "設定檔")</span><span class="sxs-lookup"><span data-stu-id="e186c-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="e186c-189">按一下 [安全性和單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="e186c-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="e186c-190">![安全性和單一登入](./media/active-directory-saas-aha-tutorial/IC798952.png "安全性和單一登入")</span><span class="sxs-lookup"><span data-stu-id="e186c-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="e186c-191">在 [單一登入] 區段中，針對 [識別提供者] 選取 [SAML2.0]。</span><span class="sxs-lookup"><span data-stu-id="e186c-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="e186c-192">![安全性和單一登入](./media/active-directory-saas-aha-tutorial/IC798953.png "安全性和單一登入")</span><span class="sxs-lookup"><span data-stu-id="e186c-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="e186c-193">在 hello**單一登入**組態頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e186c-193">On hello **Single Sign-On** configuration page, perform hello following steps:</span></span>
    
    <span data-ttu-id="e186c-194">![單一登入](./media/active-directory-saas-aha-tutorial/IC798954.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="e186c-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="e186c-195">a.</span><span class="sxs-lookup"><span data-stu-id="e186c-195">a.</span></span> <span data-ttu-id="e186c-196">在 hello**名稱**文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="e186c-196">In hello **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="e186c-197">b.</span><span class="sxs-lookup"><span data-stu-id="e186c-197">b.</span></span> <span data-ttu-id="e186c-198">針對 [設定使用]，選取 [中繼資料檔]。</span><span class="sxs-lookup"><span data-stu-id="e186c-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="e186c-199">c.</span><span class="sxs-lookup"><span data-stu-id="e186c-199">c.</span></span> <span data-ttu-id="e186c-200">tooupload 您下載的中繼資料檔案中，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="e186c-200">tooupload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="e186c-201">d.</span><span class="sxs-lookup"><span data-stu-id="e186c-201">d.</span></span> <span data-ttu-id="e186c-202">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="e186c-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="e186c-203">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="e186c-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e186c-204">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="e186c-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e186c-205">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e186c-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e186c-206">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e186c-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="e186c-207">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e186c-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e186c-209">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e186c-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e186c-210">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e186c-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e186c-212">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="e186c-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e186c-214">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="e186c-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e186c-216">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e186c-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e186c-218">a.</span><span class="sxs-lookup"><span data-stu-id="e186c-218">a.</span></span> <span data-ttu-id="e186c-219">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e186c-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e186c-220">b.</span><span class="sxs-lookup"><span data-stu-id="e186c-220">b.</span></span> <span data-ttu-id="e186c-221">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="e186c-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e186c-222">c.</span><span class="sxs-lookup"><span data-stu-id="e186c-222">c.</span></span> <span data-ttu-id="e186c-223">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="e186c-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e186c-224">d.</span><span class="sxs-lookup"><span data-stu-id="e186c-224">d.</span></span> <span data-ttu-id="e186c-225">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e186c-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="e186c-226">建立 Aha!</span><span class="sxs-lookup"><span data-stu-id="e186c-226">Creating an Aha!</span></span> <span data-ttu-id="e186c-227">測試使用者</span><span class="sxs-lookup"><span data-stu-id="e186c-227">test user</span></span>

<span data-ttu-id="e186c-228">在 tooAha tooenable Azure AD 使用者 toolog ！，您必須佈建到 Aha ！。</span><span class="sxs-lookup"><span data-stu-id="e186c-228">tooenable Azure AD users toolog in tooAha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="e186c-229">在 hello 案例中的 Aha ！，佈建是自動化的工作。</span><span class="sxs-lookup"><span data-stu-id="e186c-229">In hello case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="e186c-230">沒有您適用的動作項目。</span><span class="sxs-lookup"><span data-stu-id="e186c-230">There is no action item for you.</span></span>

<span data-ttu-id="e186c-231">使用者會自動建立必要 hello 第一個單一登入嘗試期間。</span><span class="sxs-lookup"><span data-stu-id="e186c-231">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="e186c-232">您可以使用任何其他的 Aha!</span><span class="sxs-lookup"><span data-stu-id="e186c-232">You can use any other Aha!</span></span> <span data-ttu-id="e186c-233">使用者帳戶建立工具或 Aha!</span><span class="sxs-lookup"><span data-stu-id="e186c-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="e186c-234">tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e186c-234">tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e186c-235">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="e186c-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e186c-236">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooAha ！。</span><span class="sxs-lookup"><span data-stu-id="e186c-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAha!.</span></span>

![指派使用者][200] 

<span data-ttu-id="e186c-238">**tooassign 許 Simon tooAha ！，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e186c-238">**tooassign Britta Simon tooAha!, perform hello following steps:**</span></span>

1. <span data-ttu-id="e186c-239">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e186c-239">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e186c-241">在 [hello] 應用程式清單中，選取**Aha ！**。</span><span class="sxs-lookup"><span data-stu-id="e186c-241">In hello applications list, select **Aha!**.</span></span>

    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="e186c-243">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="e186c-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e186c-245">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e186c-245">Click **Add** button.</span></span> <span data-ttu-id="e186c-246">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e186c-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e186c-248">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="e186c-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e186c-249">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e186c-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e186c-250">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e186c-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e186c-251">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e186c-251">Testing single sign-on</span></span>

<span data-ttu-id="e186c-252">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="e186c-252">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="e186c-253">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e186c-253">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e186c-254">其他資源</span><span class="sxs-lookup"><span data-stu-id="e186c-254">Additional resources</span></span>

* [<span data-ttu-id="e186c-255">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e186c-255">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e186c-256">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e186c-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

