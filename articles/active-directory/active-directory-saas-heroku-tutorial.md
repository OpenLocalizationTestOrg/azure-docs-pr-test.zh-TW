---
title: "教學課程：Azure Active Directory 與 Heroku 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Heroku 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee11db647fd385140f1dbcab2586dfafffe5d912
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="d9b03-103">教學課程：Azure Active Directory 與 Heroku 整合</span><span class="sxs-lookup"><span data-stu-id="d9b03-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="d9b03-104">在此教學課程中，您學會如何 toointegrate Heroku 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d9b03-104">In this tutorial, you learn how toointegrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9b03-105">與 Azure AD 整合 Heroku 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="d9b03-105">Integrating Heroku with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d9b03-106">您可以控制存取 tooHeroku Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="d9b03-106">You can control in Azure AD who has access tooHeroku</span></span>
- <span data-ttu-id="d9b03-107">您可以啟用您的使用者 tooautomatically get 登入 tooHeroku （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="d9b03-107">You can enable your users tooautomatically get signed-on tooHeroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9b03-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d9b03-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d9b03-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d9b03-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9b03-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d9b03-110">Prerequisites</span></span>

<span data-ttu-id="d9b03-111">tooconfigure Heroku 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d9b03-111">tooconfigure Azure AD integration with Heroku, you need hello following items:</span></span>

- <span data-ttu-id="d9b03-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d9b03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9b03-113">已啟用 Heroku 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d9b03-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9b03-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="d9b03-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9b03-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d9b03-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9b03-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d9b03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9b03-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d9b03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9b03-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d9b03-118">Scenario description</span></span>
<span data-ttu-id="d9b03-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9b03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9b03-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d9b03-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9b03-121">從 hello 圖庫加入 Heroku</span><span class="sxs-lookup"><span data-stu-id="d9b03-121">Adding Heroku from hello gallery</span></span>
2. <span data-ttu-id="d9b03-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d9b03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-hello-gallery"></a><span data-ttu-id="d9b03-123">從 hello 圖庫加入 Heroku</span><span class="sxs-lookup"><span data-stu-id="d9b03-123">Adding Heroku from hello gallery</span></span>
<span data-ttu-id="d9b03-124">tooconfigure hello 整合 Heroku 到 Azure AD，您需要 tooadd Heroku hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9b03-124">tooconfigure hello integration of Heroku into Azure AD, you need tooadd Heroku from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d9b03-125">**tooadd Heroku 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d9b03-125">**tooadd Heroku from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9b03-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d9b03-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9b03-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d9b03-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d9b03-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9b03-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d9b03-133">在 [hello] 搜尋方塊中，輸入**Heroku**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-133">In hello search box, type **Heroku**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="d9b03-135">在 hello 結果 窗格中，選取  **Heroku**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9b03-135">In hello results panel, select **Heroku**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9b03-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d9b03-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="d9b03-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Heroku 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9b03-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9b03-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Heroku 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="d9b03-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Heroku is tooa user in Azure AD.</span></span> <span data-ttu-id="d9b03-140">換句話說，Azure AD 使用者與 hello Heroku 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="d9b03-140">In other words, a link relationship between an Azure AD user and hello related user in Heroku needs toobe established.</span></span>

<span data-ttu-id="d9b03-141">Heroku 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d9b03-141">In Heroku, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d9b03-142">tooconfigure 及 Heroku 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="d9b03-142">tooconfigure and test Azure AD single sign-on with Heroku, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d9b03-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="d9b03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d9b03-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="d9b03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9b03-145">**[建立測試使用者 Heroku](#creating-a-heroku-test-user)**  -toohave 許 Simon Heroku 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="d9b03-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - toohave a counterpart of Britta Simon in Heroku that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9b03-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9b03-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9b03-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="d9b03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9b03-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d9b03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9b03-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Heroku 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9b03-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="d9b03-150">**tooconfigure Azure AD 單一登入與 Heroku，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d9b03-150">**tooconfigure Azure AD single sign-on with Heroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9b03-151">在 Azure 入口網站上 hello hello **Heroku**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-151">In hello Azure portal, on hello **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d9b03-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9b03-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="d9b03-155">在 hello **Heroku 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9b03-155">On hello **Heroku Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="d9b03-157">a.</span><span class="sxs-lookup"><span data-stu-id="d9b03-157">a.</span></span> <span data-ttu-id="d9b03-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9b03-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="d9b03-159">b.</span><span class="sxs-lookup"><span data-stu-id="d9b03-159">b.</span></span> <span data-ttu-id="d9b03-160">在 hello**識別項 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9b03-160">In hello **Identifier URL** textbox, type a URL using hello following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="d9b03-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="d9b03-161">These values are not real.</span></span> <span data-ttu-id="d9b03-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="d9b03-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d9b03-163">您可以從 Heroku 小組取得這些值，本文後面幾節會有相關說明。</span><span class="sxs-lookup"><span data-stu-id="d9b03-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="d9b03-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="d9b03-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="d9b03-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9b03-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d9b03-168">tooenable SSO 中 Heroku，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9b03-168">tooenable SSO in Heroku, perform hello following steps:</span></span>
   
    <span data-ttu-id="d9b03-169">a.</span><span class="sxs-lookup"><span data-stu-id="d9b03-169">a.</span></span> <span data-ttu-id="d9b03-170">登入 toohello Heroku 帳戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="d9b03-170">Log in toohello Heroku account as an administrator.</span></span>

    <span data-ttu-id="d9b03-171">b.</span><span class="sxs-lookup"><span data-stu-id="d9b03-171">b.</span></span> <span data-ttu-id="d9b03-172">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d9b03-172">Click hello **Settings** tab.</span></span>

    <span data-ttu-id="d9b03-173">c.</span><span class="sxs-lookup"><span data-stu-id="d9b03-173">c.</span></span> <span data-ttu-id="d9b03-174">在 hello**單一登入頁面**，按一下 **上傳中繼資料**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-174">On hello **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="d9b03-175">d.</span><span class="sxs-lookup"><span data-stu-id="d9b03-175">d.</span></span> <span data-ttu-id="d9b03-176">上傳 hello 中繼資料檔案，從 hello Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="d9b03-176">Upload hello metadata file, which you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="d9b03-177">e.</span><span class="sxs-lookup"><span data-stu-id="d9b03-177">e.</span></span> <span data-ttu-id="d9b03-178">Hello 安裝成功時，系統管理員，請參閱 「 確認對話方塊，並顯示 hello URL hello SSO 登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="d9b03-178">When hello setup is successful, administrators see a confirmation dialog and hello URL of hello SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="d9b03-179">f.</span><span class="sxs-lookup"><span data-stu-id="d9b03-179">f.</span></span> <span data-ttu-id="d9b03-180">複製 hello **Heroku 登入 URL**和**Heroku 實體識別碼**值和移回太**Heroku 網域和 Url**區段在 Azure 入口網站，並將這些值貼到 hello **登入 Url**和**識別碼**文字方塊分別。</span><span class="sxs-lookup"><span data-stu-id="d9b03-180">Copy hello **Heroku Login URL** and **Heroku Entity ID** values and go back too**Heroku Domain and URLs** section in Azure portal and paste these values into hello **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="d9b03-182">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d9b03-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="d9b03-183">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="d9b03-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d9b03-184">加入此應用程式從 hello 之後**Active Directory 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="d9b03-184">After adding this app from hello **Active Directory Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d9b03-185">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9b03-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9b03-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9b03-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="d9b03-187">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d9b03-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d9b03-189">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d9b03-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9b03-190">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d9b03-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9b03-192">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9b03-194">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="d9b03-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9b03-196">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9b03-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9b03-198">a.</span><span class="sxs-lookup"><span data-stu-id="d9b03-198">a.</span></span> <span data-ttu-id="d9b03-199">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9b03-200">b.</span><span class="sxs-lookup"><span data-stu-id="d9b03-200">b.</span></span> <span data-ttu-id="d9b03-201">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="d9b03-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9b03-202">c.</span><span class="sxs-lookup"><span data-stu-id="d9b03-202">c.</span></span> <span data-ttu-id="d9b03-203">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d9b03-204">d.</span><span class="sxs-lookup"><span data-stu-id="d9b03-204">d.</span></span> <span data-ttu-id="d9b03-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d9b03-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="d9b03-206">建立 Heroku 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9b03-206">Creating a Heroku test user</span></span>

<span data-ttu-id="d9b03-207">在本節中，您要在 Heroku 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="d9b03-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="d9b03-208">Heroku 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="d9b03-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="d9b03-209">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="d9b03-209">There is no action item for you in this section.</span></span> <span data-ttu-id="d9b03-210">如果還不存在的 hello 使用者存取 Heroku 時，會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="d9b03-210">A new user is created when accessing Heroku if hello user doesn't exist yet.</span></span> <span data-ttu-id="d9b03-211">Hello 帳戶佈建之後，hello 使用者會獲得驗證電子郵件，並需要 tooclick hello 通知連結。</span><span class="sxs-lookup"><span data-stu-id="d9b03-211">After hello account is provisioned, hello end user receives a verification email and needs tooclick hello acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="d9b03-212">若要手動 toocreate 使用者，您需要 toocontact hello [Heroku 用戶端支援小組](https://www.heroku.com/support)。</span><span class="sxs-lookup"><span data-stu-id="d9b03-212">If you need toocreate a user manually, you need toocontact hello [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d9b03-213">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9b03-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d9b03-214">在本節中，您可以授與存取 tooHeroku 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9b03-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHeroku.</span></span>

![指派使用者][200] 

<span data-ttu-id="d9b03-216">**tooassign 許 Simon tooHeroku，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d9b03-216">**tooassign Britta Simon tooHeroku, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9b03-217">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d9b03-219">在 [hello] 應用程式清單中，選取**Heroku**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-219">In hello applications list, select **Heroku**.</span></span>

    ![設定單一登入](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="d9b03-221">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="d9b03-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d9b03-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9b03-223">Click **Add** button.</span></span> <span data-ttu-id="d9b03-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d9b03-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d9b03-226">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="d9b03-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d9b03-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9b03-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9b03-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9b03-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9b03-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d9b03-229">Testing single sign-on</span></span>

<span data-ttu-id="d9b03-230">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="d9b03-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d9b03-231">當您按一下 hello Heroku 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Heroku 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9b03-231">When you click hello Heroku tile in hello Access Panel, you should get automatically signed-on tooyour Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9b03-232">其他資源</span><span class="sxs-lookup"><span data-stu-id="d9b03-232">Additional resources</span></span>

* [<span data-ttu-id="d9b03-233">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9b03-233">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9b03-234">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d9b03-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
