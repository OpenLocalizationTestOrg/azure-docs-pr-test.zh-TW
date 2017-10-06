---
title: "教學課程：Azure Active Directory 與 MobileXpense 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 MobileXpense 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: b9d109f9d4244f8a7eb8b49b0d980cd3df0fc59d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="66732-103">教學課程：Azure Active Directory 與 MobileXpense 整合</span><span class="sxs-lookup"><span data-stu-id="66732-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="66732-104">在此教學課程中，您學會如何 toointegrate MobileXpense 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="66732-104">In this tutorial, you learn how toointegrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66732-105">與 Azure AD 整合 MobileXpense 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="66732-105">Integrating MobileXpense with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66732-106">您可以控制存取 tooMobileXpense Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="66732-106">You can control in Azure AD who has access tooMobileXpense</span></span>
- <span data-ttu-id="66732-107">您可以啟用您的使用者 tooautomatically get 登入 tooMobileXpense （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="66732-107">You can enable your users tooautomatically get signed-on tooMobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66732-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="66732-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="66732-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="66732-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66732-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="66732-110">Prerequisites</span></span>

<span data-ttu-id="66732-111">tooconfigure MobileXpense 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="66732-111">tooconfigure Azure AD integration with MobileXpense, you need hello following items:</span></span>

- <span data-ttu-id="66732-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66732-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66732-113">已啟用 MobileXpense 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66732-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66732-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="66732-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66732-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="66732-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66732-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="66732-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66732-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="66732-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66732-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="66732-118">Scenario description</span></span>
<span data-ttu-id="66732-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66732-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66732-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="66732-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66732-121">從 hello 圖庫加入 MobileXpense</span><span class="sxs-lookup"><span data-stu-id="66732-121">Adding MobileXpense from hello gallery</span></span>
2. <span data-ttu-id="66732-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66732-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-hello-gallery"></a><span data-ttu-id="66732-123">從 hello 圖庫加入 MobileXpense</span><span class="sxs-lookup"><span data-stu-id="66732-123">Adding MobileXpense from hello gallery</span></span>
<span data-ttu-id="66732-124">tooconfigure hello 整合 MobileXpense 到 Azure AD，您需要 tooadd MobileXpense hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66732-124">tooconfigure hello integration of MobileXpense into Azure AD, you need tooadd MobileXpense from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66732-125">**tooadd MobileXpense 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66732-125">**tooadd MobileXpense from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66732-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="66732-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66732-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="66732-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66732-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="66732-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="66732-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="66732-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="66732-133">在 [hello] 搜尋方塊中，輸入**MobileXpense**。</span><span class="sxs-lookup"><span data-stu-id="66732-133">In hello search box, type **MobileXpense**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="66732-135">在 [hello [結果] 窗格中，選取 [ **MobileXpense**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66732-135">In hello results panel, select **MobileXpense**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66732-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66732-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66732-138">在本節中，您會以測試使用者 "Britta Simon" 的身分，設定及測試 Azure AD 與 MobileXpense 的單一登入。</span><span class="sxs-lookup"><span data-stu-id="66732-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="66732-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 MobileXpense 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="66732-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MobileXpense is tooa user in Azure AD.</span></span> <span data-ttu-id="66732-140">換句話說，Azure AD 使用者與 hello MobileXpense 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="66732-140">In other words, a link relationship between an Azure AD user and hello related user in MobileXpense needs toobe established.</span></span>

<span data-ttu-id="66732-141">MobileXpense 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="66732-141">In MobileXpense, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66732-142">tooconfigure 及 MobileXpense 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="66732-142">tooconfigure and test Azure AD single sign-on with MobileXpense, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66732-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="66732-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66732-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="66732-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66732-145">**[建立測試使用者 MobileXpense](#creating-a-mobilexpense-test-user) ** -toohave 許 Simon MobileXpense 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="66732-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - toohave a counterpart of Britta Simon in MobileXpense that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="66732-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66732-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66732-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="66732-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66732-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66732-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66732-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 MobileXpense 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="66732-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="66732-150">**tooconfigure Azure AD 單一登入與 MobileXpense，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66732-150">**tooconfigure Azure AD single sign-on with MobileXpense, perform hello following steps:**</span></span>

1. <span data-ttu-id="66732-151">在 Azure 入口網站上 hello hello **MobileXpense**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="66732-151">In hello Azure portal, on hello **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="66732-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66732-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="66732-155">在 [hello **MobileXpense 網域和 Url**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="66732-155">On hello **MobileXpense Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="66732-157">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="66732-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="66732-158">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="66732-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="66732-160">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello::`https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="66732-160">In hello **Sign-on URL** textbox, type a URL using hello following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="66732-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="66732-161">These values are not real.</span></span> <span data-ttu-id="66732-162">Hello 實際的回覆 URL 和登入 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="66732-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="66732-163">請連絡[MobileXpense 用戶端支援小組](http://www.mobilexpense.net/contact)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="66732-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) tooget these values.</span></span> 

5. <span data-ttu-id="66732-164">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="66732-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="66732-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="66732-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="66732-168">tooconfigure 單一登入上**MobileXpense**端，您需要下載 toosend hello**中繼資料 XML**太[MobileXpense 支援小組](http://www.mobilexpense.net/contact)。</span><span class="sxs-lookup"><span data-stu-id="66732-168">tooconfigure single sign-on on **MobileXpense** side, you need toosend hello downloaded **Metadata XML** too[MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="66732-169">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="66732-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66732-170">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="66732-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66732-171">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66732-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66732-172">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="66732-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="66732-173">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="66732-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="66732-175">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66732-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66732-176">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="66732-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66732-178">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="66732-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66732-180">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="66732-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66732-182">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="66732-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66732-184">a.</span><span class="sxs-lookup"><span data-stu-id="66732-184">a.</span></span> <span data-ttu-id="66732-185">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="66732-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66732-186">b.</span><span class="sxs-lookup"><span data-stu-id="66732-186">b.</span></span> <span data-ttu-id="66732-187">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="66732-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66732-188">c.</span><span class="sxs-lookup"><span data-stu-id="66732-188">c.</span></span> <span data-ttu-id="66732-189">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="66732-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66732-190">d.</span><span class="sxs-lookup"><span data-stu-id="66732-190">d.</span></span> <span data-ttu-id="66732-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="66732-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="66732-192">建立 MobileXpense 測試使用者</span><span class="sxs-lookup"><span data-stu-id="66732-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="66732-193">在本節中，您要在 MobileXpense 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="66732-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="66732-194">使用[MobileXpense 支援小組](http://www.mobilexpense.net/contact)hello MobileXpense 平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="66732-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add hello users in hello MobileXpense platform.</span></span> <span data-ttu-id="66732-195">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="66732-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="66732-196">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="66732-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="66732-197">在本節中，您可以授與存取 tooMobileXpense 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66732-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMobileXpense.</span></span>

![指派使用者][200] 

<span data-ttu-id="66732-199">**tooassign 許 Simon tooMobileXpense，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66732-199">**tooassign Britta Simon tooMobileXpense, perform hello following steps:**</span></span>

1. <span data-ttu-id="66732-200">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="66732-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="66732-202">在 [hello] 應用程式清單中，選取**MobileXpense**。</span><span class="sxs-lookup"><span data-stu-id="66732-202">In hello applications list, select **MobileXpense**.</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="66732-204">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="66732-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="66732-206">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66732-206">Click **Add** button.</span></span> <span data-ttu-id="66732-207">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="66732-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="66732-209">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="66732-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66732-210">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66732-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66732-211">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66732-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66732-212">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="66732-212">Testing single sign-on</span></span>

<span data-ttu-id="66732-213">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="66732-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66732-214">當您按一下 hello MobileXpense 磚 hello 存取面板中的時，您應該取得自動登入 tooyour MobileXpense 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66732-214">When you click hello MobileXpense tile in hello Access Panel, you should get automatically signed-on tooyour MobileXpense application.</span></span>
<span data-ttu-id="66732-215">如需存取面板的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="66732-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="66732-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="66732-216">Additional resources</span></span>

* [<span data-ttu-id="66732-217">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66732-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66732-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="66732-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png

