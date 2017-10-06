---
title: "教學課程：Azure Active Directory 與 Direct 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間和直接傳輸。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="6a8db-103">教學課程：Azure Active Directory 與 Direct 整合</span><span class="sxs-lookup"><span data-stu-id="6a8db-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="6a8db-104">在此教學課程中，您學會如何 toointegrate Direct 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6a8db-104">In this tutorial, you learn how toointegrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6a8db-105">整合與 Azure AD 直接可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="6a8db-105">Integrating Direct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6a8db-106">您可以控制存取 tooDirect Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="6a8db-106">You can control in Azure AD who has access tooDirect</span></span>
- <span data-ttu-id="6a8db-107">您可以啟用您的使用者 tooautomatically get 登入 tooDirect （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="6a8db-107">You can enable your users tooautomatically get signed-on tooDirect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6a8db-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6a8db-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="6a8db-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6a8db-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a8db-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6a8db-110">Prerequisites</span></span>

<span data-ttu-id="6a8db-111">Azure AD 整合 tooconfigure 使用 Direct，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="6a8db-111">tooconfigure Azure AD integration with Direct, you need hello following items:</span></span>

- <span data-ttu-id="6a8db-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6a8db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6a8db-113">已啟用 Direct 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6a8db-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6a8db-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="6a8db-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6a8db-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6a8db-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6a8db-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6a8db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6a8db-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="6a8db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6a8db-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6a8db-118">Scenario description</span></span>
<span data-ttu-id="6a8db-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a8db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6a8db-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6a8db-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6a8db-121">加入直接從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="6a8db-121">Adding Direct from hello gallery</span></span>
2. <span data-ttu-id="6a8db-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6a8db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-hello-gallery"></a><span data-ttu-id="6a8db-123">加入直接從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="6a8db-123">Adding Direct from hello gallery</span></span>
<span data-ttu-id="6a8db-124">tooconfigure hello 整合直接到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Direct。</span><span class="sxs-lookup"><span data-stu-id="6a8db-124">tooconfigure hello integration of Direct into Azure AD, you need tooadd Direct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6a8db-125">**tooadd 直接從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6a8db-125">**tooadd Direct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a8db-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6a8db-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6a8db-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6a8db-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6a8db-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a8db-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6a8db-133">在 [hello] 搜尋方塊中，輸入**直接**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-133">In hello search box, type **Direct**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="6a8db-135">在 [hello [結果] 窗格中，選取 [**直接**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a8db-135">In hello results panel, select **Direct**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6a8db-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6a8db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6a8db-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Direct 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a8db-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6a8db-139">單一登入 toowork，Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者直接都 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="6a8db-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Direct is tooa user in Azure AD.</span></span> <span data-ttu-id="6a8db-140">換句話說，Azure AD 使用者與 hello 之間的連結關聯性相關的使用者建立的直接需求 toobe 中。</span><span class="sxs-lookup"><span data-stu-id="6a8db-140">In other words, a link relationship between an Azure AD user and hello related user in Direct needs toobe established.</span></span>

<span data-ttu-id="6a8db-141">在直接、 hello hello 值指派**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6a8db-141">In Direct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6a8db-142">tooconfigure 和測試 Azure AD 單一登入使用 Direct，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="6a8db-142">tooconfigure and test Azure AD single sign-on with Direct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6a8db-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="6a8db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6a8db-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="6a8db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6a8db-145">**[建立直接測試使用者](#creating-a-direct-test-user)** -toohave 許 Simon 中是表示連結的 toohello Azure AD 使用者的直接對應項目。</span><span class="sxs-lookup"><span data-stu-id="6a8db-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - toohave a counterpart of Britta Simon in Direct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6a8db-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a8db-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6a8db-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="6a8db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6a8db-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6a8db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6a8db-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並直接在應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a8db-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="6a8db-150">**tooconfigure Azure AD 單一登入使用 Direct，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6a8db-150">**tooconfigure Azure AD single sign-on with Direct, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a8db-151">在 Azure 入口網站上 hello hello**直接**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-151">In hello Azure portal, on hello **Direct** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6a8db-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a8db-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="6a8db-155">在 [hello**直接網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="6a8db-155">On hello **Direct Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="6a8db-157">在 [hello**識別碼**文字方塊中，型別 hello URL:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="6a8db-157">In hello **Identifier** textbox, type hello URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="6a8db-158">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="6a8db-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="6a8db-160">在 [hello**登入 URL**文字方塊中，型別 hello URL:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="6a8db-160">In hello **Sign-on URL** textbox, type hello URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="6a8db-161">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="6a8db-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="6a8db-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a8db-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="6a8db-165">tooconfigure 單一登入上**直接**端，您需要下載 toosend hello**中繼資料 XML**太[直接支援小組](https://direct4b.com/ja/support.html#inquiry)。</span><span class="sxs-lookup"><span data-stu-id="6a8db-165">tooconfigure single sign-on on **Direct** side, you need toosend hello downloaded **Metadata XML** too[Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="6a8db-166">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="6a8db-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6a8db-167">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="6a8db-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6a8db-168">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6a8db-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6a8db-169">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6a8db-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="6a8db-170">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6a8db-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6a8db-172">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6a8db-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a8db-173">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="6a8db-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6a8db-175">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6a8db-177">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="6a8db-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6a8db-179">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6a8db-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6a8db-181">a.</span><span class="sxs-lookup"><span data-stu-id="6a8db-181">a.</span></span> <span data-ttu-id="6a8db-182">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6a8db-183">b.</span><span class="sxs-lookup"><span data-stu-id="6a8db-183">b.</span></span> <span data-ttu-id="6a8db-184">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="6a8db-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6a8db-185">c.</span><span class="sxs-lookup"><span data-stu-id="6a8db-185">c.</span></span> <span data-ttu-id="6a8db-186">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6a8db-187">d.</span><span class="sxs-lookup"><span data-stu-id="6a8db-187">d.</span></span> <span data-ttu-id="6a8db-188">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6a8db-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="6a8db-189">建立 Direct 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6a8db-189">Creating a Direct test user</span></span>

<span data-ttu-id="6a8db-190">在本節中，您要在 Direct 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6a8db-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="6a8db-191">使用[直接支援小組](https://direct4b.com/ja/support.html#inquiry)hello 直接平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="6a8db-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add hello users in hello Direct platform.</span></span> <span data-ttu-id="6a8db-192">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a8db-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6a8db-193">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="6a8db-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6a8db-194">在本節中，您可以授與存取 tooDirect 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6a8db-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirect.</span></span>

![指派使用者][200] 

<span data-ttu-id="6a8db-196">**tooassign 許 Simon tooDirect，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="6a8db-196">**tooassign Britta Simon tooDirect, perform hello following steps:**</span></span>

1. <span data-ttu-id="6a8db-197">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6a8db-199">在 [hello] 應用程式清單中，選取**直接**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-199">In hello applications list, select **Direct**.</span></span>

    ![設定單一登入](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="6a8db-201">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="6a8db-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6a8db-203">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a8db-203">Click **Add** button.</span></span> <span data-ttu-id="6a8db-204">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6a8db-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6a8db-206">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="6a8db-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6a8db-207">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a8db-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6a8db-208">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6a8db-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6a8db-209">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6a8db-209">Testing single sign-on</span></span>

<span data-ttu-id="6a8db-210">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="6a8db-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="6a8db-211">如果您想在 tootest **IDP 起始模式**:</span><span class="sxs-lookup"><span data-stu-id="6a8db-211">If you wish tootest in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="6a8db-212">當您按一下 hello**直接**以並排顯示 hello 存取面板中，您應該取得自動登入 tooyour**直接**應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a8db-212">When you click hello **Direct** tile in hello Access Panel, you should get automatically signed-on tooyour **Direct** application.</span></span>

2. <span data-ttu-id="6a8db-213">如果您想在 tootest **SP 起始模式**:</span><span class="sxs-lookup"><span data-stu-id="6a8db-213">If you wish tootest in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="6a8db-214">a.</span><span class="sxs-lookup"><span data-stu-id="6a8db-214">a.</span></span> <span data-ttu-id="6a8db-215">按一下 hello**直接**磚 hello 存取面板中，您將無法登入頁面重新導向的 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a8db-215">Click on hello **Direct** tile in hello Access Panel and you will be redirected toohello application sign-on page.</span></span>

    <span data-ttu-id="6a8db-216">b.</span><span class="sxs-lookup"><span data-stu-id="6a8db-216">b.</span></span> <span data-ttu-id="6a8db-217">輸入您`subdomain`中顯示的 hello 文字方塊，然後按 '次へ （下一步）'，而且您應該取得自動登入 tooyour**直接**應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a8db-217">Input your `subdomain` in hello textbox displayed and press '次へ (Next)' and you should get automatically signed-on tooyour **Direct** application .</span></span>
    
<span data-ttu-id="6a8db-218">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6a8db-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6a8db-219">其他資源</span><span class="sxs-lookup"><span data-stu-id="6a8db-219">Additional resources</span></span>

* [<span data-ttu-id="6a8db-220">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6a8db-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6a8db-221">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6a8db-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

