---
title: "教學課程：Azure Active Directory 與 itslearning 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 itslearning 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 4ee6c8d450cc3972a87da67fc79890473cfa498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="8e063-103">教學課程：Azure Active Directory 與 itslearning 整合</span><span class="sxs-lookup"><span data-stu-id="8e063-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="8e063-104">在此教學課程中，您學會如何 toointegrate itslearning 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8e063-104">In this tutorial, you learn how toointegrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e063-105">與 Azure AD 整合 itslearning 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="8e063-105">Integrating itslearning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8e063-106">您可以控制存取 tooitslearning Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="8e063-106">You can control in Azure AD who has access tooitslearning</span></span>
- <span data-ttu-id="8e063-107">您可以啟用您的使用者 tooautomatically get 登入 tooitslearning （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="8e063-107">You can enable your users tooautomatically get signed-on tooitslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e063-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8e063-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8e063-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8e063-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e063-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8e063-110">Prerequisites</span></span>

<span data-ttu-id="8e063-111">tooconfigure itslearning 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="8e063-111">tooconfigure Azure AD integration with itslearning, you need hello following items:</span></span>

- <span data-ttu-id="8e063-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8e063-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e063-113">啟用 itslearning 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8e063-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e063-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="8e063-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e063-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8e063-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e063-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8e063-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e063-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="8e063-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e063-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8e063-118">Scenario description</span></span>
<span data-ttu-id="8e063-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8e063-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e063-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8e063-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e063-121">從 hello 圖庫加入 itslearning</span><span class="sxs-lookup"><span data-stu-id="8e063-121">Adding itslearning from hello gallery</span></span>
2. <span data-ttu-id="8e063-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8e063-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-hello-gallery"></a><span data-ttu-id="8e063-123">從 hello 圖庫加入 itslearning</span><span class="sxs-lookup"><span data-stu-id="8e063-123">Adding itslearning from hello gallery</span></span>
<span data-ttu-id="8e063-124">tooconfigure hello 整合 itslearning 到 Azure AD，您需要 tooadd itslearning hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8e063-124">tooconfigure hello integration of itslearning into Azure AD, you need tooadd itslearning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8e063-125">**tooadd itslearning 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8e063-125">**tooadd itslearning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e063-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8e063-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e063-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8e063-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8e063-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8e063-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8e063-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8e063-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8e063-133">在 [hello] 搜尋方塊中，輸入**itslearning**。</span><span class="sxs-lookup"><span data-stu-id="8e063-133">In hello search box, type **itslearning**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_search.png)

5. <span data-ttu-id="8e063-135">在 hello 結果 窗格中，選取  **itslearning**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8e063-135">In hello results panel, select **itslearning**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e063-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8e063-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e063-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 itslearning 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8e063-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8e063-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 itslearning 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="8e063-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in itslearning is tooa user in Azure AD.</span></span> <span data-ttu-id="8e063-140">換句話說，Azure AD 使用者與 hello itslearning 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="8e063-140">In other words, a link relationship between an Azure AD user and hello related user in itslearning needs toobe established.</span></span>

<span data-ttu-id="8e063-141">Itslearning 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8e063-141">In itslearning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8e063-142">tooconfigure 及 itslearning 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="8e063-142">tooconfigure and test Azure AD single sign-on with itslearning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8e063-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="8e063-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8e063-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="8e063-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e063-145">**[建立測試使用者 itslearning](#creating-an-itslearning-test-user)**  -toohave 是連結的 toohello Azure AD 使用者表示法的 itslearning 的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="8e063-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - toohave a counterpart of Britta Simon in itslearning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e063-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8e063-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e063-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="8e063-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e063-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8e063-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e063-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 itslearning 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8e063-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="8e063-150">**tooconfigure Azure AD 單一登入與 itslearning，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8e063-150">**tooconfigure Azure AD single sign-on with itslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e063-151">在 Azure 入口網站上 hello hello **itslearning**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="8e063-151">In hello Azure portal, on hello **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8e063-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8e063-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_samlbase.png)

3. <span data-ttu-id="8e063-155">在 hello **itslearning 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e063-155">On hello **itslearning Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="8e063-157">a.</span><span class="sxs-lookup"><span data-stu-id="8e063-157">a.</span></span> <span data-ttu-id="8e063-158">在 hello**登入 URL**文字方塊中，輸入與 URL:</span><span class="sxs-lookup"><span data-stu-id="8e063-158">In hello **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="8e063-159">b.</span><span class="sxs-lookup"><span data-stu-id="8e063-159">b.</span></span> <span data-ttu-id="8e063-160">在 hello**識別碼**文字方塊中，輸入 URL:`urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="8e063-160">In hello **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

4. <span data-ttu-id="8e063-161">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="8e063-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_certificate.png) 

5. <span data-ttu-id="8e063-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8e063-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-itslearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e063-165">tooconfigure 單一登入上**itslearning**端，您需要下載 toosend hello**中繼資料 XML**太[itslearning 支援小組](mailto:support@itslearning.com)。</span><span class="sxs-lookup"><span data-stu-id="8e063-165">tooconfigure single sign-on on **itslearning** side, you need toosend hello downloaded **Metadata XML** too[itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="8e063-166">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="8e063-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8e063-167">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="8e063-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8e063-168">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="8e063-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8e063-169">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e063-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e063-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8e063-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e063-171">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8e063-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8e063-173">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8e063-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e063-174">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8e063-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itslearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e063-176">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="8e063-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itslearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e063-178">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="8e063-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itslearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e063-180">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e063-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e063-182">a.</span><span class="sxs-lookup"><span data-stu-id="8e063-182">a.</span></span> <span data-ttu-id="8e063-183">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8e063-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e063-184">b.</span><span class="sxs-lookup"><span data-stu-id="8e063-184">b.</span></span> <span data-ttu-id="8e063-185">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="8e063-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e063-186">c.</span><span class="sxs-lookup"><span data-stu-id="8e063-186">c.</span></span> <span data-ttu-id="8e063-187">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="8e063-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8e063-188">d.</span><span class="sxs-lookup"><span data-stu-id="8e063-188">d.</span></span> <span data-ttu-id="8e063-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8e063-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="8e063-190">建立 itslearning 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8e063-190">Creating an itslearning test user</span></span>

<span data-ttu-id="8e063-191">在本節中，您要在 itslearning 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8e063-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="8e063-192">使用[itslearning 用戶端支援小組](mailto:support@itslearning.com)hello itslearning 平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="8e063-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add hello users in hello itslearning platform.</span></span> <span data-ttu-id="8e063-193">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="8e063-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8e063-194">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="8e063-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8e063-195">在本節中，您可以授與存取 tooitslearning 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8e063-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooitslearning.</span></span>

![指派使用者][200] 

<span data-ttu-id="8e063-197">**tooassign 許 Simon tooitslearning，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8e063-197">**tooassign Britta Simon tooitslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="8e063-198">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8e063-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8e063-200">在 [hello] 應用程式清單中，選取**itslearning**。</span><span class="sxs-lookup"><span data-stu-id="8e063-200">In hello applications list, select **itslearning**.</span></span>

    ![設定單一登入](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_app.png) 

3. <span data-ttu-id="8e063-202">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="8e063-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8e063-204">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8e063-204">Click **Add** button.</span></span> <span data-ttu-id="8e063-205">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8e063-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8e063-207">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="8e063-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8e063-208">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8e063-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e063-209">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8e063-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e063-210">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8e063-210">Testing single sign-on</span></span>

<span data-ttu-id="8e063-211">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="8e063-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8e063-212">當您按一下 hello itslearning 磚 hello 存取面板中的時，您應該取得 itslearning 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="8e063-212">When you click hello itslearning tile in hello Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="8e063-213">按一下**登入 Windows Azure ACS1** hello 應用程式的成功登入。</span><span class="sxs-lookup"><span data-stu-id="8e063-213">Click **Log in with Windows Azure ACS1** for successful login into hello application.</span></span>

  ![登入](./media/active-directory-saas-itslearning-tutorial/login.png)

<span data-ttu-id="8e063-215">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="8e063-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e063-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="8e063-216">Additional resources</span></span>

* [<span data-ttu-id="8e063-217">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e063-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e063-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8e063-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_203.png

