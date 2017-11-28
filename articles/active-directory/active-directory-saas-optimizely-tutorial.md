---
title: "教學課程：Azure Active Directory 與 Optimizely 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Optimizely 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 868aefae27ca155d2963f3dcfcd79bbb564b48ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="c9cd7-103">教學課程：Azure Active Directory 與 Optimizely 整合</span><span class="sxs-lookup"><span data-stu-id="c9cd7-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="c9cd7-104">在此教學課程中，您學會如何 toointegrate Optimizely 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-104">In this tutorial, you learn how toointegrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9cd7-105">與 Azure AD 整合 Optimizely 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cd7-105">Integrating Optimizely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c9cd7-106">您可以控制存取 tooOptimizely Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="c9cd7-106">You can control in Azure AD who has access tooOptimizely</span></span>
- <span data-ttu-id="c9cd7-107">您可以啟用您的使用者 tooautomatically get 登入 tooOptimizely （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="c9cd7-107">You can enable your users tooautomatically get signed-on tooOptimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9cd7-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c9cd7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c9cd7-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9cd7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c9cd7-110">Prerequisites</span></span>

<span data-ttu-id="c9cd7-111">tooconfigure Optimizely 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cd7-111">tooconfigure Azure AD integration with Optimizely, you need hello following items:</span></span>

- <span data-ttu-id="c9cd7-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c9cd7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9cd7-113">啟用 Optimizely 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c9cd7-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9cd7-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9cd7-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c9cd7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9cd7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9cd7-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9cd7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c9cd7-118">Scenario description</span></span>
<span data-ttu-id="c9cd7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9cd7-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c9cd7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9cd7-121">從 hello 圖庫加入 Optimizely</span><span class="sxs-lookup"><span data-stu-id="c9cd7-121">Adding Optimizely from hello gallery</span></span>
2. <span data-ttu-id="c9cd7-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c9cd7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-hello-gallery"></a><span data-ttu-id="c9cd7-123">從 hello 圖庫加入 Optimizely</span><span class="sxs-lookup"><span data-stu-id="c9cd7-123">Adding Optimizely from hello gallery</span></span>
<span data-ttu-id="c9cd7-124">tooconfigure hello 整合 Optimizely 到 Azure AD，您需要 tooadd Optimizely hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-124">tooconfigure hello integration of Optimizely into Azure AD, you need tooadd Optimizely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c9cd7-125">**tooadd Optimizely 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c9cd7-125">**tooadd Optimizely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9cd7-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9cd7-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c9cd7-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c9cd7-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c9cd7-133">在 [hello] 搜尋方塊中，輸入**Optimizely**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-133">In hello search box, type **Optimizely**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="c9cd7-135">在 [hello [結果] 窗格中，選取 [ **Optimizely**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-135">In hello results panel, select **Optimizely**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9cd7-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c9cd7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9cd7-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Optimizely 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c9cd7-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Optimizely 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Optimizely is tooa user in Azure AD.</span></span> <span data-ttu-id="c9cd7-140">換句話說，Azure AD 使用者與 hello Optimizely 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-140">In other words, a link relationship between an Azure AD user and hello related user in Optimizely needs toobe established.</span></span>

<span data-ttu-id="c9cd7-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Optimizely 中。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Optimizely.</span></span>

<span data-ttu-id="c9cd7-142">tooconfigure 及 Optimizely 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c9cd7-142">tooconfigure and test Azure AD single sign-on with Optimizely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c9cd7-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c9cd7-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9cd7-145">**[建立測試使用者 Optimizely](#creating-an-optimizely-test-user) ** -toohave 許 Simon Optimizely 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - toohave a counterpart of Britta Simon in Optimizely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9cd7-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9cd7-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9cd7-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c9cd7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9cd7-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Optimizely 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="c9cd7-150">**tooconfigure Azure AD 單一登入與 Optimizely，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c9cd7-150">**tooconfigure Azure AD single sign-on with Optimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9cd7-151">在 Azure 入口網站上 hello hello **Optimizely**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-151">In hello Azure portal, on hello **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c9cd7-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="c9cd7-155">在 [hello **Optimizely 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cd7-155">On hello **Optimizely Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="c9cd7-157">a.</span><span class="sxs-lookup"><span data-stu-id="c9cd7-157">a.</span></span> <span data-ttu-id="c9cd7-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="c9cd7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="c9cd7-159">b.</span><span class="sxs-lookup"><span data-stu-id="c9cd7-159">b.</span></span> <span data-ttu-id="c9cd7-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="c9cd7-160">In hello **Identifier** textbox, type a URL using hello following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9cd7-161">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-161">These values are not hello real.</span></span> <span data-ttu-id="c9cd7-162">您將使用 hello 實際登入 URL 和識別碼，這在 hello 教學課程稍後會說明更新 hello 值。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-162">You will update hello value with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="c9cd7-163">在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-163">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="c9cd7-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-165">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c9cd7-167">在 [hello **Optimizely 組態**區段中，按一下**設定 Optimizely** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-167">On hello **Optimizely Configuration** section, click **Configure Optimizely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c9cd7-168">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="c9cd7-168">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="c9cd7-170">tooconfigure 單一登入上**Optimizely**側邊，請連絡您的 Optimizely 帳戶管理員，提供下載的 hello**憑證 (Base64)**，和**SAML 單一登入服務 URL**.</span><span class="sxs-lookup"><span data-stu-id="c9cd7-170">tooconfigure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide hello downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="c9cd7-171">回應 tooyour 電子郵件、 Optimizely 提供您 hello 登入 URL (SP 起始 SSO) 與 hello 識別碼 （服務提供者識別碼） 值。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-171">In response tooyour email, Optimizely provides you with hello Sign On URL (SP-initiated SSO) and hello Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="c9cd7-172">a.</span><span class="sxs-lookup"><span data-stu-id="c9cd7-172">a.</span></span> <span data-ttu-id="c9cd7-173">複製 hello **SP 起始 SSO URL**提供 Optimizely，然後貼入 hello**登入 URL** ] 文字方塊中的**Optimizely 網域和 Url** Azure 入口網站上的區段</span><span class="sxs-lookup"><span data-stu-id="c9cd7-173">Copy hello **SP-initiated SSO URL** provided by Optimizely, and paste into hello **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="c9cd7-174">b.</span><span class="sxs-lookup"><span data-stu-id="c9cd7-174">b.</span></span> <span data-ttu-id="c9cd7-175">複製 hello**服務提供者識別碼**提供 Optimizely，然後貼入 hello**識別碼**] 文字方塊中的**Optimizely 網域和 Url** Azure 入口網站上的區段</span><span class="sxs-lookup"><span data-stu-id="c9cd7-175">Copy hello **Service Provider Entity ID** provided by Optimizely, and paste into hello **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="c9cd7-176">在不同的瀏覽器視窗中，登入 tooyour Optimizely 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-176">In a different browser window, sign-on tooyour Optimizely application.</span></span>

10. <span data-ttu-id="c9cd7-177">按一下帳戶名稱在 hello 最佳右下角，然後**帳戶設定**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-177">Click you account name in hello top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD 單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="c9cd7-179">在 hello 帳戶索引標籤上，核取方塊 hello**啟用 SSO**下單一登入在 hello**概觀**> 一節。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-179">In hello Account tab, check hello box **Enable SSO** under Single Sign On in hello **Overview** section.</span></span>
   
    ![Azure AD 單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="c9cd7-181">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="c9cd7-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="c9cd7-182">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="c9cd7-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c9cd7-183">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c9cd7-184">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c9cd7-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9cd7-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c9cd7-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9cd7-186">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c9cd7-188">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c9cd7-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9cd7-189">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9cd7-191">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9cd7-193">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9cd7-195">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c9cd7-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9cd7-197">a.</span><span class="sxs-lookup"><span data-stu-id="c9cd7-197">a.</span></span> <span data-ttu-id="c9cd7-198">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9cd7-199">b.</span><span class="sxs-lookup"><span data-stu-id="c9cd7-199">b.</span></span> <span data-ttu-id="c9cd7-200">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="c9cd7-201">c.</span><span class="sxs-lookup"><span data-stu-id="c9cd7-201">c.</span></span> <span data-ttu-id="c9cd7-202">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c9cd7-203">d.</span><span class="sxs-lookup"><span data-stu-id="c9cd7-203">d.</span></span> <span data-ttu-id="c9cd7-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="c9cd7-205">建立 Optimizely 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c9cd7-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="c9cd7-206">在本節中，您會在 Optimizely 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="c9cd7-207">在 [hello 首頁上，選取 [**共同作業者**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-207">On hello home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="c9cd7-208">新的共同作業者 toohello 專案 tooadd，按一下 [**新的共同作業者**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-208">tooadd new collaborator toohello project, click **New Collaborator**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="c9cd7-210">填滿 hello 電子郵件地址，並將它們指派角色。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-210">Fill in hello email address and assign them a role.</span></span> <span data-ttu-id="c9cd7-211">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-211">Click **Invite**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="c9cd7-213">這些人員會收到一封電子郵件邀請。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-213">They receive an email invite.</span></span> <span data-ttu-id="c9cd7-214">它們使用 hello 電子郵件地址，有 tooOptimizely toolog。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-214">Using hello email address, they have toolog in tooOptimizely.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c9cd7-215">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="c9cd7-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c9cd7-216">在本節中，您可以授與存取 tooOptimizely 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOptimizely.</span></span>

![指派使用者][200] 

<span data-ttu-id="c9cd7-218">**tooassign 許 Simon tooOptimizely，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c9cd7-218">**tooassign Britta Simon tooOptimizely, perform hello following steps:**</span></span>

1. <span data-ttu-id="c9cd7-219">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c9cd7-221">在 [hello] 應用程式清單中，選取**Optimizely**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-221">In hello applications list, select **Optimizely**.</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="c9cd7-223">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c9cd7-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-225">Click **Add** button.</span></span> <span data-ttu-id="c9cd7-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c9cd7-228">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c9cd7-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9cd7-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c9cd7-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c9cd7-231">Testing single sign-on</span></span>

<span data-ttu-id="c9cd7-232">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c9cd7-233">當您按一下 hello Optimizely 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Optimizely 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c9cd7-233">When you click hello Optimizely tile in hello Access Panel, you should get automatically signed-on tooyour Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c9cd7-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="c9cd7-234">Additional resources</span></span>

* [<span data-ttu-id="c9cd7-235">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9cd7-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9cd7-236">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c9cd7-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

