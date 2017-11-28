---
title: "教學課程： Azure Active Directory 與 BC hello 雲端中的整合 |Microsoft 文件"
description: "了解如何 tooconfigure 單一登入 Azure Active Directory 與 BC 中的之間 hello 雲端。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: e81ffb522b2c96c7e9b2919abd8d3b199c295eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-hello-cloud"></a><span data-ttu-id="51a31-103">教學課程： Azure Active Directory 與 BC hello 雲端中的整合</span><span class="sxs-lookup"><span data-stu-id="51a31-103">Tutorial: Azure Active Directory integration with BC in hello Cloud</span></span>

<span data-ttu-id="51a31-104">在此教學課程中，您學會如何 toointegrate BC 中的 hello 與 Azure Active Directory (Azure AD) 的雲端。</span><span class="sxs-lookup"><span data-stu-id="51a31-104">In this tutorial, you learn how toointegrate BC in hello Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51a31-105">在 hello 雲端與 Azure AD 中整合 BC 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="51a31-105">Integrating BC in hello Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="51a31-106">您可以控制存取 tooBC hello 雲端中的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="51a31-106">You can control in Azure AD who has access tooBC in hello Cloud</span></span>
- <span data-ttu-id="51a31-107">您可以啟用您的使用者 tooautomatically get 登入 tooBC 其 Azure AD 帳戶與 hello （單一登入） 的雲端中</span><span class="sxs-lookup"><span data-stu-id="51a31-107">You can enable your users tooautomatically get signed-on tooBC in hello Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="51a31-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="51a31-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="51a31-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="51a31-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51a31-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="51a31-110">Prerequisites</span></span>

<span data-ttu-id="51a31-111">tooconfigure 與 BC hello 雲端中的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="51a31-111">tooconfigure Azure AD integration with BC in hello Cloud, you need hello following items:</span></span>

- <span data-ttu-id="51a31-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="51a31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51a31-113">在 啟用訂用帳戶的 hello 雲端的單一登 BC</span><span class="sxs-lookup"><span data-stu-id="51a31-113">A BC in hello Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51a31-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="51a31-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51a31-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="51a31-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51a31-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="51a31-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51a31-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="51a31-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51a31-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="51a31-118">Scenario description</span></span>
<span data-ttu-id="51a31-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="51a31-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51a31-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="51a31-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51a31-121">在 hello 從 hello 組件庫的雲端中加入 BC</span><span class="sxs-lookup"><span data-stu-id="51a31-121">Adding BC in hello Cloud from hello gallery</span></span>
2. <span data-ttu-id="51a31-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="51a31-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-hello-cloud-from-hello-gallery"></a><span data-ttu-id="51a31-123">在 hello 從 hello 組件庫的雲端中加入 BC</span><span class="sxs-lookup"><span data-stu-id="51a31-123">Adding BC in hello Cloud from hello gallery</span></span>
<span data-ttu-id="51a31-124">tooconfigure hello BC hello 雲端至 Azure AD 中整合，您需要 tooadd BC hello 雲端 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="51a31-124">tooconfigure hello integration of BC in hello Cloud into Azure AD, you need tooadd BC in hello Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="51a31-125">**tooadd BC hello hello 圖庫中，從雲端中的執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="51a31-125">**tooadd BC in hello Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="51a31-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="51a31-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="51a31-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="51a31-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="51a31-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="51a31-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="51a31-131">tooadd 新應用程式中，按一下 **新增**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="51a31-131">tooadd new application, click **Add** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="51a31-133">在 [hello] 搜尋方塊中，輸入**BC 中 hello 雲端**。</span><span class="sxs-lookup"><span data-stu-id="51a31-133">In hello search box, type **BC in hello Cloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="51a31-135">在 hello 結果 窗格中，選取  **BC hello 雲端中的**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51a31-135">In hello results panel, select **BC in hello Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="51a31-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="51a31-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="51a31-138">在本節中，設定並測試 Azure AD 單一登入與 BC hello 稱為 「 許 Simon。 「 測試使用者為基礎的雲端中</span><span class="sxs-lookup"><span data-stu-id="51a31-138">In this section, you configure and test Azure AD single sign-on with BC in hello Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="51a31-139">單一登入 toowork，Azure AD 需要 tooknow 哪些 hello BC 中 hello 雲端中的對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="51a31-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BC in hello Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="51a31-140">換句話說，Azure AD 使用者與 hello BC 中 hello 雲端中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="51a31-140">In other words, a link relationship between an Azure AD user and hello related user in BC in hello Cloud needs toobe established.</span></span>

<span data-ttu-id="51a31-141">在 BC hello 雲端中，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="51a31-141">In BC in hello Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="51a31-142">tooconfigure 及測試 Azure AD 單一登入與 BC hello 雲端中，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="51a31-142">tooconfigure and test Azure AD single sign-on with BC in hello Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="51a31-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="51a31-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="51a31-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="51a31-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51a31-145">**[建立 hello 雲端測試使用者 a BC](#creating-a-bc-in-the-cloud-test-user)**  -toohave 許 Simon BC 中 hello 是連結的 toohello Azure AD 使用者表示法的雲端中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="51a31-145">**[Creating a BC in hello Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - toohave a counterpart of Britta Simon in BC in hello Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="51a31-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="51a31-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51a31-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="51a31-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="51a31-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="51a31-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="51a31-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並在您 BC hello 雲端應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="51a31-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BC in hello Cloud application.</span></span>

<span data-ttu-id="51a31-150">**tooconfigure Azure AD 單一登入與 BC hello 雲端中執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="51a31-150">**tooconfigure Azure AD single sign-on with BC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="51a31-151">在 Azure 入口網站上 hello hello **BC 中 hello 雲端**應用程式整合頁面上，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="51a31-151">In hello Azure portal, on hello **BC in hello Cloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="51a31-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="51a31-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="51a31-155">在 hello **BC 中 hello 雲端網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="51a31-155">On hello **BC in hello Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="51a31-157">a.</span><span class="sxs-lookup"><span data-stu-id="51a31-157">a.</span></span> <span data-ttu-id="51a31-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="51a31-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="51a31-159">b.</span><span class="sxs-lookup"><span data-stu-id="51a31-159">b.</span></span> <span data-ttu-id="51a31-160">在 hello**識別碼**文字方塊中，輸入 URL:`https://app.bcinthecloud.com`</span><span class="sxs-lookup"><span data-stu-id="51a31-160">In hello **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="51a31-161">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="51a31-161">This value is not real.</span></span> <span data-ttu-id="51a31-162">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="51a31-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="51a31-163">請連絡[BC 中 hello 雲端的用戶端支援小組](https://www.bcinthecloud.com/supportcenter/)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="51a31-163">Contact [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) tooget this value.</span></span> 
 
4. <span data-ttu-id="51a31-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="51a31-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="51a31-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="51a31-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51a31-168">tooconfigure 單一登入上**BC 中 hello 雲端**端，您需要下載 toosend hello**中繼資料 XML**太[BC 中 hello 雲端支援小組](https://www.bcinthecloud.com/supportcenter/)。</span><span class="sxs-lookup"><span data-stu-id="51a31-168">tooconfigure single sign-on on **BC in hello Cloud** side, you need toosend hello downloaded **Metadata XML** too[BC in hello Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="51a31-169">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="51a31-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="51a31-170">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="51a31-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="51a31-171">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="51a31-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="51a31-172">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="51a31-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="51a31-173">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="51a31-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="51a31-175">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="51a31-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="51a31-176">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="51a31-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="51a31-178">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="51a31-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="51a31-180">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="51a31-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="51a31-182">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="51a31-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="51a31-184">a.</span><span class="sxs-lookup"><span data-stu-id="51a31-184">a.</span></span> <span data-ttu-id="51a31-185">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="51a31-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="51a31-186">b.</span><span class="sxs-lookup"><span data-stu-id="51a31-186">b.</span></span> <span data-ttu-id="51a31-187">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="51a31-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="51a31-188">c.</span><span class="sxs-lookup"><span data-stu-id="51a31-188">c.</span></span> <span data-ttu-id="51a31-189">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="51a31-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="51a31-190">d.</span><span class="sxs-lookup"><span data-stu-id="51a31-190">d.</span></span> <span data-ttu-id="51a31-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="51a31-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-hello-cloud-test-user"></a><span data-ttu-id="51a31-192">建立 a BC 中 hello 雲端測試使用者</span><span class="sxs-lookup"><span data-stu-id="51a31-192">Creating a BC in hello Cloud test user</span></span>

<span data-ttu-id="51a31-193">在本節中，您可以建立呼叫 BC 許 Simon hello 雲端中的使用者。</span><span class="sxs-lookup"><span data-stu-id="51a31-193">In this section, you create a user called Britta Simon in BC in hello Cloud.</span></span> <span data-ttu-id="51a31-194">使用[BC 中 hello 雲端的用戶端支援小組](https://www.bcinthecloud.com/supportcenter/)若要新增 hello 雲端應用程式中的 hello BC hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="51a31-194">Work with [BC in hello Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add hello users in hello BC in hello Cloud application.</span></span> <span data-ttu-id="51a31-195">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="51a31-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="51a31-196">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="51a31-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="51a31-197">在本節中，您可以授與存取 tooBC hello 雲端中的啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="51a31-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBC in hello Cloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="51a31-199">**tooassign 許 Simon tooBC hello 雲端中執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="51a31-199">**tooassign Britta Simon tooBC in hello Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="51a31-200">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="51a31-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="51a31-202">在 [hello] 應用程式清單中，選取**BC 中 hello 雲端**。</span><span class="sxs-lookup"><span data-stu-id="51a31-202">In hello applications list, select **BC in hello Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="51a31-204">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="51a31-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="51a31-206">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51a31-206">Click **Add** button.</span></span> <span data-ttu-id="51a31-207">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="51a31-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="51a31-209">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="51a31-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="51a31-210">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51a31-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51a31-211">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51a31-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="51a31-212">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="51a31-212">Testing single sign-on</span></span>

<span data-ttu-id="51a31-213">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="51a31-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

 <span data-ttu-id="51a31-214">當您按一下 hello BC hello 存取面板中的 hello 雲端磚中時，您應該取得自動登入 tooyour BC hello 雲端應用程式中。</span><span class="sxs-lookup"><span data-stu-id="51a31-214">When you click hello BC in hello Cloud tile in hello Access Panel, you should get automatically signed-on tooyour BC in hello Cloud application.</span></span> <span data-ttu-id="51a31-215">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="51a31-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51a31-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="51a31-216">Additional resources</span></span>

* [<span data-ttu-id="51a31-217">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51a31-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51a31-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="51a31-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

