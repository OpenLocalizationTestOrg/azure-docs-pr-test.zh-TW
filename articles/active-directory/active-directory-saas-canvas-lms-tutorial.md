---
title: "教學課程：Azure Active Directory 與 Canvas LMS 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Canvas LMS 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="18e01-103">教學課程：Azure Active Directory 與 Canvas LMS 整合</span><span class="sxs-lookup"><span data-stu-id="18e01-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="18e01-104">在此教學課程中，您學會如何 toointegrate 畫布與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="18e01-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18e01-105">與 Azure AD 整合畫布可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="18e01-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="18e01-106">您可以控制存取 tooCanvas Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="18e01-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="18e01-107">您可以啟用您的使用者 tooautomatically get 登入 tooCanvas （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="18e01-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18e01-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="18e01-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="18e01-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="18e01-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18e01-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="18e01-110">Prerequisites</span></span>

<span data-ttu-id="18e01-111">tooconfigure 與 Canvas 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="18e01-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="18e01-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="18e01-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18e01-113">已啟用 Canvas 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="18e01-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18e01-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="18e01-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18e01-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="18e01-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18e01-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="18e01-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18e01-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="18e01-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18e01-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="18e01-118">Scenario description</span></span>
<span data-ttu-id="18e01-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18e01-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18e01-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="18e01-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18e01-121">從 hello 圖庫加入畫布</span><span class="sxs-lookup"><span data-stu-id="18e01-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="18e01-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="18e01-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="18e01-123">從 hello 圖庫加入畫布</span><span class="sxs-lookup"><span data-stu-id="18e01-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="18e01-124">tooconfigure hello 整合畫布的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 畫布。</span><span class="sxs-lookup"><span data-stu-id="18e01-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="18e01-125">**tooadd 畫布 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="18e01-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="18e01-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="18e01-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="18e01-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="18e01-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="18e01-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="18e01-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="18e01-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="18e01-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="18e01-133">在 [hello] 搜尋方塊中，輸入**畫布**。</span><span class="sxs-lookup"><span data-stu-id="18e01-133">In hello search box, type **Canvas**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="18e01-135">在 [hello [結果] 窗格中，選取 [**畫布**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="18e01-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18e01-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="18e01-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18e01-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Canvas 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18e01-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="18e01-139">單一登入 toowork，Azure AD 需要 tooknow hello 對應項目在畫布中的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="18e01-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="18e01-140">換句話說，Azure AD 使用者與 hello 畫布中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="18e01-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="18e01-141">在畫布上，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="18e01-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="18e01-142">tooconfigure 及測試 Azure AD 單一登入與畫布上，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="18e01-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="18e01-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="18e01-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="18e01-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="18e01-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18e01-145">**[建立測試使用者畫布](#creating-a-canvas-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的畫布中對應項目。</span><span class="sxs-lookup"><span data-stu-id="18e01-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="18e01-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18e01-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18e01-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="18e01-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18e01-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="18e01-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18e01-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Canvas 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="18e01-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="18e01-150">**tooconfigure Azure AD 單一登入與畫布上，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="18e01-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="18e01-151">在 Azure 入口網站上 hello hello**畫布**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="18e01-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="18e01-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18e01-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="18e01-155">在 [hello**畫布網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="18e01-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="18e01-157">a.</span><span class="sxs-lookup"><span data-stu-id="18e01-157">a.</span></span> <span data-ttu-id="18e01-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="18e01-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="18e01-159">b.</span><span class="sxs-lookup"><span data-stu-id="18e01-159">b.</span></span> <span data-ttu-id="18e01-160">在 [hello**識別碼**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="18e01-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="18e01-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="18e01-161">These values are not real.</span></span> <span data-ttu-id="18e01-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="18e01-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="18e01-163">請連絡[畫布用戶端支援小組](https://community.canvaslms.com/community/help)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="18e01-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="18e01-164">在 [hello **SAML 簽章憑證**區段，複製 hello**指紋**憑證值。</span><span class="sxs-lookup"><span data-stu-id="18e01-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="18e01-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="18e01-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="18e01-168">在 hello**畫布組態**區段中，按一下**設定畫布**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="18e01-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="18e01-169">複製 hello**變更密碼 URL、 登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="18e01-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="18e01-171">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour Canvas 公司網站。</span><span class="sxs-lookup"><span data-stu-id="18e01-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="18e01-172">跳過**課程\>受管理的帳戶\>Microsoft**。</span><span class="sxs-lookup"><span data-stu-id="18e01-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="18e01-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="18e01-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="18e01-174">Hello hello 左側瀏覽窗格中選取**驗證**，然後按一下 [**新增 SAML 設定**。</span><span class="sxs-lookup"><span data-stu-id="18e01-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="18e01-175">![驗證](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "驗證")</span><span class="sxs-lookup"><span data-stu-id="18e01-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="18e01-176">在 hello 目前整合頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="18e01-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="18e01-177">![目前的整合](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "目前的整合")</span><span class="sxs-lookup"><span data-stu-id="18e01-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="18e01-178">a.</span><span class="sxs-lookup"><span data-stu-id="18e01-178">a.</span></span> <span data-ttu-id="18e01-179">在**IdP 實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="18e01-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="18e01-180">b.</span><span class="sxs-lookup"><span data-stu-id="18e01-180">b.</span></span> <span data-ttu-id="18e01-181">在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="18e01-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="18e01-182">c.</span><span class="sxs-lookup"><span data-stu-id="18e01-182">c.</span></span> <span data-ttu-id="18e01-183">在**登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="18e01-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="18e01-184">d.</span><span class="sxs-lookup"><span data-stu-id="18e01-184">d.</span></span> <span data-ttu-id="18e01-185">在**變更密碼連結**文字方塊中，貼上 hello 值**變更密碼 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="18e01-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="18e01-186">e.</span><span class="sxs-lookup"><span data-stu-id="18e01-186">e.</span></span> <span data-ttu-id="18e01-187">在**憑證指紋**文字方塊中，貼上 hello**指紋**憑證，您從 Azure 入口網站複製的值。</span><span class="sxs-lookup"><span data-stu-id="18e01-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="18e01-188">f.</span><span class="sxs-lookup"><span data-stu-id="18e01-188">f.</span></span> <span data-ttu-id="18e01-189">從 hello**登入屬性**清單中，選取**NameID**。</span><span class="sxs-lookup"><span data-stu-id="18e01-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="18e01-190">g.</span><span class="sxs-lookup"><span data-stu-id="18e01-190">g.</span></span> <span data-ttu-id="18e01-191">從 hello**識別碼格式**清單中，選取**emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="18e01-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="18e01-192">h.</span><span class="sxs-lookup"><span data-stu-id="18e01-192">h.</span></span> <span data-ttu-id="18e01-193">按一下 [儲存驗證設定] 。</span><span class="sxs-lookup"><span data-stu-id="18e01-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="18e01-194">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="18e01-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="18e01-195">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="18e01-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="18e01-196">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18e01-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18e01-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="18e01-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="18e01-198">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="18e01-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="18e01-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="18e01-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="18e01-201">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="18e01-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18e01-203">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="18e01-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18e01-205">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="18e01-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18e01-207">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="18e01-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18e01-209">a.</span><span class="sxs-lookup"><span data-stu-id="18e01-209">a.</span></span> <span data-ttu-id="18e01-210">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="18e01-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18e01-211">b.</span><span class="sxs-lookup"><span data-stu-id="18e01-211">b.</span></span> <span data-ttu-id="18e01-212">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="18e01-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18e01-213">c.</span><span class="sxs-lookup"><span data-stu-id="18e01-213">c.</span></span> <span data-ttu-id="18e01-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="18e01-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="18e01-215">d.</span><span class="sxs-lookup"><span data-stu-id="18e01-215">d.</span></span> <span data-ttu-id="18e01-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="18e01-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="18e01-217">建立 Canvas 測試使用者</span><span class="sxs-lookup"><span data-stu-id="18e01-217">Creating a Canvas test user</span></span>

<span data-ttu-id="18e01-218">tooenable Azure AD 使用者 toolog 中 tooCanvas，它們必須佈建到 Canvas。</span><span class="sxs-lookup"><span data-stu-id="18e01-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="18e01-219">就 Canvas 而言，需以手動方式佈建使用者。</span><span class="sxs-lookup"><span data-stu-id="18e01-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="18e01-220">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="18e01-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="18e01-221">登入 tooyour**畫布**租用戶。</span><span class="sxs-lookup"><span data-stu-id="18e01-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="18e01-222">跳過**課程\>受管理的帳戶\>Microsoft**。</span><span class="sxs-lookup"><span data-stu-id="18e01-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="18e01-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="18e01-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="18e01-224">按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="18e01-224">Click **Users**.</span></span>
   
   <span data-ttu-id="18e01-225">![使用者](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="18e01-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="18e01-226">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="18e01-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="18e01-227">![使用者](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="18e01-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="18e01-228">在 hello 新增新的使用者] 對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="18e01-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="18e01-229">![新增使用者](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="18e01-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="18e01-230">a.</span><span class="sxs-lookup"><span data-stu-id="18e01-230">a.</span></span> <span data-ttu-id="18e01-231">在 [hello**全名**文字方塊中，輸入 hello 類似的使用者名稱**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="18e01-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="18e01-232">b.</span><span class="sxs-lookup"><span data-stu-id="18e01-232">b.</span></span> <span data-ttu-id="18e01-233">在 [hello**電子郵件**文字方塊中，輸入 hello 電子郵件的使用者，例如** brittasimon@contoso.com **。</span><span class="sxs-lookup"><span data-stu-id="18e01-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="18e01-234">c.</span><span class="sxs-lookup"><span data-stu-id="18e01-234">c.</span></span> <span data-ttu-id="18e01-235">在 [hello**登入**文字方塊中，輸入 hello 使用者的 Azure AD 電子郵件地址，例如** brittasimon@contoso.com **。</span><span class="sxs-lookup"><span data-stu-id="18e01-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="18e01-236">d.</span><span class="sxs-lookup"><span data-stu-id="18e01-236">d.</span></span> <span data-ttu-id="18e01-237">選取**有關此帳戶建立電子郵件 hello 使用者**。</span><span class="sxs-lookup"><span data-stu-id="18e01-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="18e01-238">e.</span><span class="sxs-lookup"><span data-stu-id="18e01-238">e.</span></span> <span data-ttu-id="18e01-239">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="18e01-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="18e01-240">您可以使用任何其他 Canvas 使用者帳戶建立工具或 Api 提供畫布 tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="18e01-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="18e01-241">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="18e01-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="18e01-242">在本節中，您可以授與存取 tooCanvas 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="18e01-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![指派使用者][200] 

<span data-ttu-id="18e01-244">**tooassign 許 Simon tooCanvas，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="18e01-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="18e01-245">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="18e01-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="18e01-247">在 [hello] 應用程式清單中，選取**畫布**。</span><span class="sxs-lookup"><span data-stu-id="18e01-247">In hello applications list, select **Canvas**.</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="18e01-249">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="18e01-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="18e01-251">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="18e01-251">Click **Add** button.</span></span> <span data-ttu-id="18e01-252">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="18e01-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="18e01-254">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="18e01-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="18e01-255">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="18e01-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18e01-256">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="18e01-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18e01-257">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="18e01-257">Testing single sign-on</span></span>

<span data-ttu-id="18e01-258">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="18e01-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="18e01-259">當您按一下 hello 畫布磚 hello 存取面板中的時，您應該取得自動登入 tooyour 畫布應用程式。</span><span class="sxs-lookup"><span data-stu-id="18e01-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="18e01-260">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="18e01-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="18e01-261">其他資源</span><span class="sxs-lookup"><span data-stu-id="18e01-261">Additional resources</span></span>

* [<span data-ttu-id="18e01-262">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18e01-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18e01-263">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="18e01-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

