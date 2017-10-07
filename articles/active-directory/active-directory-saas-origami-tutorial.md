---
title: "教學課程：Azure Active Directory 與 Origami 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Origami 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="cbbde-103">教學課程：Azure Active Directory 與 Origami 整合</span><span class="sxs-lookup"><span data-stu-id="cbbde-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="cbbde-104">在此教學課程中，您學會如何 toointegrate Origami 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cbbde-104">In this tutorial, you learn how toointegrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cbbde-105">與 Azure AD 整合 Origami 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="cbbde-105">Integrating Origami with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cbbde-106">您可以控制存取 tooOrigami Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="cbbde-106">You can control in Azure AD who has access tooOrigami</span></span>
- <span data-ttu-id="cbbde-107">您可以啟用您的使用者 tooautomatically get 登入 tooOrigami （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="cbbde-107">You can enable your users tooautomatically get signed-on tooOrigami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cbbde-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cbbde-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cbbde-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cbbde-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbbde-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cbbde-110">Prerequisites</span></span>

<span data-ttu-id="cbbde-111">tooconfigure Origami 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="cbbde-111">tooconfigure Azure AD integration with Origami, you need hello following items:</span></span>

- <span data-ttu-id="cbbde-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cbbde-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cbbde-113">已啟用 Origami 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cbbde-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cbbde-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="cbbde-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cbbde-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cbbde-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cbbde-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cbbde-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cbbde-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="cbbde-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cbbde-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cbbde-118">Scenario description</span></span>
<span data-ttu-id="cbbde-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbbde-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cbbde-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="cbbde-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cbbde-121">從 hello 圖庫加入 Origami</span><span class="sxs-lookup"><span data-stu-id="cbbde-121">Adding Origami from hello gallery</span></span>
2. <span data-ttu-id="cbbde-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cbbde-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-hello-gallery"></a><span data-ttu-id="cbbde-123">從 hello 圖庫加入 Origami</span><span class="sxs-lookup"><span data-stu-id="cbbde-123">Adding Origami from hello gallery</span></span>
<span data-ttu-id="cbbde-124">tooconfigure hello 整合 Origami 到 Azure AD，您需要 tooadd Origami hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbbde-124">tooconfigure hello integration of Origami into Azure AD, you need tooadd Origami from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cbbde-125">**tooadd Origami hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cbbde-125">**tooadd Origami from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbbde-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cbbde-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cbbde-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cbbde-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="cbbde-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbbde-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="cbbde-133">在 [hello] 搜尋方塊中，輸入**Origami**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-133">In hello search box, type **Origami**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="cbbde-135">在 hello 結果 窗格中，選取  **Origami**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbbde-135">In hello results panel, select **Origami**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cbbde-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cbbde-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cbbde-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Origami 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbbde-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cbbde-139">單一登入 toowork，Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者 Origami 都 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="cbbde-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Origami is tooa user in Azure AD.</span></span> <span data-ttu-id="cbbde-140">換句話說，Azure AD 使用者與 hello Origami 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="cbbde-140">In other words, a link relationship between an Azure AD user and hello related user in Origami needs toobe established.</span></span>

<span data-ttu-id="cbbde-141">Origami 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cbbde-141">In Origami, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cbbde-142">tooconfigure 及 Origami 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="cbbde-142">tooconfigure and test Azure AD single sign-on with Origami, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cbbde-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="cbbde-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cbbde-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="cbbde-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cbbde-145">**[建立測試使用者 Origami](#creating-an-origami-test-user)**  -toohave 許 Simon Origami 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="cbbde-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - toohave a counterpart of Britta Simon in Origami that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cbbde-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbbde-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cbbde-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="cbbde-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cbbde-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cbbde-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cbbde-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Origami 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbbde-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="cbbde-150">**tooconfigure Azure AD 單一登入與 Origami，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cbbde-150">**tooconfigure Azure AD single sign-on with Origami, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbbde-151">在 Azure 入口網站上 hello hello **Origami**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-151">In hello Azure portal, on hello **Origami** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="cbbde-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbbde-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="cbbde-155">在 hello **Origami 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbbde-155">On hello **Origami Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="cbbde-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="cbbde-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cbbde-158">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="cbbde-158">hello value is not real.</span></span> <span data-ttu-id="cbbde-159">更新 hello 值與 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="cbbde-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="cbbde-160">請連絡[Origami 用戶端支援小組](https://wordpress.org/support/theme/origami)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="cbbde-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) tooget hello value.</span></span> 
 
4. <span data-ttu-id="cbbde-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="cbbde-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="cbbde-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbbde-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cbbde-165">在 hello **Origami 組態**區段中，按一下**設定摺**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="cbbde-165">On hello **Origami Configuration** section, click **Configure Origami** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cbbde-166">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="cbbde-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="cbbde-168">登入 toohello Origami 帳戶擁有管理員權限。</span><span class="sxs-lookup"><span data-stu-id="cbbde-168">Log in toohello Origami account with Admin rights.</span></span>

8. <span data-ttu-id="cbbde-169">在 hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="cbbde-171">在 hello 單一登入安裝 對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbbde-171">On hello Single Sign On Setup dialog page, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="cbbde-173">a.</span><span class="sxs-lookup"><span data-stu-id="cbbde-173">a.</span></span> <span data-ttu-id="cbbde-174">選取 [啟用單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="cbbde-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="cbbde-175">b.</span><span class="sxs-lookup"><span data-stu-id="cbbde-175">b.</span></span> <span data-ttu-id="cbbde-176">在 hello**身分識別提供者登入頁面 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="cbbde-176">In hello **Identity Provider's Sign-in Page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cbbde-177">c.</span><span class="sxs-lookup"><span data-stu-id="cbbde-177">c.</span></span> <span data-ttu-id="cbbde-178">在 hello**身分識別提供者的登出頁面 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="cbbde-178">In hello **Identity Provider's Sign-out Page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cbbde-179">d.</span><span class="sxs-lookup"><span data-stu-id="cbbde-179">d.</span></span> <span data-ttu-id="cbbde-180">按一下**瀏覽**tooupload hello 憑證從 hello Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="cbbde-180">Click **Browse** tooupload hello certificate you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="cbbde-181">e.</span><span class="sxs-lookup"><span data-stu-id="cbbde-181">e.</span></span> <span data-ttu-id="cbbde-182">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="cbbde-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="cbbde-183">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="cbbde-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cbbde-184">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="cbbde-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cbbde-185">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cbbde-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cbbde-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cbbde-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="cbbde-187">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cbbde-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="cbbde-189">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cbbde-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbbde-190">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="cbbde-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cbbde-192">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cbbde-194">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="cbbde-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cbbde-196">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbbde-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cbbde-198">a.</span><span class="sxs-lookup"><span data-stu-id="cbbde-198">a.</span></span> <span data-ttu-id="cbbde-199">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cbbde-200">b.</span><span class="sxs-lookup"><span data-stu-id="cbbde-200">b.</span></span> <span data-ttu-id="cbbde-201">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="cbbde-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cbbde-202">c.</span><span class="sxs-lookup"><span data-stu-id="cbbde-202">c.</span></span> <span data-ttu-id="cbbde-203">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cbbde-204">d.</span><span class="sxs-lookup"><span data-stu-id="cbbde-204">d.</span></span> <span data-ttu-id="cbbde-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cbbde-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="cbbde-206">建立 Origami 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cbbde-206">Creating an Origami test user</span></span>

<span data-ttu-id="cbbde-207">在本節中，您要在 Origami 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="cbbde-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="cbbde-208">登入 toohello Origami 帳戶擁有管理員權限。</span><span class="sxs-lookup"><span data-stu-id="cbbde-208">Log in toohello Origami account with Admin rights.</span></span>

2. <span data-ttu-id="cbbde-209">在 hello 最上層顯示 hello 功能表上，按一下**Admin**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-209">In hello menu on hello top, click **Admin**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="cbbde-211">在 hello**的使用者和安全性群組** 對話方塊中，按一下 **使用者**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-211">On hello **Users and Security** dialog, click **Users**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="cbbde-213">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="cbbde-213">Click **Add New User**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="cbbde-215">在 hello 新增使用者對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="cbbde-215">On hello Add New User dialog, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="cbbde-217">a.</span><span class="sxs-lookup"><span data-stu-id="cbbde-217">a.</span></span> <span data-ttu-id="cbbde-218">在 hello**使用者名稱**文字方塊中，輸入 hello 電子郵件的使用者，例如 **brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="cbbde-218">In hello **User Name** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="cbbde-219">b.</span><span class="sxs-lookup"><span data-stu-id="cbbde-219">b.</span></span> <span data-ttu-id="cbbde-220">在 hello**密碼**文字方塊中，輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="cbbde-220">In hello **Password** textbox, type a password.</span></span>

    <span data-ttu-id="cbbde-221">c.</span><span class="sxs-lookup"><span data-stu-id="cbbde-221">c.</span></span> <span data-ttu-id="cbbde-222">在 hello**確認密碼**文字方塊中，輸入 hello 密碼一次。</span><span class="sxs-lookup"><span data-stu-id="cbbde-222">In hello **Confirm Password** textbox, type hello password again.</span></span>

    <span data-ttu-id="cbbde-223">d.</span><span class="sxs-lookup"><span data-stu-id="cbbde-223">d.</span></span> <span data-ttu-id="cbbde-224">在 hello**名字**文字方塊中，輸入 hello 名字，例如使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-224">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="cbbde-225">e.</span><span class="sxs-lookup"><span data-stu-id="cbbde-225">e.</span></span> <span data-ttu-id="cbbde-226">在 hello**姓氏**文字方塊中，輸入 hello 姓氏的使用者，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-226">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="cbbde-227">f.</span><span class="sxs-lookup"><span data-stu-id="cbbde-227">f.</span></span> <span data-ttu-id="cbbde-228">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="cbbde-228">Click **Save**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="cbbde-230">指派**使用者角色**和**用戶端存取**toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="cbbde-230">Assign **User Roles** and **Client Access** toohello user.</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cbbde-232">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="cbbde-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cbbde-233">在本節中，您可以授與存取 tooOrigami 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cbbde-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOrigami.</span></span>

![指派使用者][200] 

<span data-ttu-id="cbbde-235">**tooassign 許 Simon tooOrigami，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="cbbde-235">**tooassign Britta Simon tooOrigami, perform hello following steps:**</span></span>

1. <span data-ttu-id="cbbde-236">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cbbde-238">在 [hello] 應用程式清單中，選取**Origami**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-238">In hello applications list, select **Origami**.</span></span>

    ![設定單一登入](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="cbbde-240">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="cbbde-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="cbbde-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbbde-242">Click **Add** button.</span></span> <span data-ttu-id="cbbde-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cbbde-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="cbbde-245">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="cbbde-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cbbde-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbbde-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cbbde-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbbde-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cbbde-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cbbde-248">Testing single sign-on</span></span>

<span data-ttu-id="cbbde-249">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="cbbde-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cbbde-250">當您按一下 hello Origami 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Origami 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbbde-250">When you click hello Origami tile in hello Access Panel, you should get automatically signed-on tooyour Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cbbde-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="cbbde-251">Additional resources</span></span>

* [<span data-ttu-id="cbbde-252">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cbbde-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cbbde-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cbbde-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

