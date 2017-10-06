---
title: "教學課程：Azure Active Directory 與 Huddle 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Huddle 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="a151a-103">教學課程：Azure Active Directory 與 Huddle 整合</span><span class="sxs-lookup"><span data-stu-id="a151a-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="a151a-104">在此教學課程中，您學會如何 toointegrate Huddle 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a151a-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a151a-105">與 Azure AD 整合 Huddle 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="a151a-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a151a-106">您可以控制存取 tooHuddle Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="a151a-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="a151a-107">您可以啟用您的使用者 tooautomatically get 登入 tooHuddle （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a151a-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a151a-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a151a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a151a-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a151a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a151a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a151a-110">Prerequisites</span></span>

<span data-ttu-id="a151a-111">與 Huddle tooconfigure Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a151a-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="a151a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a151a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a151a-113">已啟用 Huddle 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a151a-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a151a-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a151a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a151a-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a151a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a151a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a151a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a151a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a151a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a151a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a151a-118">Scenario description</span></span>

<span data-ttu-id="a151a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a151a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a151a-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a151a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a151a-121">從 hello 圖庫加入 Huddle</span><span class="sxs-lookup"><span data-stu-id="a151a-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="a151a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a151a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="a151a-123">從 hello 圖庫加入 Huddle</span><span class="sxs-lookup"><span data-stu-id="a151a-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="a151a-124">tooconfigure hello Huddle 至 Azure AD 整合，您需要 tooadd Huddle hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a151a-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a151a-125">**tooadd Huddle 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a151a-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a151a-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a151a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a151a-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a151a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a151a-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a151a-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a151a-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a151a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a151a-133">在 [hello] 搜尋方塊中，輸入**Huddle**。</span><span class="sxs-lookup"><span data-stu-id="a151a-133">In hello search box, type **Huddle**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="a151a-135">在 [hello [結果] 窗格中，選取 [ **Huddle**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a151a-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a151a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a151a-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a151a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Huddle 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a151a-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a151a-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Huddle 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a151a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="a151a-140">換句話說，Azure AD 使用者與 hello 之間的連結關聯性相關的建立 Huddle 需求 toobe 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="a151a-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="a151a-141">在 Huddle 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="a151a-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a151a-142">tooconfigure 及測試 Azure AD 單一登入 Huddle，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a151a-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a151a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a151a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="a151a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a151a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="a151a-145">**[建立測試使用者 Huddle](#creating-a-huddle-test-user) ** -toohave 許 Simon Huddle 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a151a-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="a151a-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a151a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="a151a-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a151a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a151a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a151a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a151a-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Huddle 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="a151a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="a151a-150">**tooconfigure Azure AD 單一登入與 Huddle，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a151a-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="a151a-151">在 Azure 入口網站上 hello hello **Huddle**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a151a-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a151a-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a151a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="a151a-155">在 [hello **Huddle 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a151a-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="a151a-157">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="a151a-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a151a-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="a151a-158">This value is not real.</span></span> <span data-ttu-id="a151a-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="a151a-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a151a-160">請連絡[Huddle 的用戶端支援小組](https://huddle.zendesk.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="a151a-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="a151a-161">在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="a151a-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="a151a-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="a151a-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a151a-165">在 [hello **Huddle 設定**區段中，按一下**設定 Huddle** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="a151a-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a151a-166">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="a151a-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="a151a-168">tooconfigure 單一登入 Huddle 端上，您需要下載 toosend hello**憑證**， **SAML 單一登入服務 URL**，和**SAML 實體識別碼**太[Huddle 的用戶端支援小組](https://huddle.zendesk.com)。</span><span class="sxs-lookup"><span data-stu-id="a151a-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="a151a-169">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="a151a-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="a151a-170">單一登入需要 toobe 由 hello Huddle 支援小組啟用。</span><span class="sxs-lookup"><span data-stu-id="a151a-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="a151a-171">Hello 組態完成後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="a151a-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="a151a-172">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a151a-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a151a-173">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a151a-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a151a-174">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a151a-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a151a-175">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a151a-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="a151a-176">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a151a-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a151a-178">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a151a-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a151a-179">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a151a-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a151a-181">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a151a-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a151a-183">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="a151a-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a151a-185">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a151a-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a151a-187">a.</span><span class="sxs-lookup"><span data-stu-id="a151a-187">a.</span></span> <span data-ttu-id="a151a-188">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a151a-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a151a-189">b.</span><span class="sxs-lookup"><span data-stu-id="a151a-189">b.</span></span> <span data-ttu-id="a151a-190">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="a151a-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a151a-191">c.</span><span class="sxs-lookup"><span data-stu-id="a151a-191">c.</span></span> <span data-ttu-id="a151a-192">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a151a-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a151a-193">d.</span><span class="sxs-lookup"><span data-stu-id="a151a-193">d.</span></span> <span data-ttu-id="a151a-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a151a-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="a151a-195">建立 Huddle 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a151a-195">Creating a Huddle test user</span></span>

<span data-ttu-id="a151a-196">tooenable Azure AD 使用者 toolog 中 tooHuddle，它們必須佈建到 Huddle。</span><span class="sxs-lookup"><span data-stu-id="a151a-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="a151a-197">在 Huddle 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="a151a-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="a151a-198">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a151a-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="a151a-199">登入 tooyour **Huddle**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="a151a-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="a151a-200">按一下 [工作區] 。</span><span class="sxs-lookup"><span data-stu-id="a151a-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="a151a-201">按一下 [人員] \> [邀請人員]。</span><span class="sxs-lookup"><span data-stu-id="a151a-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="a151a-202">![人員](./media/active-directory-saas-huddle-tutorial/IC787838.png "人員")</span><span class="sxs-lookup"><span data-stu-id="a151a-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="a151a-203">在 [hello**建立新的邀請**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a151a-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="a151a-204">![新的邀請](./media/active-directory-saas-huddle-tutorial/IC787839.png "新的邀請")</span><span class="sxs-lookup"><span data-stu-id="a151a-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="a151a-205">a.</span><span class="sxs-lookup"><span data-stu-id="a151a-205">a.</span></span> <span data-ttu-id="a151a-206">在 [hello**選擇小組 tooinvite 人員 toojoin**清單中，選取**小組**。</span><span class="sxs-lookup"><span data-stu-id="a151a-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="a151a-207">b.</span><span class="sxs-lookup"><span data-stu-id="a151a-207">b.</span></span> <span data-ttu-id="a151a-208">型別 hello**電子郵件地址**有效的 Azure AD 的帳戶中您要 tooprovision 太**輸入電子郵件地址的人，您想要 tooinvite**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a151a-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="a151a-209">c.</span><span class="sxs-lookup"><span data-stu-id="a151a-209">c.</span></span> <span data-ttu-id="a151a-210">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="a151a-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="a151a-211">hello Azure AD 帳戶持有者將收到包含連結 tooconfirm hello 帳戶之前它會變成作用中的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="a151a-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="a151a-212">您可以使用任何其他 Huddle 使用者帳戶建立工具或 Api 提供 Huddle tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a151a-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a151a-213">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a151a-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a151a-214">在本節中，您可以授與存取 tooHuddle 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a151a-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![指派使用者][200] 

<span data-ttu-id="a151a-216">**tooassign 許 Simon tooHuddle，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a151a-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="a151a-217">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a151a-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a151a-219">在 [hello] 應用程式清單中，選取**Huddle**。</span><span class="sxs-lookup"><span data-stu-id="a151a-219">In hello applications list, select **Huddle**.</span></span>

    ![設定單一登入](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="a151a-221">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a151a-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a151a-223">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a151a-223">Click **Add** button.</span></span> <span data-ttu-id="a151a-224">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a151a-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a151a-226">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="a151a-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a151a-227">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a151a-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a151a-228">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a151a-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a151a-229">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a151a-229">Testing single sign-on</span></span>

<span data-ttu-id="a151a-230">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a151a-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a151a-231">當您按一下 hello Huddle 磚 hello 存取面板中的時，您應該取得自動 Huddle 的應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="a151a-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="a151a-232">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a151a-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a151a-233">其他資源</span><span class="sxs-lookup"><span data-stu-id="a151a-233">Additional resources</span></span>

* [<span data-ttu-id="a151a-234">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a151a-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a151a-235">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a151a-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
