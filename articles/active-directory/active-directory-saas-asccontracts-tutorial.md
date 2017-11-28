---
title: "教學課程：Azure Active Directory 與 ASC Contracts 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ASC 合約之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 8320af8acfda3e3d37e589c9887cd697d5ab651c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="c0956-103">教學課程：Azure Active Directory 與 ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="c0956-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="c0956-104">在此教學課程中，您學會如何與 Azure Active Directory (Azure AD) 的 toointegrate ASC 合約。</span><span class="sxs-lookup"><span data-stu-id="c0956-104">In this tutorial, you learn how toointegrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c0956-105">與 Azure AD 整合 ASC 合約可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="c0956-105">Integrating ASC Contracts with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c0956-106">您可以控制可以存取 Azure AD 中 tooASC 合約</span><span class="sxs-lookup"><span data-stu-id="c0956-106">You can control in Azure AD who has access tooASC Contracts</span></span>
- <span data-ttu-id="c0956-107">您可以啟用使用者 tooautomatically 取得其 Azure AD 帳戶的登入 tooASC 合約 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="c0956-107">You can enable your users tooautomatically get signed-on tooASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c0956-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c0956-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c0956-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c0956-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0956-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c0956-110">Prerequisites</span></span>

<span data-ttu-id="c0956-111">tooconfigure ASC 合約與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c0956-111">tooconfigure Azure AD integration with ASC Contracts, you need hello following items:</span></span>

- <span data-ttu-id="c0956-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c0956-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c0956-113">啟用 ASC Contracts 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c0956-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c0956-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c0956-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c0956-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c0956-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c0956-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c0956-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c0956-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c0956-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c0956-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c0956-118">Scenario description</span></span>
<span data-ttu-id="c0956-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0956-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c0956-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c0956-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c0956-121">從 hello 圖庫加入 ASC 合約</span><span class="sxs-lookup"><span data-stu-id="c0956-121">Adding ASC Contracts from hello gallery</span></span>
2. <span data-ttu-id="c0956-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c0956-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-hello-gallery"></a><span data-ttu-id="c0956-123">從 hello 圖庫加入 ASC 合約</span><span class="sxs-lookup"><span data-stu-id="c0956-123">Adding ASC Contracts from hello gallery</span></span>
<span data-ttu-id="c0956-124">tooconfigure hello 整合 ASC 合約到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd ASC 合約。</span><span class="sxs-lookup"><span data-stu-id="c0956-124">tooconfigure hello integration of ASC Contracts into Azure AD, you need tooadd ASC Contracts from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c0956-125">**tooadd ASC 合約從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c0956-125">**tooadd ASC Contracts from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0956-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c0956-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c0956-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c0956-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c0956-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c0956-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c0956-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0956-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c0956-133">在 [hello] 搜尋方塊中，輸入**ASC 合約**。</span><span class="sxs-lookup"><span data-stu-id="c0956-133">In hello search box, type **ASC Contracts**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="c0956-135">在 hello 結果 窗格中，選取  **ASC 合約**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0956-135">In hello results panel, select **ASC Contracts**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c0956-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c0956-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c0956-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ASC Contracts 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0956-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c0956-139">單一登入 toowork，Azure AD 需要 tooknow ASC 合約中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c0956-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ASC Contracts is tooa user in Azure AD.</span></span> <span data-ttu-id="c0956-140">換句話說，Azure AD 使用者與 hello ASC 合約中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="c0956-140">In other words, a link relationship between an Azure AD user and hello related user in ASC Contracts needs toobe established.</span></span>

<span data-ttu-id="c0956-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** ASC 合約中。</span><span class="sxs-lookup"><span data-stu-id="c0956-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ASC Contracts.</span></span>

<span data-ttu-id="c0956-142">tooconfigure 及測試 Azure AD 單一登入與 ASC 合約，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c0956-142">tooconfigure and test Azure AD single sign-on with ASC Contracts, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c0956-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c0956-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c0956-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c0956-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c0956-145">**[建立測試使用者 ASC 合約](#creating-an-asc-contracts-test-user)** -toohave 許 Simon ASC 合約所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="c0956-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - toohave a counterpart of Britta Simon in ASC Contracts that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c0956-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0956-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c0956-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c0956-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c0956-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c0956-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c0956-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 ASC 合約應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0956-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="c0956-150">**tooconfigure Azure AD 單一登入使用 ASC 的合約，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c0956-150">**tooconfigure Azure AD single sign-on with ASC Contracts, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0956-151">在 Azure 入口網站上 hello hello **ASC 合約**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c0956-151">In hello Azure portal, on hello **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c0956-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c0956-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="c0956-155">在 hello **ASC 合約網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c0956-155">On hello **ASC Contracts Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="c0956-157">a.</span><span class="sxs-lookup"><span data-stu-id="c0956-157">a.</span></span> <span data-ttu-id="c0956-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="c0956-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="c0956-159">b.</span><span class="sxs-lookup"><span data-stu-id="c0956-159">b.</span></span> <span data-ttu-id="c0956-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span><span class="sxs-lookup"><span data-stu-id="c0956-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c0956-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c0956-161">These values are not real.</span></span> <span data-ttu-id="c0956-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="c0956-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c0956-163">請連絡 ASC 網路 Inc.(ASC) 團隊**613.599.6178** tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="c0956-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** tooget these values.</span></span>

4. <span data-ttu-id="c0956-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="c0956-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="c0956-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0956-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c0956-168">tooconfigure 單一登入上**ASC 合約**側邊，請呼叫在 ASC 網路 Inc.(ASC) 支援**613.599.6178**並提供給他們，以下載 hello**中繼資料 XML**。</span><span class="sxs-lookup"><span data-stu-id="c0956-168">tooconfigure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with hello downloaded **Metadata XML**.</span></span> <span data-ttu-id="c0956-169">這些設定 toohave hello SAML SSO 連線兩端上正確設定此應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0956-169">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c0956-170">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="c0956-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c0956-171">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="c0956-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c0956-172">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c0956-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c0956-173">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c0956-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="c0956-174">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c0956-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c0956-176">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c0956-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0956-177">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c0956-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c0956-179">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="c0956-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c0956-181">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="c0956-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c0956-183">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c0956-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c0956-185">a.</span><span class="sxs-lookup"><span data-stu-id="c0956-185">a.</span></span> <span data-ttu-id="c0956-186">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c0956-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c0956-187">b.</span><span class="sxs-lookup"><span data-stu-id="c0956-187">b.</span></span> <span data-ttu-id="c0956-188">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c0956-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c0956-189">c.</span><span class="sxs-lookup"><span data-stu-id="c0956-189">c.</span></span> <span data-ttu-id="c0956-190">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c0956-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c0956-191">d.</span><span class="sxs-lookup"><span data-stu-id="c0956-191">d.</span></span> <span data-ttu-id="c0956-192">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c0956-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="c0956-193">建立 ASC Contracts 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c0956-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="c0956-194">ASC 網路 Inc.(ASC) 支援團隊處理**613.599.6178** tooget hello 使用者加入 hello ASC 合約平台。</span><span class="sxs-lookup"><span data-stu-id="c0956-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** tooget hello users added in hello ASC Contracts platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c0956-195">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="c0956-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c0956-196">在本節中，以啟用 Azure 單一登入許 Simon toouse tooASC 合約授與存取權。</span><span class="sxs-lookup"><span data-stu-id="c0956-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooASC Contracts.</span></span>

![指派使用者][200] 

<span data-ttu-id="c0956-198">**tooassign 許 Simon tooASC 合約中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c0956-198">**tooassign Britta Simon tooASC Contracts, perform hello following steps:**</span></span>

1. <span data-ttu-id="c0956-199">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c0956-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c0956-201">在 [hello] 應用程式清單中，選取**ASC 合約**。</span><span class="sxs-lookup"><span data-stu-id="c0956-201">In hello applications list, select **ASC Contracts**.</span></span>

    ![設定單一登入](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="c0956-203">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c0956-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c0956-205">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0956-205">Click **Add** button.</span></span> <span data-ttu-id="c0956-206">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c0956-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c0956-208">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="c0956-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c0956-209">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0956-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c0956-210">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c0956-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c0956-211">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c0956-211">Testing single sign-on</span></span>

<span data-ttu-id="c0956-212">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="c0956-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c0956-213">當您按一下的 hello ASC 合約磚 hello 存取面板中時，您應該取得自動登入 tooyour ASC 合約應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0956-213">When you click hello ASC Contracts tile in hello Access Panel, you should get automatically signed-on tooyour ASC Contracts application.</span></span> <span data-ttu-id="c0956-214">如需存取面板的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="c0956-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="c0956-215">[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="c0956-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0956-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="c0956-216">Additional resources</span></span>

* [<span data-ttu-id="c0956-217">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c0956-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c0956-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c0956-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

