---
title: "教學課程：Azure Active Directory 與 Neota Logic Studio 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Neota 邏輯 Studio 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: a479ee49618de8275132dbc2c21a8ef723d92d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="aa707-103">教學課程：Azure Active Directory 與 Neota Logic Studio 整合</span><span class="sxs-lookup"><span data-stu-id="aa707-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="aa707-104">在此教學課程中，您學會如何 toointegrate Neota 邏輯 Studio 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="aa707-104">In this tutorial, you learn how toointegrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa707-105">與 Azure AD 整合 Neota 邏輯 Studio 為您提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="aa707-105">Integrating Neota Logic Studio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aa707-106">您可以控制存取 tooNeota 邏輯 Studio Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="aa707-106">You can control in Azure AD who has access tooNeota Logic Studio</span></span>
- <span data-ttu-id="aa707-107">您可以啟用您的使用者 tooautomatically get 登入 tooNeota （單一登入） 的邏輯 Studio 使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="aa707-107">You can enable your users tooautomatically get signed-on tooNeota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa707-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="aa707-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aa707-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。</span><span class="sxs-lookup"><span data-stu-id="aa707-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="aa707-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="aa707-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa707-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="aa707-111">Prerequisites</span></span>

<span data-ttu-id="aa707-112">tooconfigure Neota 邏輯 Studio 中的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="aa707-112">tooconfigure Azure AD integration with Neota Logic Studio, you need hello following items:</span></span>

- <span data-ttu-id="aa707-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="aa707-113">An Azure AD subscription</span></span>
- <span data-ttu-id="aa707-114">已啟用 Neota Logic Studio 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="aa707-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa707-115">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="aa707-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa707-116">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="aa707-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa707-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="aa707-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa707-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="aa707-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa707-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="aa707-119">Scenario description</span></span>

<span data-ttu-id="aa707-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="aa707-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa707-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="aa707-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa707-122">從 hello 圖庫加入 Neota 邏輯 Studio</span><span class="sxs-lookup"><span data-stu-id="aa707-122">Adding Neota Logic Studio from hello gallery</span></span>
2. <span data-ttu-id="aa707-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="aa707-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-hello-gallery"></a><span data-ttu-id="aa707-124">從 hello 圖庫加入 Neota 邏輯 Studio</span><span class="sxs-lookup"><span data-stu-id="aa707-124">Adding Neota Logic Studio from hello gallery</span></span>

<span data-ttu-id="aa707-125">tooconfigure hello 整合 Neota 邏輯 Studio 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Neota 邏輯 Studio。</span><span class="sxs-lookup"><span data-stu-id="aa707-125">tooconfigure hello integration of Neota Logic Studio into Azure AD, you need tooadd Neota Logic Studio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aa707-126">**tooadd Neota 邏輯 Studio 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="aa707-126">**tooadd Neota Logic Studio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa707-127">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="aa707-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa707-129">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="aa707-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aa707-130">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="aa707-130">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="aa707-132">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="aa707-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="aa707-134">在 [hello] 搜尋方塊中，輸入**Neota 邏輯 Studio**。</span><span class="sxs-lookup"><span data-stu-id="aa707-134">In hello search box, type **Neota Logic Studio**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="aa707-136">在 hello 結果 窗格中，選取  **Neota 邏輯 Studio**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa707-136">In hello results panel, select **Neota Logic Studio**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa707-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="aa707-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="aa707-139">在本節中，您會以測試使用者 Britta Simon 的身分，設定及測試 Azure AD 與 Neota Logic Studio 的單一登入。</span><span class="sxs-lookup"><span data-stu-id="aa707-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aa707-140">單一登入 toowork，Azure AD 需要 tooknow Neota 邏輯 Studio 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="aa707-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Neota Logic Studio is tooa user in Azure AD.</span></span> <span data-ttu-id="aa707-141">換句話說，Azure AD 使用者與 hello Neota 邏輯 Studio 中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="aa707-141">In other words, a link relationship between an Azure AD user and hello related user in Neota Logic Studio needs toobe established.</span></span>

<span data-ttu-id="aa707-142">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Neota 邏輯 Studio 中。</span><span class="sxs-lookup"><span data-stu-id="aa707-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="aa707-143">tooconfigure 及 Neota 邏輯 Studio 中的 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="aa707-143">tooconfigure and test Azure AD single sign-on with Neota Logic Studio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aa707-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="aa707-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aa707-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="aa707-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa707-146">**[建立測試使用者 Neota 邏輯 Studio](#creating-a-neota-logic-studio-test-user)**  -toohave 許 Simon Neota 邏輯 Studio 連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="aa707-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - toohave a counterpart of Britta Simon in Neota Logic Studio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa707-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="aa707-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa707-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="aa707-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa707-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="aa707-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa707-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Neota 邏輯 Studio 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="aa707-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="aa707-151">**tooconfigure Azure AD 單一登入與 Neota 邏輯 Studio 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="aa707-151">**tooconfigure Azure AD single sign-on with Neota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa707-152">在 Azure 入口網站上 hello hello **Neota 邏輯 Studio**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="aa707-152">In hello Azure portal, on hello **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="aa707-154">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="aa707-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="aa707-156">在 hello **Neota 邏輯 Studio 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="aa707-156">On hello **Neota Logic Studio Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="aa707-158">a.</span><span class="sxs-lookup"><span data-stu-id="aa707-158">a.</span></span> <span data-ttu-id="aa707-159">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="aa707-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="aa707-160">b.</span><span class="sxs-lookup"><span data-stu-id="aa707-160">b.</span></span> <span data-ttu-id="aa707-161">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="aa707-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="aa707-162">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="aa707-162">These values are not hello real.</span></span> <span data-ttu-id="aa707-163">更新這些值與實際的 hello 登入 URL （& s） 的識別項。</span><span class="sxs-lookup"><span data-stu-id="aa707-163">Update these values with hello actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="aa707-164">這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="aa707-164">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="aa707-165">請連絡[Neota 邏輯 Studio 用戶端支援小組](https://www.neotalogic.com/contact-us/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="aa707-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="aa707-166">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="aa707-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="aa707-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="aa707-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aa707-170">設定應用程式，請連絡 SSO tooget [Neota 邏輯 Studio 支援](https://www.neotalogic.com/contact-us/)小組，並提供給他們與下載**中繼資料 XML**檔案。</span><span class="sxs-lookup"><span data-stu-id="aa707-170">tooget SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="aa707-171">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="aa707-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aa707-172">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="aa707-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aa707-173">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa707-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa707-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="aa707-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa707-175">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="aa707-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="aa707-177">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="aa707-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa707-178">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="aa707-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa707-180">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="aa707-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa707-182">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="aa707-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa707-184">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="aa707-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa707-186">a.</span><span class="sxs-lookup"><span data-stu-id="aa707-186">a.</span></span> <span data-ttu-id="aa707-187">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="aa707-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa707-188">b.</span><span class="sxs-lookup"><span data-stu-id="aa707-188">b.</span></span> <span data-ttu-id="aa707-189">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="aa707-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa707-190">c.</span><span class="sxs-lookup"><span data-stu-id="aa707-190">c.</span></span> <span data-ttu-id="aa707-191">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="aa707-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aa707-192">d.</span><span class="sxs-lookup"><span data-stu-id="aa707-192">d.</span></span> <span data-ttu-id="aa707-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="aa707-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="aa707-194">建立 Neota Logic Studio 測試使用者</span><span class="sxs-lookup"><span data-stu-id="aa707-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="aa707-195">在本節中，您要在 Neota Logic Studio 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="aa707-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="aa707-196">使用[Neota 邏輯 Studio 用戶端支援小組](https://www.neotalogic.com/contact-us/)hello Neota 邏輯 Studio 平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="aa707-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add hello users in hello Neota Logic Studio platform.</span></span> <span data-ttu-id="aa707-197">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="aa707-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aa707-198">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="aa707-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aa707-199">在本節中，您可以授與存取 tooNeota 邏輯 Studio 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="aa707-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNeota Logic Studio.</span></span>

![指派使用者][200] 

<span data-ttu-id="aa707-201">**tooassign 許 Simon tooNeota 邏輯 Studio 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="aa707-201">**tooassign Britta Simon tooNeota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa707-202">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="aa707-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="aa707-204">在 [hello] 應用程式清單中，選取**Neota 邏輯 Studio**。</span><span class="sxs-lookup"><span data-stu-id="aa707-204">In hello applications list, select **Neota Logic Studio**.</span></span>

    ![設定單一登入](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="aa707-206">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="aa707-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="aa707-208">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="aa707-208">Click **Add** button.</span></span> <span data-ttu-id="aa707-209">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="aa707-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="aa707-211">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="aa707-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aa707-212">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="aa707-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa707-213">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="aa707-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa707-214">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="aa707-214">Testing single sign-on</span></span>

<span data-ttu-id="aa707-215">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="aa707-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aa707-216">按一下 hello Neota 邏輯 Studio 磚在 hello 存取面板，您將會重新導向的 tooOrganization 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="aa707-216">Click hello Neota Logic Studio tile in hello Access Panel, you will be redirected tooOrganization sign-on page.</span></span> <span data-ttu-id="aa707-217">後成功登入，您就無法登入 tooyour Neota 邏輯 Studio 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa707-217">After successful login, you will be signed-on tooyour Neota Logic Studio application.</span></span> <span data-ttu-id="aa707-218">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="aa707-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="aa707-219">如需 hello 存取面板的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="aa707-219">For more information about hello Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="aa707-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="aa707-220">Additional resources</span></span>

* [<span data-ttu-id="aa707-221">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aa707-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa707-222">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="aa707-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

