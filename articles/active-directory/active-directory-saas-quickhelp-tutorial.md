---
title: "教學課程：Azure Active Directory 與 QuickHelp 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 QuickHelp 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: bbde5eb9bdad89680923ccd36c321b6923f91789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="e42b9-103">教學課程：Azure Active Directory 與 QuickHelp 整合</span><span class="sxs-lookup"><span data-stu-id="e42b9-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="e42b9-104">在此教學課程中，您學會如何 toointegrate QuickHelp 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e42b9-104">In this tutorial, you learn how toointegrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e42b9-105">與 Azure AD 整合 QuickHelp 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="e42b9-105">Integrating QuickHelp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e42b9-106">您可以控制存取 tooQuickHelp Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="e42b9-106">You can control in Azure AD who has access tooQuickHelp</span></span>
- <span data-ttu-id="e42b9-107">您可以啟用您的使用者 tooautomatically get 登入 tooQuickHelp （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="e42b9-107">You can enable your users tooautomatically get signed-on tooQuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e42b9-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e42b9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e42b9-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e42b9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e42b9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e42b9-110">Prerequisites</span></span>

<span data-ttu-id="e42b9-111">tooconfigure QuickHelp 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="e42b9-111">tooconfigure Azure AD integration with QuickHelp, you need hello following items:</span></span>

- <span data-ttu-id="e42b9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e42b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e42b9-113">啟用 QuickHelp 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e42b9-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e42b9-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="e42b9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e42b9-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e42b9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e42b9-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e42b9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e42b9-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e42b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e42b9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e42b9-118">Scenario description</span></span>
<span data-ttu-id="e42b9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e42b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e42b9-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e42b9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e42b9-121">從 hello 圖庫加入 QuickHelp</span><span class="sxs-lookup"><span data-stu-id="e42b9-121">Adding QuickHelp from hello gallery</span></span>
2. <span data-ttu-id="e42b9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e42b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-hello-gallery"></a><span data-ttu-id="e42b9-123">從 hello 圖庫加入 QuickHelp</span><span class="sxs-lookup"><span data-stu-id="e42b9-123">Adding QuickHelp from hello gallery</span></span>
<span data-ttu-id="e42b9-124">tooconfigure hello 整合 QuickHelp 到 Azure AD，您需要 tooadd QuickHelp hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e42b9-124">tooconfigure hello integration of QuickHelp into Azure AD, you need tooadd QuickHelp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e42b9-125">**tooadd QuickHelp 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e42b9-125">**tooadd QuickHelp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e42b9-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e42b9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e42b9-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e42b9-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e42b9-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e42b9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e42b9-133">在 [hello] 搜尋方塊中，輸入**QuickHelp**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-133">In hello search box, type **QuickHelp**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="e42b9-135">在 hello 結果 窗格中，選取  **QuickHelp**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e42b9-135">In hello results panel, select **QuickHelp**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e42b9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e42b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e42b9-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 QuickHelp 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e42b9-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e42b9-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 QuickHelp 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="e42b9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp is tooa user in Azure AD.</span></span> <span data-ttu-id="e42b9-140">換句話說，Azure AD 使用者與 hello QuickHelp 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="e42b9-140">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="e42b9-141">QuickHelp 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e42b9-141">In QuickHelp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e42b9-142">tooconfigure 及 QuickHelp 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="e42b9-142">tooconfigure and test Azure AD single sign-on with QuickHelp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e42b9-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="e42b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e42b9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="e42b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e42b9-145">**[建立測試使用者 QuickHelp](#creating-a-quickhelp-test-user)**  -toohave 許 Simon QuickHelp 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="e42b9-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - toohave a counterpart of Britta Simon in QuickHelp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e42b9-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e42b9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e42b9-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="e42b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e42b9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e42b9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e42b9-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 QuickHelp 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e42b9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="e42b9-150">**tooconfigure Azure AD 單一登入與 QuickHelp，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e42b9-150">**tooconfigure Azure AD single sign-on with QuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="e42b9-151">在 Azure 入口網站上 hello hello **QuickHelp**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-151">In hello Azure portal, on hello **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e42b9-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e42b9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="e42b9-155">在 hello **QuickHelp 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e42b9-155">On hello **QuickHelp Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="e42b9-157">a.</span><span class="sxs-lookup"><span data-stu-id="e42b9-157">a.</span></span> <span data-ttu-id="e42b9-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="e42b9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="e42b9-159">b.</span><span class="sxs-lookup"><span data-stu-id="e42b9-159">b.</span></span> <span data-ttu-id="e42b9-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="e42b9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e42b9-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="e42b9-161">These values are not real.</span></span> <span data-ttu-id="e42b9-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="e42b9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e42b9-163">請連絡[QuickHelp 用戶端支援小組](https://support.quickhelp.com/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="e42b9-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="e42b9-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="e42b9-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="e42b9-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e42b9-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="e42b9-168">以系統管理員身分登入 tooyour QuickHelp 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e42b9-168">Sign-on tooyour QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="e42b9-169">在 hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![設定單一登入][21]

8. <span data-ttu-id="e42b9-171">在 hello **QuickHelp Admin**功能表上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-171">In hello **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![設定單一登入][22]

9. <span data-ttu-id="e42b9-173">按一下 [驗證設定] 。</span><span class="sxs-lookup"><span data-stu-id="e42b9-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="e42b9-174">在 hello**驗證設定**頁面上，執行下列步驟的 hello</span><span class="sxs-lookup"><span data-stu-id="e42b9-174">On hello **Authentication Settings** page, perform hello following steps</span></span>
   
    ![設定單一登入][23]
   
    <span data-ttu-id="e42b9-176">a.</span><span class="sxs-lookup"><span data-stu-id="e42b9-176">a.</span></span> <span data-ttu-id="e42b9-177">對 [SSO 類型] 選取 [WSFederation]。</span><span class="sxs-lookup"><span data-stu-id="e42b9-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="e42b9-178">b.</span><span class="sxs-lookup"><span data-stu-id="e42b9-178">b.</span></span> <span data-ttu-id="e42b9-179">tooupload 下載 Azure 的中繼資料檔案，按一下 **瀏覽**、 瀏覽 toohello 檔案，然後按一下**上傳中繼資料**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-179">tooupload your downloaded Azure metadata file, click **Browse**, navigate toohello file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="e42b9-180">c.</span><span class="sxs-lookup"><span data-stu-id="e42b9-180">c.</span></span> <span data-ttu-id="e42b9-181">在 hello**電子郵件**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="e42b9-181">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="e42b9-182">d.</span><span class="sxs-lookup"><span data-stu-id="e42b9-182">d.</span></span> <span data-ttu-id="e42b9-183">在 hello**名字**文字方塊中， `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`。</span><span class="sxs-lookup"><span data-stu-id="e42b9-183">In hello **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="e42b9-184">e.</span><span class="sxs-lookup"><span data-stu-id="e42b9-184">e.</span></span> <span data-ttu-id="e42b9-185">在 hello**姓氏**文字方塊中， `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`。</span><span class="sxs-lookup"><span data-stu-id="e42b9-185">In hello **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="e42b9-186">f.</span><span class="sxs-lookup"><span data-stu-id="e42b9-186">f.</span></span> <span data-ttu-id="e42b9-187">在 hello**動作列**，按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-187">In hello **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e42b9-188">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="e42b9-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e42b9-189">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="e42b9-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e42b9-190">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e42b9-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e42b9-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e42b9-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="e42b9-192">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e42b9-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e42b9-194">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e42b9-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e42b9-195">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e42b9-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e42b9-197">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e42b9-199">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="e42b9-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e42b9-201">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e42b9-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e42b9-203">a.</span><span class="sxs-lookup"><span data-stu-id="e42b9-203">a.</span></span> <span data-ttu-id="e42b9-204">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e42b9-205">b.</span><span class="sxs-lookup"><span data-stu-id="e42b9-205">b.</span></span> <span data-ttu-id="e42b9-206">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="e42b9-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e42b9-207">c.</span><span class="sxs-lookup"><span data-stu-id="e42b9-207">c.</span></span> <span data-ttu-id="e42b9-208">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e42b9-209">d.</span><span class="sxs-lookup"><span data-stu-id="e42b9-209">d.</span></span> <span data-ttu-id="e42b9-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e42b9-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="e42b9-211">建立 QuickHelp 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e42b9-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="e42b9-212">hello 本節目標在於 toocreate QuickHelp 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="e42b9-212">hello objective of this section is toocreate a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="e42b9-213">單一登入 toowork，Azure AD 需要 tooknow QuickHelp tooa 使用者在 Azure AD 中哪些 hello 對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="e42b9-213">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp tooa user in Azure AD is.</span></span> <span data-ttu-id="e42b9-214">換句話說，Azure AD 使用者與 hello QuickHelp 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="e42b9-214">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="e42b9-215">QuickHelp 支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="e42b9-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="e42b9-216">這表示，如有必要，QuickHelp 中自動建立的使用者帳戶與 hello 帳戶是連結的 toohello Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e42b9-216">This means, if necessary, a user account is automatically created in QuickHelp and hello account is linked toohello Azure AD account.</span></span>

<span data-ttu-id="e42b9-217">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="e42b9-217">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e42b9-218">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="e42b9-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e42b9-219">在本節中，您可以授與存取 tooQuickHelp 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e42b9-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQuickHelp.</span></span>

![指派使用者][200] 

<span data-ttu-id="e42b9-221">**tooassign 許 Simon tooQuickHelp，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e42b9-221">**tooassign Britta Simon tooQuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="e42b9-222">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e42b9-224">在 [hello] 應用程式清單中，選取**QuickHelp**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-224">In hello applications list, select **QuickHelp**.</span></span>

    ![設定單一登入](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="e42b9-226">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="e42b9-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e42b9-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e42b9-228">Click **Add** button.</span></span> <span data-ttu-id="e42b9-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e42b9-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e42b9-231">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="e42b9-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e42b9-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e42b9-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e42b9-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e42b9-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e42b9-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e42b9-234">Testing single sign-on</span></span>

<span data-ttu-id="e42b9-235">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="e42b9-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="e42b9-236">當您按一下 hello QuickHelp 磚 hello 存取面板中的時，您應該取得自動登入 tooyour QuickHelp 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e42b9-236">When you click hello QuickHelp tile in hello Access Panel, you should get automatically signed-on tooyour QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="e42b9-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="e42b9-237">Additional resources</span></span>

* [<span data-ttu-id="e42b9-238">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e42b9-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e42b9-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e42b9-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
