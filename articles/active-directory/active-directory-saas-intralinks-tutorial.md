---
title: "教學課程：Azure Active Directory 與 Intralinks 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Intralinks 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="55a7d-103">教學課程：Azure Active Directory 與 Intralinks 整合</span><span class="sxs-lookup"><span data-stu-id="55a7d-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="55a7d-104">在此教學課程中，您學會如何 toointegrate Intralinks 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="55a7d-104">In this tutorial, you learn how toointegrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55a7d-105">與 Azure AD 整合 Intralinks 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="55a7d-105">Integrating Intralinks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="55a7d-106">您可以控制存取 tooIntralinks Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="55a7d-106">You can control in Azure AD who has access tooIntralinks</span></span>
- <span data-ttu-id="55a7d-107">您可以啟用您的使用者 tooautomatically get 登入 tooIntralinks （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="55a7d-107">You can enable your users tooautomatically get signed-on tooIntralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55a7d-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="55a7d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="55a7d-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="55a7d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55a7d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="55a7d-110">Prerequisites</span></span>

<span data-ttu-id="55a7d-111">tooconfigure Intralinks 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="55a7d-111">tooconfigure Azure AD integration with Intralinks, you need hello following items:</span></span>

- <span data-ttu-id="55a7d-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="55a7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55a7d-113">啟用 Intralinks 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="55a7d-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55a7d-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="55a7d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55a7d-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="55a7d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55a7d-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="55a7d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55a7d-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="55a7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55a7d-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="55a7d-118">Scenario description</span></span>
<span data-ttu-id="55a7d-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55a7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55a7d-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="55a7d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55a7d-121">從 hello 圖庫加入 Intralinks</span><span class="sxs-lookup"><span data-stu-id="55a7d-121">Adding Intralinks from hello gallery</span></span>
2. <span data-ttu-id="55a7d-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="55a7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-hello-gallery"></a><span data-ttu-id="55a7d-123">從 hello 圖庫加入 Intralinks</span><span class="sxs-lookup"><span data-stu-id="55a7d-123">Adding Intralinks from hello gallery</span></span>
<span data-ttu-id="55a7d-124">tooconfigure hello 整合 Intralinks 到 Azure AD，您需要 tooadd Intralinks hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55a7d-124">tooconfigure hello integration of Intralinks into Azure AD, you need tooadd Intralinks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="55a7d-125">**tooadd Intralinks 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="55a7d-125">**tooadd Intralinks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="55a7d-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="55a7d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="55a7d-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="55a7d-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="55a7d-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="55a7d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="55a7d-133">在 [hello] 搜尋方塊中，輸入**Intralinks**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-133">In hello search box, type **Intralinks**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="55a7d-135">在 hello 結果 窗格中，選取  **Intralinks**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55a7d-135">In hello results panel, select **Intralinks**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="55a7d-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="55a7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="55a7d-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Intralinks 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55a7d-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55a7d-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Intralinks 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="55a7d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intralinks is tooa user in Azure AD.</span></span> <span data-ttu-id="55a7d-140">換句話說，Azure AD 使用者與 hello Intralinks 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="55a7d-140">In other words, a link relationship between an Azure AD user and hello related user in Intralinks needs toobe established.</span></span>

<span data-ttu-id="55a7d-141">Intralinks 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="55a7d-141">In Intralinks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="55a7d-142">tooconfigure 及 Intralinks 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="55a7d-142">tooconfigure and test Azure AD single sign-on with Intralinks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="55a7d-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="55a7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="55a7d-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="55a7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="55a7d-145">**[建立測試使用者 Intralinks](#creating-an-intralinks-test-user)**  -toohave 許 Simon Intralinks 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="55a7d-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - toohave a counterpart of Britta Simon in Intralinks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="55a7d-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55a7d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="55a7d-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="55a7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="55a7d-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="55a7d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="55a7d-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Intralinks 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="55a7d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="55a7d-150">**tooconfigure Azure AD 單一登入與 Intralinks，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="55a7d-150">**tooconfigure Azure AD single sign-on with Intralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="55a7d-151">在 Azure 入口網站上 hello hello **Intralinks**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-151">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="55a7d-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55a7d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="55a7d-155">在 hello **Intralinks 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="55a7d-155">On hello **Intralinks Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="55a7d-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="55a7d-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55a7d-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="55a7d-158">This value is not real.</span></span> <span data-ttu-id="55a7d-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="55a7d-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="55a7d-160">請連絡[Intralinks 用戶端支援小組](https://www.intralinks.com/contact-1)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="55a7d-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) tooget this value.</span></span> 
 
4. <span data-ttu-id="55a7d-161">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="55a7d-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="55a7d-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="55a7d-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="55a7d-165">tooconfigure 單一登入上**Intralinks**端，您需要下載 toosend hello**中繼資料 XML** [Intralinks 支援小組](https://www.intralinks.com/contact-1)。</span><span class="sxs-lookup"><span data-stu-id="55a7d-165">tooconfigure single sign-on on **Intralinks** side, you need toosend hello downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="55a7d-166">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="55a7d-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="55a7d-167">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="55a7d-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="55a7d-168">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="55a7d-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="55a7d-169">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55a7d-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="55a7d-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="55a7d-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="55a7d-171">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="55a7d-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="55a7d-173">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="55a7d-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="55a7d-174">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="55a7d-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="55a7d-176">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="55a7d-178">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="55a7d-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="55a7d-180">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="55a7d-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="55a7d-182">a.</span><span class="sxs-lookup"><span data-stu-id="55a7d-182">a.</span></span> <span data-ttu-id="55a7d-183">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55a7d-184">b.</span><span class="sxs-lookup"><span data-stu-id="55a7d-184">b.</span></span> <span data-ttu-id="55a7d-185">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="55a7d-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55a7d-186">c.</span><span class="sxs-lookup"><span data-stu-id="55a7d-186">c.</span></span> <span data-ttu-id="55a7d-187">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="55a7d-188">d.</span><span class="sxs-lookup"><span data-stu-id="55a7d-188">d.</span></span> <span data-ttu-id="55a7d-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="55a7d-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="55a7d-190">建立 Intralinks 測試使用者</span><span class="sxs-lookup"><span data-stu-id="55a7d-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="55a7d-191">在本節中，您要在 Intralinks 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="55a7d-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="55a7d-192">請使用[Intralinks 支援小組](https://www.intralinks.com/contact-1)tooadd hello hello Intralinks 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="55a7d-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) tooadd hello users in hello Intralinks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="55a7d-193">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="55a7d-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="55a7d-194">在本節中，您可以授與存取 tooIntralinks 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="55a7d-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntralinks.</span></span>

![指派使用者][200] 

<span data-ttu-id="55a7d-196">**tooassign 許 Simon tooIntralinks，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="55a7d-196">**tooassign Britta Simon tooIntralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="55a7d-197">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="55a7d-199">在 [hello] 應用程式清單中，選取**Intralinks**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-199">In hello applications list, select **Intralinks**.</span></span>

    ![設定單一登入](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="55a7d-201">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="55a7d-203">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55a7d-203">Click **Add** button.</span></span> <span data-ttu-id="55a7d-204">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="55a7d-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="55a7d-206">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="55a7d-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="55a7d-207">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55a7d-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="55a7d-208">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55a7d-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="55a7d-209">新增 Intralinks VIA 或 Elite 應用程式</span><span class="sxs-lookup"><span data-stu-id="55a7d-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="55a7d-210">Intralinks 使用 hello 相同處理 Nexus 應用程式但不包括其他 Intralinks 應用程式的 SSO 識別身分平台。</span><span class="sxs-lookup"><span data-stu-id="55a7d-210">Intralinks uses hello same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="55a7d-211">因此如果您計劃 toouse 其他 Intralinks 應用程式然後首先您必須使用上述的 hello 程序的一個主要 Intralinks 應用程式的 tooconfigure SSO。</span><span class="sxs-lookup"><span data-stu-id="55a7d-211">So if you plan toouse any other Intralinks application then first you have tooconfigure SSO for one Primary Intralinks application using hello procedure described above.</span></span>

<span data-ttu-id="55a7d-212">之後，您可以依照下列程序 tooadd hello 另一個 Intralinks 應用程式可以利用此主要的應用程式的 SSO 的租用戶中。</span><span class="sxs-lookup"><span data-stu-id="55a7d-212">After that you can follow hello below procedure tooadd another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="55a7d-213">這項功能是可用只有 tooAzure AD Premium SKU 客戶並不適用於免費或基本 SKU 的客戶。</span><span class="sxs-lookup"><span data-stu-id="55a7d-213">This feature is available only tooAzure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="55a7d-214">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="55a7d-214">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="55a7d-216">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-216">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="55a7d-217">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-217">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="55a7d-219">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="55a7d-219">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="55a7d-221">在 [hello] 搜尋方塊中，輸入**Intralinks**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-221">In hello search box, type **Intralinks**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="55a7d-223">在**Intralinks 新增應用程式**執行 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="55a7d-223">On **Intralinks Add app** perform hello following steps:</span></span>

    ![新增 Intralinks VIA 或 Elite 應用程式](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="55a7d-225">a.</span><span class="sxs-lookup"><span data-stu-id="55a7d-225">a.</span></span> <span data-ttu-id="55a7d-226">在**名稱**文字方塊中，輸入適當的 hello 應用程式的名稱，例如**Intralinks 精銳**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-226">In **Name** textbox, enter appropriate name of hello application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="55a7d-227">b.</span><span class="sxs-lookup"><span data-stu-id="55a7d-227">b.</span></span> <span data-ttu-id="55a7d-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="55a7d-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="55a7d-229">在 Azure 入口網站上 hello hello **Intralinks**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-229">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

7. <span data-ttu-id="55a7d-231">在 hello**單一登入**對話方塊中，選取**模式**為**連結登入**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-231">On hello **Single sign-on** dialog, select **Mode** as   **Linked Sign-on**.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="55a7d-233">取得從 hello hello SP 起始 SSO URL [Intralinks 小組](https://www.intralinks.com/contact-1)的 hello 其他 Intralinks 應用程式，並在輸入中**設定登入 URL**如下所示。</span><span class="sxs-lookup"><span data-stu-id="55a7d-233">Get hello hello SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for hello other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![設定單一登入](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="55a7d-235">在 hello 登入 URL 文字方塊中輸入應用程式所使用的使用者 toosign 上 tooyour Intralinks 使用下列模式的 hello hello URL:</span><span class="sxs-lookup"><span data-stu-id="55a7d-235">In hello Sign On URL textbox, type hello URL used by your users toosign-on tooyour Intralinks application using hello following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="55a7d-236">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="55a7d-236">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="55a7d-238">將 hello 應用程式 toouser 或群組指派 hello > 一節中所示**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)**。</span><span class="sxs-lookup"><span data-stu-id="55a7d-238">Assign hello application toouser or groups as shown in hello section **[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="55a7d-239">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="55a7d-239">Testing single sign-on</span></span>

<span data-ttu-id="55a7d-240">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="55a7d-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="55a7d-241">當您按一下的 hello Intralinks 磚 hello 存取面板中時，您應該取得自動登入 tooyour Intralinks 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55a7d-241">When you click hello Intralinks tile in hello Access Panel, you should get automatically signed-on tooyour Intralinks application.</span></span>
<span data-ttu-id="55a7d-242">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="55a7d-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55a7d-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="55a7d-243">Additional resources</span></span>

* [<span data-ttu-id="55a7d-244">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55a7d-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55a7d-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="55a7d-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

