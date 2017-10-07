---
title: "教學課程：Azure Active Directory 與 Marketo 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和 Marketo 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 87f88cde4f027f99a83c1ab3b318247bb4d658ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a><span data-ttu-id="4484a-103">教學課程：Azure Active Directory 與 Marketo 整合</span><span class="sxs-lookup"><span data-stu-id="4484a-103">Tutorial: Azure Active Directory integration with Marketo</span></span>

<span data-ttu-id="4484a-104">在此教學課程中，您學會如何 toointegrate Marketo 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4484a-104">In this tutorial, you learn how toointegrate Marketo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4484a-105">與 Azure AD 整合 Marketo 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="4484a-105">Integrating Marketo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4484a-106">您可以控制存取 tooMarketo Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="4484a-106">You can control in Azure AD who has access tooMarketo</span></span>
- <span data-ttu-id="4484a-107">您可以啟用您的使用者 tooautomatically get 登入 tooMarketo （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="4484a-107">You can enable your users tooautomatically get signed-on tooMarketo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4484a-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4484a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4484a-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4484a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4484a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4484a-110">Prerequisites</span></span>

<span data-ttu-id="4484a-111">tooconfigure Marketo 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="4484a-111">tooconfigure Azure AD integration with Marketo, you need hello following items:</span></span>

- <span data-ttu-id="4484a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4484a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4484a-113">啟用 Marketo 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4484a-113">A Marketo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4484a-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="4484a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4484a-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4484a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4484a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4484a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4484a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="4484a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4484a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4484a-118">Scenario description</span></span>
<span data-ttu-id="4484a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4484a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4484a-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="4484a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4484a-121">從 hello 圖庫加入 Marketo</span><span class="sxs-lookup"><span data-stu-id="4484a-121">Adding Marketo from hello gallery</span></span>
2. <span data-ttu-id="4484a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4484a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-marketo-from-hello-gallery"></a><span data-ttu-id="4484a-123">從 hello 圖庫加入 Marketo</span><span class="sxs-lookup"><span data-stu-id="4484a-123">Adding Marketo from hello gallery</span></span>
<span data-ttu-id="4484a-124">tooconfigure hello 整合 Marketo 到 Azure AD，您需要 tooadd Marketo hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4484a-124">tooconfigure hello integration of Marketo into Azure AD, you need tooadd Marketo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4484a-125">**tooadd Marketo hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4484a-125">**tooadd Marketo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4484a-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4484a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4484a-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4484a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4484a-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4484a-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="4484a-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="4484a-133">在 [hello] 搜尋方塊中，輸入**Marketo**。</span><span class="sxs-lookup"><span data-stu-id="4484a-133">In hello search box, type **Marketo**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_search.png)

5. <span data-ttu-id="4484a-135">在 hello 結果 窗格中，選取  **Marketo**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4484a-135">In hello results panel, select **Marketo**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4484a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4484a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4484a-138">在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Marketo 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4484a-138">In this section, you configure and test Azure AD single sign-on with Marketo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4484a-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者於 Marketo 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="4484a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Marketo is tooa user in Azure AD.</span></span> <span data-ttu-id="4484a-140">換句話說，Azure AD 使用者與 hello Marketo 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="4484a-140">In other words, a link relationship between an Azure AD user and hello related user in Marketo needs toobe established.</span></span>

<span data-ttu-id="4484a-141">於 Marketo，指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4484a-141">In Marketo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4484a-142">tooconfigure 及 Marketo 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="4484a-142">tooconfigure and test Azure AD single sign-on with Marketo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4484a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="4484a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4484a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="4484a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4484a-145">**[建立測試使用者 Marketo](#creating-a-marketo-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Marketo 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="4484a-145">**[Creating a Marketo test user](#creating-a-marketo-test-user)** - toohave a counterpart of Britta Simon in Marketo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4484a-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4484a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4484a-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="4484a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4484a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4484a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4484a-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的 Marketo 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="4484a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Marketo application.</span></span>

<span data-ttu-id="4484a-150">**tooconfigure Azure AD 單一登入與 Marketo，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4484a-150">**tooconfigure Azure AD single sign-on with Marketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="4484a-151">在 Azure 入口網站上 hello hello **Marketo**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="4484a-151">In hello Azure portal, on hello **Marketo** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="4484a-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4484a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_samlbase.png)

3. <span data-ttu-id="4484a-155">在 hello **Marketo 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4484a-155">On hello **Marketo Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_url.png)

    <span data-ttu-id="4484a-157">a.</span><span class="sxs-lookup"><span data-stu-id="4484a-157">a.</span></span> <span data-ttu-id="4484a-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://saml.marketo.com/sp`</span><span class="sxs-lookup"><span data-stu-id="4484a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://saml.marketo.com/sp`</span></span>

    <span data-ttu-id="4484a-159">b.</span><span class="sxs-lookup"><span data-stu-id="4484a-159">b.</span></span> <span data-ttu-id="4484a-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://login.marketo.com/saml/assertion/\<munchkinid\>`</span><span class="sxs-lookup"><span data-stu-id="4484a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://login.marketo.com/saml/assertion/\<munchkinid\>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4484a-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="4484a-161">These values are not real.</span></span> <span data-ttu-id="4484a-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="4484a-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="4484a-163">請連絡[Marketo 支援小組](http://investors.marketo.com/contactus.cfm)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="4484a-163">Contact [Marketo support team](http://investors.marketo.com/contactus.cfm) tooget these values.</span></span>
 
4. <span data-ttu-id="4484a-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="4484a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_certificate.png) 

5. <span data-ttu-id="4484a-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4484a-168">在 hello **Marketo 組態**區段中，按一下**設定 Marketo** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="4484a-168">On hello **Marketo Configuration** section, click **Configure Marketo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4484a-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="4484a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_configure.png) 

7. <span data-ttu-id="4484a-171">tooget Munchkin 識別碼，應用程式的登入 tooMarketo 使用管理員認證，然後執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="4484a-171">tooget Munchkin Id of your application, log in tooMarketo using admin credentials and perform following actions:</span></span>
   
    <span data-ttu-id="4484a-172">a.</span><span class="sxs-lookup"><span data-stu-id="4484a-172">a.</span></span> <span data-ttu-id="4484a-173">登入 tooMarketo 應用程式使用系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="4484a-173">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="4484a-174">b.</span><span class="sxs-lookup"><span data-stu-id="4484a-174">b.</span></span> <span data-ttu-id="4484a-175">按一下 hello **Admin** hello 上方瀏覽窗格上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-175">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="4484a-177">c.</span><span class="sxs-lookup"><span data-stu-id="4484a-177">c.</span></span> <span data-ttu-id="4484a-178">瀏覽 toohello 整合功能表上，按一下 hello **Munchkin 連結**。</span><span class="sxs-lookup"><span data-stu-id="4484a-178">Navigate toohello Integration menu and click hello **Munchkin link**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_11.png)
   
    <span data-ttu-id="4484a-180">d.</span><span class="sxs-lookup"><span data-stu-id="4484a-180">d.</span></span> <span data-ttu-id="4484a-181">複製 hello Munchkin 識別碼 hello 螢幕上顯示，並完成您的回覆 URL 在 hello Azure AD 設定精靈。</span><span class="sxs-lookup"><span data-stu-id="4484a-181">Copy hello Munchkin Id shown on hello screen and complete your Reply URL in hello Azure AD configuration wizard.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_12.png) 

8. <span data-ttu-id="4484a-183">tooconfigure hello SSO hello 應用程式中，請遵循下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="4484a-183">tooconfigure hello SSO in hello application, follow hello below steps:</span></span>
   
    <span data-ttu-id="4484a-184">a.</span><span class="sxs-lookup"><span data-stu-id="4484a-184">a.</span></span> <span data-ttu-id="4484a-185">登入 tooMarketo 應用程式使用系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="4484a-185">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="4484a-186">b.</span><span class="sxs-lookup"><span data-stu-id="4484a-186">b.</span></span> <span data-ttu-id="4484a-187">按一下 hello **Admin** hello 上方瀏覽窗格上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-187">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="4484a-189">c.</span><span class="sxs-lookup"><span data-stu-id="4484a-189">c.</span></span> <span data-ttu-id="4484a-190">瀏覽 toohello 整合功能表上，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="4484a-190">Navigate toohello Integration menu and click **Single Sign On**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_07.png) 
   
    <span data-ttu-id="4484a-192">d.</span><span class="sxs-lookup"><span data-stu-id="4484a-192">d.</span></span> <span data-ttu-id="4484a-193">按一下 [tooenable hello SAML 設定**編輯**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-193">tooenable hello SAML Settings, click **Edit** button.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_08.png) 
   
    <span data-ttu-id="4484a-195">e.</span><span class="sxs-lookup"><span data-stu-id="4484a-195">e.</span></span> <span data-ttu-id="4484a-196">**已啟用**單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="4484a-196">**Enabled** Single Sign-On settings.</span></span>
   
    <span data-ttu-id="4484a-197">f.</span><span class="sxs-lookup"><span data-stu-id="4484a-197">f.</span></span> <span data-ttu-id="4484a-198">貼上 hello **SAML 實體識別碼**，在 hello**簽發者 ID**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4484a-198">Paste hello **SAML Entity ID**, in hello **Issuer ID** textbox.</span></span>
   
    <span data-ttu-id="4484a-199">g.</span><span class="sxs-lookup"><span data-stu-id="4484a-199">g.</span></span> <span data-ttu-id="4484a-200">在 hello**實體識別碼**文字方塊中，輸入 hello URL 做為`http://saml.marketo.com/sp`。</span><span class="sxs-lookup"><span data-stu-id="4484a-200">In hello **Entity ID** textbox, enter hello URL as `http://saml.marketo.com/sp`.</span></span>
   
    <span data-ttu-id="4484a-201">h.</span><span class="sxs-lookup"><span data-stu-id="4484a-201">h.</span></span> <span data-ttu-id="4484a-202">選取 hello 使用者識別碼位置做為**名稱識別碼元素**。</span><span class="sxs-lookup"><span data-stu-id="4484a-202">Select hello User ID Location as **Name Identifier element**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > <span data-ttu-id="4484a-204">如果您的使用者識別碼不是 UPN 值則變更 hello 屬性 索引標籤中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="4484a-204">If your User Identifier is not UPN value then change hello value in hello Attribute tab.</span></span>
   
    <span data-ttu-id="4484a-205">i.</span><span class="sxs-lookup"><span data-stu-id="4484a-205">i.</span></span> <span data-ttu-id="4484a-206">上傳 hello 憑證，您已下載從 Azure AD 組態精靈。</span><span class="sxs-lookup"><span data-stu-id="4484a-206">Upload hello certificate, which you have downloaded from Azure AD configuration wizard.</span></span> <span data-ttu-id="4484a-207">**儲存**hello 設定。</span><span class="sxs-lookup"><span data-stu-id="4484a-207">**Save** hello settings.</span></span>
   
    <span data-ttu-id="4484a-208">j.</span><span class="sxs-lookup"><span data-stu-id="4484a-208">j.</span></span> <span data-ttu-id="4484a-209">編輯 hello 重新導向頁面設定。</span><span class="sxs-lookup"><span data-stu-id="4484a-209">Edit hello Redirect Pages settings.</span></span>
   
    <span data-ttu-id="4484a-210">k.</span><span class="sxs-lookup"><span data-stu-id="4484a-210">k.</span></span> <span data-ttu-id="4484a-211">貼上 hello **SAML 單一登入服務 URL**在 hello**登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4484a-211">Paste hello **SAML Single Sign-On Service URL** in hello **Login URL** textbox.</span></span>
   
    <span data-ttu-id="4484a-212">l.</span><span class="sxs-lookup"><span data-stu-id="4484a-212">l.</span></span> <span data-ttu-id="4484a-213">貼上 hello**登出 URL**在 hello**登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4484a-213">Paste hello **Sign-Out URL** in hello **Logout URL** textbox.</span></span>
   
    <span data-ttu-id="4484a-214">m.</span><span class="sxs-lookup"><span data-stu-id="4484a-214">m.</span></span> <span data-ttu-id="4484a-215">在 hello**錯誤 URL**，複製您**Marketo 的執行個體 URL**按一下**儲存**按鈕 toosave 設定。</span><span class="sxs-lookup"><span data-stu-id="4484a-215">In hello **Error URL**, copy your **Marketo instance URL** and click **Save** button toosave settings.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_10.png)

9. <span data-ttu-id="4484a-217">tooenable hello SSO 的使用者，完成下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="4484a-217">tooenable hello SSO for users, complete hello following actions:</span></span>
   
    <span data-ttu-id="4484a-218">a.</span><span class="sxs-lookup"><span data-stu-id="4484a-218">a.</span></span> <span data-ttu-id="4484a-219">登入 tooMarketo 應用程式使用系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="4484a-219">Log in tooMarketo app using admin credentials.</span></span>
   
    <span data-ttu-id="4484a-220">b.</span><span class="sxs-lookup"><span data-stu-id="4484a-220">b.</span></span> <span data-ttu-id="4484a-221">按一下 hello **Admin** hello 上方瀏覽窗格上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-221">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 
   
    <span data-ttu-id="4484a-223">c.</span><span class="sxs-lookup"><span data-stu-id="4484a-223">c.</span></span> <span data-ttu-id="4484a-224">瀏覽 toohello**安全性**功能表，然後按一下**登入設定**。</span><span class="sxs-lookup"><span data-stu-id="4484a-224">Navigate toohello **Security** menu and click **Login Settings**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_13.png)
   
    <span data-ttu-id="4484a-226">d.</span><span class="sxs-lookup"><span data-stu-id="4484a-226">d.</span></span> <span data-ttu-id="4484a-227">檢查 hello**需要 SSO**選項和**儲存**hello 設定。</span><span class="sxs-lookup"><span data-stu-id="4484a-227">Check hello **Require SSO** option and **Save** hello settings.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> <span data-ttu-id="4484a-229">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="4484a-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4484a-230">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="4484a-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4484a-231">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4484a-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4484a-232">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4484a-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="4484a-233">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4484a-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="4484a-235">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4484a-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4484a-236">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4484a-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4484a-238">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="4484a-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4484a-240">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="4484a-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4484a-242">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4484a-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-marketo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4484a-244">a.</span><span class="sxs-lookup"><span data-stu-id="4484a-244">a.</span></span> <span data-ttu-id="4484a-245">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4484a-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4484a-246">b.</span><span class="sxs-lookup"><span data-stu-id="4484a-246">b.</span></span> <span data-ttu-id="4484a-247">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="4484a-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4484a-248">c.</span><span class="sxs-lookup"><span data-stu-id="4484a-248">c.</span></span> <span data-ttu-id="4484a-249">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="4484a-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4484a-250">d.</span><span class="sxs-lookup"><span data-stu-id="4484a-250">d.</span></span> <span data-ttu-id="4484a-251">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4484a-251">Click **Create**.</span></span>
 
### <a name="creating-a-marketo-test-user"></a><span data-ttu-id="4484a-252">建立 Marketo 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4484a-252">Creating a Marketo test user</span></span>

<span data-ttu-id="4484a-253">在本節中，您要在 Marketo 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4484a-253">In this section, you create a user called Britta Simon in Marketo.</span></span> <span data-ttu-id="4484a-254">請遵循這些步驟 toocreate Marketo 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="4484a-254">follow these steps toocreate a user in Marketo platform.</span></span>

1. <span data-ttu-id="4484a-255">登入 tooMarketo 應用程式使用系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="4484a-255">Log in tooMarketo app using admin credentials.</span></span>

2. <span data-ttu-id="4484a-256">按一下 hello **Admin** hello 上方瀏覽窗格上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-256">Click hello **Admin** button on hello top navigation pane.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_06.png) 

3. <span data-ttu-id="4484a-258">瀏覽 toohello**安全性**功能表，然後按一下**使用者和角色**</span><span class="sxs-lookup"><span data-stu-id="4484a-258">Navigate toohello **Security** menu and click **Users & Roles**</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_19.png)  

4. <span data-ttu-id="4484a-260">按一下 hello**邀請新使用者**hello 使用者 索引標籤上的連結</span><span class="sxs-lookup"><span data-stu-id="4484a-260">Click hello **Invite New User** link on hello Users tab</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_15.png) 

5. <span data-ttu-id="4484a-262">在下列資訊的 hello 邀請新增使用者精靈填滿 hello</span><span class="sxs-lookup"><span data-stu-id="4484a-262">In hello Invite New User wizard fill hello following information</span></span>
   
    <span data-ttu-id="4484a-263">a.</span><span class="sxs-lookup"><span data-stu-id="4484a-263">a.</span></span> <span data-ttu-id="4484a-264">輸入 hello 使用者**電子郵件**hello 文字方塊中的位址</span><span class="sxs-lookup"><span data-stu-id="4484a-264">Enter hello user **Email** address in hello textbox</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_16.png)
   
    <span data-ttu-id="4484a-266">b.</span><span class="sxs-lookup"><span data-stu-id="4484a-266">b.</span></span> <span data-ttu-id="4484a-267">輸入 hello**名字**hello 文字方塊中</span><span class="sxs-lookup"><span data-stu-id="4484a-267">Enter hello **First Name** in hello textbox</span></span>
   
    <span data-ttu-id="4484a-268">c.</span><span class="sxs-lookup"><span data-stu-id="4484a-268">c.</span></span> <span data-ttu-id="4484a-269">輸入 hello**姓氏**hello 文字方塊中</span><span class="sxs-lookup"><span data-stu-id="4484a-269">Enter hello **Last Name**  in hello textbox</span></span>
   
    <span data-ttu-id="4484a-270">d.</span><span class="sxs-lookup"><span data-stu-id="4484a-270">d.</span></span> <span data-ttu-id="4484a-271">按一下 [下一步] </span><span class="sxs-lookup"><span data-stu-id="4484a-271">Click **Next**</span></span>

6. <span data-ttu-id="4484a-272">在 hello**權限**索引標籤，選取 hello **userRoles**按一下**下一步**</span><span class="sxs-lookup"><span data-stu-id="4484a-272">In hello **Permissions** tab, select hello **userRoles** and click **Next**</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_17.png)
7. <span data-ttu-id="4484a-274">按一下 hello**傳送**按鈕 toosend hello 使用者邀請</span><span class="sxs-lookup"><span data-stu-id="4484a-274">Click hello **Send** button toosend hello user invitation</span></span>
   
    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_18.png)

8. <span data-ttu-id="4484a-276">使用者會收到 hello 電子郵件通知，並擁有 tooclick hello 連結，並變更 hello 密碼 tooactivate hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4484a-276">User receives hello email notification and has tooclick hello link and change hello password tooactivate hello account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4484a-277">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="4484a-277">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4484a-278">在本節中，您可以授與存取 tooMarketo 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4484a-278">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMarketo.</span></span>

![指派使用者][200] 

<span data-ttu-id="4484a-280">**tooassign 許 Simon tooMarketo，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4484a-280">**tooassign Britta Simon tooMarketo, perform hello following steps:**</span></span>

1. <span data-ttu-id="4484a-281">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4484a-281">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4484a-283">在 [hello] 應用程式清單中，選取**Marketo**。</span><span class="sxs-lookup"><span data-stu-id="4484a-283">In hello applications list, select **Marketo**.</span></span>

    ![設定單一登入](./media/active-directory-saas-marketo-tutorial/tutorial_marketo_app.png) 

3. <span data-ttu-id="4484a-285">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="4484a-285">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="4484a-287">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-287">Click **Add** button.</span></span> <span data-ttu-id="4484a-288">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4484a-288">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="4484a-290">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="4484a-290">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4484a-291">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-291">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4484a-292">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4484a-292">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4484a-293">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4484a-293">Testing single sign-on</span></span>

<span data-ttu-id="4484a-294">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="4484a-294">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4484a-295">當您按一下 hello Marketo 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Marketo 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4484a-295">When you click hello Marketo tile in hello Access Panel, you should get automatically signed-on tooyour Marketo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4484a-296">其他資源</span><span class="sxs-lookup"><span data-stu-id="4484a-296">Additional resources</span></span>

* [<span data-ttu-id="4484a-297">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4484a-297">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4484a-298">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4484a-298">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-marketo-tutorial/tutorial_general_203.png

