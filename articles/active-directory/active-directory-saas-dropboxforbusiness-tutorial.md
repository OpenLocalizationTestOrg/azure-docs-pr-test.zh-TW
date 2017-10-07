---
title: "教學課程：Azure Active Directory 與 Dropbox for Business 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 dropbox 企業版之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="a1dcd-103">教學課程：Azure Active Directory 與 Dropbox for Business 整合</span><span class="sxs-lookup"><span data-stu-id="a1dcd-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="a1dcd-104">在此教學課程中，您學會如何 toointegrate Dropbox 企業版與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a1dcd-105">整合 Azure AD 與 dropbox 企業版可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a1dcd-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a1dcd-106">您可以控制存取 tooDropbox 商務的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="a1dcd-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="a1dcd-107">您可以啟用您使用者 tooautomatically get 登入 tooDropbox for Business （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a1dcd-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a1dcd-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a1dcd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a1dcd-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1dcd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a1dcd-110">Prerequisites</span></span>

<span data-ttu-id="a1dcd-111">tooconfigure Azure AD 與 dropbox 企業版整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a1dcd-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="a1dcd-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a1dcd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a1dcd-113">已啟用 Dropbox for Business 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a1dcd-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a1dcd-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a1dcd-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a1dcd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a1dcd-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a1dcd-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a1dcd-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a1dcd-118">Scenario description</span></span>
<span data-ttu-id="a1dcd-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a1dcd-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a1dcd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a1dcd-121">從 hello 圖庫加入 dropbox 企業版</span><span class="sxs-lookup"><span data-stu-id="a1dcd-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="a1dcd-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a1dcd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="a1dcd-123">從 hello 圖庫加入 dropbox 企業版</span><span class="sxs-lookup"><span data-stu-id="a1dcd-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="a1dcd-124">tooconfigure hello Dropbox 企業版至 Azure AD 整合，您需要 tooadd Dropbox for Business hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a1dcd-125">**tooadd Dropbox 企業版從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1dcd-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1dcd-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a1dcd-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a1dcd-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a1dcd-131">按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a1dcd-133">在 [hello] 搜尋方塊中，輸入**dropbox 企業版**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="a1dcd-135">在 [hello [結果] 窗格中，選取 [ **dropbox 企業版**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a1dcd-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a1dcd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a1dcd-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Dropbox for Business 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a1dcd-139">單一登入 toowork，Azure AD 需要 tooknow dropbox 企業版中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="a1dcd-140">換句話說，Azure AD 使用者與 dropbox 企業版中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="a1dcd-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** dropbox 企業版中。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="a1dcd-142">tooconfigure 及測試 Azure AD 單一登入 Dropbox for Business，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a1dcd-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a1dcd-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a1dcd-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a1dcd-145">**[建立商務測試使用者的 Dropbox](#creating-a-dropbox-for-business-test-user) ** -toohave 許 Simon Dropbox 企業版所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a1dcd-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a1dcd-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a1dcd-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a1dcd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a1dcd-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的 Dropbox 企業營運應用程式中。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="a1dcd-150">**tooconfigure Azure AD 單一登入 Dropbox 企業版，以執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1dcd-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1dcd-151">在 Azure 入口網站上 hello hello **dropbox 企業版**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a1dcd-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="a1dcd-155">在 [hello **Dropbox 商務網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1dcd-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="a1dcd-156">a.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-156">a.</span></span> <span data-ttu-id="a1dcd-157">登入 tooyour Dropbox 企業版租用戶。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="a1dcd-158">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="a1dcd-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="a1dcd-159">b.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-159">b.</span></span> <span data-ttu-id="a1dcd-160">Hello hello 左側瀏覽窗格中按一下**管理主控台**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="a1dcd-161">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="a1dcd-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="a1dcd-162">c.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-162">c.</span></span> <span data-ttu-id="a1dcd-163">在 [hello**管理主控台**，按一下 [**驗證**hello 左側的導覽窗格中。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="a1dcd-164">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="a1dcd-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="a1dcd-165">d.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-165">d.</span></span> <span data-ttu-id="a1dcd-166">在 hello**單一登入**區段中，選取**啟用單一登入**，然後按一下 [**詳細**tooexpand 這一節。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="a1dcd-167">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="a1dcd-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="a1dcd-168">e.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-168">e.</span></span> <span data-ttu-id="a1dcd-169">複製 hello URL 下一步太**使用者可以輸入登入電子郵件地址，或它們可以直接前往**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="a1dcd-171">f.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-171">f.</span></span> <span data-ttu-id="a1dcd-172">在 Azure 入口網站中 hello hello**登入 URL**文字方塊中，貼上 hello URL。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="a1dcd-174">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="a1dcd-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a1dcd-175">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-175">This value is not real value.</span></span> <span data-ttu-id="a1dcd-176">Hello 值以 hello 實際登入 URL 更新您從他們的單一登入區段取得。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="a1dcd-177">請連絡[商務用戶端支援小組的 Dropbox](https://www.dropbox.com/business/contact) tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="a1dcd-178">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="a1dcd-180">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-180">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a1dcd-182">在 [hello **Dropbox 商務組態**區段中，按一下**設定 dropbox 企業版**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a1dcd-183">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="a1dcd-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="a1dcd-185">tooconfigure 單一登入上**dropbox 企業版**側邊，請在您的 Dropbox 企業版租用戶中 hello**單一登入**區段 hello**驗證**] 頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1dcd-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="a1dcd-186">![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="a1dcd-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="a1dcd-187">a.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-187">a.</span></span> <span data-ttu-id="a1dcd-188">按一下 [必要]。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-188">Click **Required**.</span></span>
   
    <span data-ttu-id="a1dcd-189">b.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-189">b.</span></span> <span data-ttu-id="a1dcd-190">在 Azure 入口網站上 hello hello**設定登入**視窗中，複製 hello **SAML 單一登入服務 URL**值並貼到 hello**登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="a1dcd-191">c.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-191">c.</span></span> <span data-ttu-id="a1dcd-192">按一下**選擇憑證**，然後瀏覽 tooyour **Base64 編碼的憑證檔案**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="a1dcd-193">d.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-193">d.</span></span> <span data-ttu-id="a1dcd-194">按一下**儲存變更**toocomplete hello 設定您的 DropBox 企業版租用戶上。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="a1dcd-195">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a1dcd-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a1dcd-196">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a1dcd-197">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a1dcd-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a1dcd-198">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a1dcd-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="a1dcd-199">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a1dcd-201">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1dcd-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1dcd-202">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="a1dcd-204">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a1dcd-206">在 [hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a1dcd-208">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a1dcd-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a1dcd-210">a.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-210">a.</span></span> <span data-ttu-id="a1dcd-211">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a1dcd-212">b.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-212">b.</span></span> <span data-ttu-id="a1dcd-213">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a1dcd-214">c.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-214">c.</span></span> <span data-ttu-id="a1dcd-215">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a1dcd-216">d.</span><span class="sxs-lookup"><span data-stu-id="a1dcd-216">d.</span></span> <span data-ttu-id="a1dcd-217">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="a1dcd-218">建立 Dropbox for Business 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a1dcd-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="a1dcd-219">本節會在 Dropbox for Business 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="a1dcd-220">Dropbox for Business 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="a1dcd-221">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-221">There is no action item for you in this section.</span></span> <span data-ttu-id="a1dcd-222">如果使用者不在 dropbox 企業版中，當您嘗試 tooaccess dropbox 企業版時，會建立一個新。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="a1dcd-223">如果您需要以手動方式，請連絡使用者 toocreate [Dropbox 商務用戶端支援小組](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="a1dcd-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a1dcd-224">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a1dcd-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a1dcd-225">在本節中，您可以授與存取 tooDropbox 商務啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![指派使用者][200] 

<span data-ttu-id="a1dcd-227">**tooassign 許 Simon tooDropbox for Business，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a1dcd-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="a1dcd-228">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a1dcd-230">在 [hello] 應用程式清單中，選取**dropbox 企業版**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![設定單一登入](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="a1dcd-232">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a1dcd-234">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-234">Click **Add** button.</span></span> <span data-ttu-id="a1dcd-235">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a1dcd-237">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a1dcd-238">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a1dcd-239">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a1dcd-240">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a1dcd-240">Testing single sign-on</span></span>

<span data-ttu-id="a1dcd-241">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a1dcd-242">當您按一下商務磚 hello 存取面板中的 hello Dropbox 時，您應該取得您的 Dropbox 的登入頁面的企業營運應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1dcd-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a1dcd-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="a1dcd-243">Additional resources</span></span>

* [<span data-ttu-id="a1dcd-244">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1dcd-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a1dcd-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a1dcd-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a1dcd-246">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="a1dcd-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

