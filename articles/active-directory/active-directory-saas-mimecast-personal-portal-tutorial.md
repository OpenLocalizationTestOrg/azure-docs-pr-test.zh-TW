---
title: "教學課程：Azure Active Directory 與 Mimecast Personal Portal 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Mimecast 個人入口網站之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ee2a8edcab36f295732ac1ebe641ed7fcfc1f2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="b76ab-103">教學課程：Azure Active Directory 與 Mimecast Personal Portal 整合</span><span class="sxs-lookup"><span data-stu-id="b76ab-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="b76ab-104">在此教學課程中，您學會如何 toointegrate Mimecast 個人入口網站與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b76ab-104">In this tutorial, you learn how toointegrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b76ab-105">與 Azure AD 整合 Mimecast 個人入口網站可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="b76ab-105">Integrating Mimecast Personal Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b76ab-106">您可以控制存取 tooMimecast 個人入口網站的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="b76ab-106">You can control in Azure AD who has access tooMimecast Personal Portal</span></span>
- <span data-ttu-id="b76ab-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooMimecast 個人入口網站 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="b76ab-107">You can enable your users tooautomatically get signed-on tooMimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b76ab-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b76ab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b76ab-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b76ab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b76ab-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b76ab-110">Prerequisites</span></span>

<span data-ttu-id="b76ab-111">tooconfigure 與 Mimecast 個人入口網站的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="b76ab-111">tooconfigure Azure AD integration with Mimecast Personal Portal, you need hello following items:</span></span>

- <span data-ttu-id="b76ab-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b76ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b76ab-113">啟用 Mimecast Personal Portal 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b76ab-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b76ab-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b76ab-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b76ab-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b76ab-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b76ab-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b76ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b76ab-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b76ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b76ab-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b76ab-118">Scenario description</span></span>
<span data-ttu-id="b76ab-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b76ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b76ab-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b76ab-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b76ab-121">從 hello 圖庫加入 Mimecast 個人入口網站</span><span class="sxs-lookup"><span data-stu-id="b76ab-121">Adding Mimecast Personal Portal from hello gallery</span></span>
2. <span data-ttu-id="b76ab-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b76ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-hello-gallery"></a><span data-ttu-id="b76ab-123">從 hello 圖庫加入 Mimecast 個人入口網站</span><span class="sxs-lookup"><span data-stu-id="b76ab-123">Adding Mimecast Personal Portal from hello gallery</span></span>
<span data-ttu-id="b76ab-124">tooconfigure hello 整合 Mimecast 個人入口網站至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Mimecast 個人入口網站。</span><span class="sxs-lookup"><span data-stu-id="b76ab-124">tooconfigure hello integration of Mimecast Personal Portal into Azure AD, you need tooadd Mimecast Personal Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b76ab-125">**tooadd Mimecast 個人入口網站從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b76ab-125">**tooadd Mimecast Personal Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b76ab-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b76ab-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b76ab-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b76ab-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b76ab-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b76ab-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b76ab-133">在 [hello] 搜尋方塊中，輸入**Mimecast 個人入口網站**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-133">In hello search box, type **Mimecast Personal Portal**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="b76ab-135">在 hello 結果 窗格中，選取  **Mimecast 個人入口網站**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b76ab-135">In hello results panel, select **Mimecast Personal Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b76ab-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b76ab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b76ab-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Mimecast Personal Portal 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b76ab-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b76ab-139">單一登入 toowork，Azure AD 需要 tooknow Mimecast 個人入口網站中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="b76ab-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Mimecast Personal Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="b76ab-140">換句話說，Azure AD 使用者與 Mimecast 個人入口網站中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="b76ab-140">In other words, a link relationship between an Azure AD user and hello related user in Mimecast Personal Portal needs toobe established.</span></span>

<span data-ttu-id="b76ab-141">在 Mimecast 個人入口網站，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b76ab-141">In Mimecast Personal Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b76ab-142">tooconfigure 及測試 Azure AD 單一登入 Mimecast 個人入口網站，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="b76ab-142">tooconfigure and test Azure AD single sign-on with Mimecast Personal Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b76ab-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="b76ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b76ab-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="b76ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b76ab-145">**[建立 Mimecast 個人入口網站的測試使用者](#creating-a-mimecast-personal-portal-test-user)** -toohave 許 Simon Mimecast 個人入口網站，連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="b76ab-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - toohave a counterpart of Britta Simon in Mimecast Personal Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b76ab-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b76ab-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b76ab-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="b76ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b76ab-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b76ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b76ab-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Mimecast 個人入口網站應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b76ab-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="b76ab-150">**tooconfigure Azure AD 單一登入 Mimecast 個人入口網站，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b76ab-150">**tooconfigure Azure AD single sign-on with Mimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="b76ab-151">在 Azure 入口網站上 hello hello **Mimecast 個人入口網站**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-151">In hello Azure portal, on hello **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b76ab-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b76ab-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="b76ab-155">在 hello **Mimecast 個人入口網站的網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b76ab-155">On hello **Mimecast Personal Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="b76ab-157">a.</span><span class="sxs-lookup"><span data-stu-id="b76ab-157">a.</span></span> <span data-ttu-id="b76ab-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="b76ab-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="b76ab-159">b.</span><span class="sxs-lookup"><span data-stu-id="b76ab-159">b.</span></span> <span data-ttu-id="b76ab-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="b76ab-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="b76ab-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="b76ab-161">These values are not real.</span></span> <span data-ttu-id="b76ab-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="b76ab-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b76ab-163">請連絡[Mimecast 個人入口網站用戶端支援小組](https://www.mimecast.com/customer-success/technical-support/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="b76ab-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) tooget these values.</span></span> 
 


4. <span data-ttu-id="b76ab-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="b76ab-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="b76ab-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b76ab-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b76ab-168">在 hello **Mimecast 個人入口網站組態**區段中，按一下**設定 Mimecast 個人入口網站**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="b76ab-168">On hello **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b76ab-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="b76ab-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="b76ab-171">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Mimecast Personal Portal 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b76ab-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="b76ab-172">跳過**服務\>應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-172">Go too**Services \> Applications**.</span></span>
   
    <span data-ttu-id="b76ab-173">![應用程式](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="b76ab-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="b76ab-174">按一下 [驗證設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="b76ab-175">![驗證設定檔](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="b76ab-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="b76ab-176">按一下 [新驗證設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="b76ab-177">![新驗證設定檔](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "新驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="b76ab-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="b76ab-178">在 hello**驗證設定檔**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b76ab-178">In hello **Authentication Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b76ab-179">![驗證設定檔](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="b76ab-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="b76ab-180">a.</span><span class="sxs-lookup"><span data-stu-id="b76ab-180">a.</span></span> <span data-ttu-id="b76ab-181">在 hello**描述**文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="b76ab-181">In hello **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="b76ab-182">b.</span><span class="sxs-lookup"><span data-stu-id="b76ab-182">b.</span></span> <span data-ttu-id="b76ab-183">選取 [強制執行 Mimecast Personal Portal 的 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="b76ab-184">c.</span><span class="sxs-lookup"><span data-stu-id="b76ab-184">c.</span></span> <span data-ttu-id="b76ab-185">在 [提供者] 中選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="b76ab-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="b76ab-186">d.</span><span class="sxs-lookup"><span data-stu-id="b76ab-186">d.</span></span> <span data-ttu-id="b76ab-187">在**簽發者 URL**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="b76ab-187">In **Issuer URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="b76ab-188">e.</span><span class="sxs-lookup"><span data-stu-id="b76ab-188">e.</span></span> <span data-ttu-id="b76ab-189">在**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="b76ab-189">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="b76ab-190">f.</span><span class="sxs-lookup"><span data-stu-id="b76ab-190">f.</span></span> <span data-ttu-id="b76ab-191">在**登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="b76ab-191">In **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b76ab-192">g.</span><span class="sxs-lookup"><span data-stu-id="b76ab-192">g.</span></span> <span data-ttu-id="b76ab-193">開啟您**base-64**編碼從 Azure 入口網站中，複製到剪貼簿，其內容的 hello 下載 [記事本] 中的憑證，然後將它貼入 toohello**身分識別提供者憑證 （中繼資料）**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b76ab-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="b76ab-194">h.</span><span class="sxs-lookup"><span data-stu-id="b76ab-194">h.</span></span> <span data-ttu-id="b76ab-195">選取 [允許單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="b76ab-196">i.</span><span class="sxs-lookup"><span data-stu-id="b76ab-196">i.</span></span> <span data-ttu-id="b76ab-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b76ab-198">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="b76ab-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b76ab-199">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="b76ab-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b76ab-200">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b76ab-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b76ab-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b76ab-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="b76ab-202">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b76ab-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b76ab-204">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b76ab-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b76ab-205">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="b76ab-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b76ab-207">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b76ab-209">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="b76ab-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b76ab-211">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b76ab-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b76ab-213">a.</span><span class="sxs-lookup"><span data-stu-id="b76ab-213">a.</span></span> <span data-ttu-id="b76ab-214">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b76ab-215">b.</span><span class="sxs-lookup"><span data-stu-id="b76ab-215">b.</span></span> <span data-ttu-id="b76ab-216">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="b76ab-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b76ab-217">c.</span><span class="sxs-lookup"><span data-stu-id="b76ab-217">c.</span></span> <span data-ttu-id="b76ab-218">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b76ab-219">d.</span><span class="sxs-lookup"><span data-stu-id="b76ab-219">d.</span></span> <span data-ttu-id="b76ab-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="b76ab-221">建立 Mimecast Personal Portal 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b76ab-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="b76ab-222">在訂單 tooenable Azure AD 使用者 toolog 入 Mimecast 個人入口網站，他們必須佈建到 Mimecast 個人入口網站。</span><span class="sxs-lookup"><span data-stu-id="b76ab-222">In order tooenable Azure AD users toolog into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="b76ab-223">在 Mimecast 個人入口網站的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="b76ab-223">In hello case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="b76ab-224">您可以建立使用者之前，您會需要 tooregister 網域。</span><span class="sxs-lookup"><span data-stu-id="b76ab-224">You need tooregister a domain before you can create users.</span></span>

<span data-ttu-id="b76ab-225">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b76ab-225">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b76ab-226">登入 tooyour **Mimecast 個人入口網站**以系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="b76ab-226">Sign on tooyour **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="b76ab-227">跳過**目錄\>內部**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-227">Go too**Directories \> Internal**.</span></span>
   
    <span data-ttu-id="b76ab-228">![目錄](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "目錄")</span><span class="sxs-lookup"><span data-stu-id="b76ab-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="b76ab-229">按一下 [註冊新網域] 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="b76ab-230">![註冊新網域](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "註冊新網域")</span><span class="sxs-lookup"><span data-stu-id="b76ab-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="b76ab-231">在您建立好新網域之後，，按一下 [新位址] 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="b76ab-232">![新位址](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "新位址")</span><span class="sxs-lookup"><span data-stu-id="b76ab-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="b76ab-233">在 hello 新位址 對話方塊中，執行下列步驟的有效 azure 的 hello 想 tooprovision AD 帳戶：</span><span class="sxs-lookup"><span data-stu-id="b76ab-233">In hello new address dialog, perform hello following steps of a valid Azure AD account you want tooprovision:</span></span>
   
    <span data-ttu-id="b76ab-234">![儲存](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "儲存")</span><span class="sxs-lookup"><span data-stu-id="b76ab-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="b76ab-235">a.</span><span class="sxs-lookup"><span data-stu-id="b76ab-235">a.</span></span> <span data-ttu-id="b76ab-236">在 hello**電子郵件地址**文字方塊中，輸入**電子郵件地址**的 hello 使用者 **BrittaSimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-236">In hello **Email Address** textbox, type **Email Address** of hello user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="b76ab-237">b.</span><span class="sxs-lookup"><span data-stu-id="b76ab-237">b.</span></span> <span data-ttu-id="b76ab-238">在 hello**全域名稱**文字方塊中，型別 hello **username**做為**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-238">In hello **Global Name** textbox, type hello **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="b76ab-239">c.</span><span class="sxs-lookup"><span data-stu-id="b76ab-239">c.</span></span> <span data-ttu-id="b76ab-240">在 hello**密碼**，和**確認密碼**等文字方塊中，型別 hello**密碼**hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="b76ab-240">In hello **Password**, and **Confirm Password** textboxes, type hello **Password** of hello user.</span></span>
   
    <span data-ttu-id="b76ab-241">b.</span><span class="sxs-lookup"><span data-stu-id="b76ab-241">b.</span></span> <span data-ttu-id="b76ab-242">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b76ab-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="b76ab-243">您可以使用任何其他 Mimecast 個人入口網站使用者帳戶建立工具或 Api Mimecast 個人入口網站 tooprovision Azure AD 使用者帳戶所提供。</span><span class="sxs-lookup"><span data-stu-id="b76ab-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal tooprovision Azure AD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b76ab-244">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="b76ab-244">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b76ab-245">在本節中，您可以授與存取 tooMimecast 個人入口網站啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b76ab-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMimecast Personal Portal.</span></span>

![指派使用者][200] 

<span data-ttu-id="b76ab-247">**tooassign 許 Simon tooMimecast 個人入口網站，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="b76ab-247">**tooassign Britta Simon tooMimecast Personal Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="b76ab-248">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b76ab-250">在 [hello] 應用程式清單中，選取**Mimecast 個人入口網站**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-250">In hello applications list, select **Mimecast Personal Portal**.</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="b76ab-252">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="b76ab-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b76ab-254">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b76ab-254">Click **Add** button.</span></span> <span data-ttu-id="b76ab-255">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b76ab-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b76ab-257">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="b76ab-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b76ab-258">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b76ab-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b76ab-259">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b76ab-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b76ab-260">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b76ab-260">Testing single sign-on</span></span>
<span data-ttu-id="b76ab-261">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="b76ab-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b76ab-262">當您按一下 hello Mimecast 個人入口網站的並排顯示 hello 存取面板中時，您應該取得 tooyour 自動登入 Mimecast 個人入口網站應用程式。</span><span class="sxs-lookup"><span data-stu-id="b76ab-262">When you click hello Mimecast Personal Portal tile in hello Access Panel, you should get automatically signed-on tooyour Mimecast Personal Portal application.</span></span> <span data-ttu-id="b76ab-263">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b76ab-263">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b76ab-264">其他資源</span><span class="sxs-lookup"><span data-stu-id="b76ab-264">Additional resources</span></span>

* [<span data-ttu-id="b76ab-265">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b76ab-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b76ab-266">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b76ab-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

