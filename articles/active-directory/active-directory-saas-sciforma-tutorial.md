---
title: "教學課程：Azure Active Directory 與 Sciforma 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Sciforma 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: abbfb5ac-7687-4153-b263-8090102dae37
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.openlocfilehash: fca6237196061355e38d431e958964a45246f965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciforma"></a><span data-ttu-id="29434-103">教學課程：Azure Active Directory 與 Sciforma 整合</span><span class="sxs-lookup"><span data-stu-id="29434-103">Tutorial: Azure Active Directory integration with Sciforma</span></span>

<span data-ttu-id="29434-104">在此教學課程中，您學會如何 toointegrate Sciforma 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="29434-104">In this tutorial, you learn how toointegrate Sciforma with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29434-105">整合 Azure AD 與 Sciforma 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="29434-105">Integrating Sciforma with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="29434-106">您可以控制存取 tooSciforma Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="29434-106">You can control in Azure AD who has access tooSciforma</span></span>
- <span data-ttu-id="29434-107">您可以啟用您的使用者 tooautomatically get 登入 tooSciforma （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="29434-107">You can enable your users tooautomatically get signed-on tooSciforma (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29434-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="29434-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="29434-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="29434-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29434-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="29434-110">Prerequisites</span></span>

<span data-ttu-id="29434-111">tooconfigure Azure AD 與 Sciforma 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="29434-111">tooconfigure Azure AD integration with Sciforma, you need hello following items:</span></span>

- <span data-ttu-id="29434-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="29434-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29434-113">已啟用 Sciforma 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="29434-113">A Sciforma single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29434-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="29434-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29434-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="29434-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29434-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="29434-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29434-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="29434-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29434-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="29434-118">Scenario description</span></span>
<span data-ttu-id="29434-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29434-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29434-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="29434-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29434-121">從 hello 圖庫加入 Sciforma</span><span class="sxs-lookup"><span data-stu-id="29434-121">Adding Sciforma from hello gallery</span></span>
2. <span data-ttu-id="29434-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="29434-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciforma-from-hello-gallery"></a><span data-ttu-id="29434-123">從 hello 圖庫加入 Sciforma</span><span class="sxs-lookup"><span data-stu-id="29434-123">Adding Sciforma from hello gallery</span></span>
<span data-ttu-id="29434-124">tooconfigure hello 整合 Sciforma 的 Azure AD，您需要 tooadd Sciforma hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29434-124">tooconfigure hello integration of Sciforma into Azure AD, you need tooadd Sciforma from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="29434-125">**tooadd Sciforma 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="29434-125">**tooadd Sciforma from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="29434-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="29434-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29434-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="29434-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="29434-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="29434-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="29434-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="29434-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="29434-133">在 [hello] 搜尋方塊中，輸入**Sciforma**。</span><span class="sxs-lookup"><span data-stu-id="29434-133">In hello search box, type **Sciforma**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_search.png)

5. <span data-ttu-id="29434-135">在 [hello [結果] 窗格中，選取 [ **Sciforma**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29434-135">In hello results panel, select **Sciforma**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29434-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="29434-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="29434-138">在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Sciforma 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29434-138">In this section, you configure and test Azure AD single sign-on with Sciforma based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="29434-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Sciforma 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="29434-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Sciforma is tooa user in Azure AD.</span></span> <span data-ttu-id="29434-140">換句話說，Azure AD 使用者與 hello Sciforma 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="29434-140">In other words, a link relationship between an Azure AD user and hello related user in Sciforma needs toobe established.</span></span>

<span data-ttu-id="29434-141">Sciforma 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="29434-141">In Sciforma, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="29434-142">tooconfigure 及 Azure AD 單一登入與 Sciforma 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="29434-142">tooconfigure and test Azure AD single sign-on with Sciforma, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="29434-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="29434-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="29434-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="29434-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29434-145">**[建立測試使用者 Sciforma](#creating-a-sciforma-test-user) ** -toohave 許 Simon Sciforma 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="29434-145">**[Creating a Sciforma test user](#creating-a-sciforma-test-user)** - toohave a counterpart of Britta Simon in Sciforma that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="29434-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29434-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29434-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="29434-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="29434-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="29434-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="29434-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Sciforma 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="29434-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Sciforma application.</span></span>

<span data-ttu-id="29434-150">**tooconfigure Azure AD 單一登入 Sciforma 時，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="29434-150">**tooconfigure Azure AD single sign-on with Sciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="29434-151">在 Azure 入口網站上 hello hello **Sciforma**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="29434-151">In hello Azure portal, on hello **Sciforma** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="29434-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29434-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_samlbase.png)

3. <span data-ttu-id="29434-155">在 [hello **Sciforma 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="29434-155">On hello **Sciforma Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_url.png)

    <span data-ttu-id="29434-157">a.</span><span class="sxs-lookup"><span data-stu-id="29434-157">a.</span></span> <span data-ttu-id="29434-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.sciforma.net/sciforma/main.html`</span><span class="sxs-lookup"><span data-stu-id="29434-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/main.html`</span></span>

    <span data-ttu-id="29434-159">b.</span><span class="sxs-lookup"><span data-stu-id="29434-159">b.</span></span> <span data-ttu-id="29434-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.sciforma.net/sciforma/saml`</span><span class="sxs-lookup"><span data-stu-id="29434-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.sciforma.net/sciforma/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29434-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="29434-161">These values are not real.</span></span> <span data-ttu-id="29434-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="29434-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="29434-163">請連絡[Sciforma 用戶端支援小組](http://www.sciforma.com/company/contact_us)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="29434-163">Contact [Sciforma Client support team](http://www.sciforma.com/company/contact_us) tooget these values.</span></span> 
 


4. <span data-ttu-id="29434-164">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="29434-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_certificate.png) 

5. <span data-ttu-id="29434-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="29434-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sciforma-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="29434-168">tooconfigure 單一登入上**Sciforma**端，您需要下載 toosend hello**中繼資料 XML**太[Sciforma 支援小組](http://www.sciforma.com/company/contact_us)。</span><span class="sxs-lookup"><span data-stu-id="29434-168">tooconfigure single sign-on on **Sciforma** side, you need toosend hello downloaded **Metadata XML** too[Sciforma support team](http://www.sciforma.com/company/contact_us).</span></span>

> [!TIP]
> <span data-ttu-id="29434-169">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="29434-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="29434-170">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="29434-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="29434-171">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29434-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29434-172">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="29434-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="29434-173">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="29434-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="29434-175">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="29434-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="29434-176">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="29434-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sciforma-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29434-178">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="29434-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sciforma-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29434-180">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="29434-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sciforma-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29434-182">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="29434-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sciforma-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29434-184">a.</span><span class="sxs-lookup"><span data-stu-id="29434-184">a.</span></span> <span data-ttu-id="29434-185">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="29434-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29434-186">b.</span><span class="sxs-lookup"><span data-stu-id="29434-186">b.</span></span> <span data-ttu-id="29434-187">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="29434-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29434-188">c.</span><span class="sxs-lookup"><span data-stu-id="29434-188">c.</span></span> <span data-ttu-id="29434-189">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="29434-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="29434-190">d.</span><span class="sxs-lookup"><span data-stu-id="29434-190">d.</span></span> <span data-ttu-id="29434-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="29434-191">Click **Create**.</span></span>
 
### <a name="creating-a-sciforma-test-user"></a><span data-ttu-id="29434-192">建立 Sciforma 測試使用者</span><span class="sxs-lookup"><span data-stu-id="29434-192">Creating a Sciforma test user</span></span>

<span data-ttu-id="29434-193">不沒有您 tooconfigure 使用者佈建 tooSciforma 任何動作項目。</span><span class="sxs-lookup"><span data-stu-id="29434-193">There is no action item for you tooconfigure user provisioning tooSciforma.</span></span> <span data-ttu-id="29434-194">當指派的使用者嘗試 toolog tooSciforma 使用 hello 存取面板中的時，Sciforma 會檢查 hello 使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="29434-194">When an assigned user tries toolog in tooSciforma using hello access panel, Sciforma checks whether hello user exists.</span></span>  

* <span data-ttu-id="29434-195">如果尚無可用的使用者帳戶，Sciforma 會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="29434-195">If there is no user account available yet, it is automatically created by Sciforma.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="29434-196">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="29434-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="29434-197">在本節中，您可以授與存取 tooSciforma 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29434-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSciforma.</span></span>

![指派使用者][200] 

<span data-ttu-id="29434-199">**tooassign 許 Simon tooSciforma，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="29434-199">**tooassign Britta Simon tooSciforma, perform hello following steps:**</span></span>

1. <span data-ttu-id="29434-200">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="29434-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="29434-202">在 [hello] 應用程式清單中，選取**Sciforma**。</span><span class="sxs-lookup"><span data-stu-id="29434-202">In hello applications list, select **Sciforma**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sciforma-tutorial/tutorial_sciforma_app.png) 

3. <span data-ttu-id="29434-204">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="29434-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="29434-206">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="29434-206">Click **Add** button.</span></span> <span data-ttu-id="29434-207">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="29434-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="29434-209">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="29434-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="29434-210">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="29434-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29434-211">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="29434-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="29434-212">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="29434-212">Testing single sign-on</span></span>

<span data-ttu-id="29434-213">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="29434-213">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="29434-214">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="29434-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29434-215">其他資源</span><span class="sxs-lookup"><span data-stu-id="29434-215">Additional resources</span></span>

* [<span data-ttu-id="29434-216">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29434-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29434-217">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="29434-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sciforma-tutorial/tutorial_general_203.png

