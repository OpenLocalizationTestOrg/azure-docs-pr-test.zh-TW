---
title: "教學課程：Azure Active Directory 與 UserEcho 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 UserEcho 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: efe4a94ed6e5d22d153565d4782850eac4dff37b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="91254-103">教學課程：Azure Active Directory 與 UserEcho 整合</span><span class="sxs-lookup"><span data-stu-id="91254-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="91254-104">在此教學課程中，您學會如何 toointegrate UserEcho 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="91254-104">In this tutorial, you learn how toointegrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91254-105">與 Azure AD 整合 UserEcho 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="91254-105">Integrating UserEcho with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="91254-106">您可以控制存取 tooUserEcho Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="91254-106">You can control in Azure AD who has access tooUserEcho</span></span>
- <span data-ttu-id="91254-107">您可以啟用您的使用者 tooautomatically get 登入 tooUserEcho （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="91254-107">You can enable your users tooautomatically get signed-on tooUserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91254-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="91254-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="91254-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="91254-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91254-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="91254-110">Prerequisites</span></span>

<span data-ttu-id="91254-111">tooconfigure UserEcho 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="91254-111">tooconfigure Azure AD integration with UserEcho, you need hello following items:</span></span>

- <span data-ttu-id="91254-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="91254-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91254-113">已啟用 UserEcho 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="91254-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91254-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="91254-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91254-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="91254-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91254-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="91254-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91254-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="91254-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91254-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="91254-118">Scenario description</span></span>
<span data-ttu-id="91254-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91254-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91254-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="91254-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91254-121">從 hello 圖庫加入 UserEcho</span><span class="sxs-lookup"><span data-stu-id="91254-121">Adding UserEcho from hello gallery</span></span>
2. <span data-ttu-id="91254-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91254-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-hello-gallery"></a><span data-ttu-id="91254-123">從 hello 圖庫加入 UserEcho</span><span class="sxs-lookup"><span data-stu-id="91254-123">Adding UserEcho from hello gallery</span></span>
<span data-ttu-id="91254-124">tooconfigure hello 整合 UserEcho 到 Azure AD，您需要 tooadd UserEcho hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91254-124">tooconfigure hello integration of UserEcho into Azure AD, you need tooadd UserEcho from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="91254-125">**tooadd UserEcho 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91254-125">**tooadd UserEcho from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="91254-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="91254-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="91254-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="91254-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="91254-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="91254-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="91254-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="91254-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="91254-133">在 [hello] 搜尋方塊中，輸入**UserEcho**。</span><span class="sxs-lookup"><span data-stu-id="91254-133">In hello search box, type **UserEcho**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_search.png)

5. <span data-ttu-id="91254-135">在 [hello [結果] 窗格中，選取 [ **UserEcho**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91254-135">In hello results panel, select **UserEcho**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91254-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91254-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91254-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 UserEcho 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91254-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91254-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 UserEcho 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="91254-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserEcho is tooa user in Azure AD.</span></span> <span data-ttu-id="91254-140">換句話說，Azure AD 使用者與 hello UserEcho 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="91254-140">In other words, a link relationship between an Azure AD user and hello related user in UserEcho needs toobe established.</span></span>

<span data-ttu-id="91254-141">UserEcho 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="91254-141">In UserEcho, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="91254-142">tooconfigure 及 UserEcho 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="91254-142">tooconfigure and test Azure AD single sign-on with UserEcho, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="91254-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="91254-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="91254-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="91254-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91254-145">**[建立測試使用者 UserEcho](#creating-a-userecho-test-user) ** -toohave 許 Simon UserEcho 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="91254-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - toohave a counterpart of Britta Simon in UserEcho that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="91254-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91254-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91254-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="91254-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91254-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="91254-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91254-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 UserEcho 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="91254-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="91254-150">**tooconfigure Azure AD 單一登入與 UserEcho，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91254-150">**tooconfigure Azure AD single sign-on with UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="91254-151">在 Azure 入口網站上 hello hello **UserEcho**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="91254-151">In hello Azure portal, on hello **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="91254-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91254-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_samlbase.png)

3. <span data-ttu-id="91254-155">在 [hello **UserEcho 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="91254-155">On hello **UserEcho Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="91254-157">a.</span><span class="sxs-lookup"><span data-stu-id="91254-157">a.</span></span> <span data-ttu-id="91254-158">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="91254-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="91254-159">b.</span><span class="sxs-lookup"><span data-stu-id="91254-159">b.</span></span> <span data-ttu-id="91254-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="91254-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91254-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="91254-161">These values are not real.</span></span> <span data-ttu-id="91254-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="91254-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="91254-163">請連絡[UserEcho 用戶端支援小組](https://feedback.userecho.com/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="91254-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) tooget these values.</span></span> 

4. <span data-ttu-id="91254-164">在 [hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="91254-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_certificate.png) 

5. <span data-ttu-id="91254-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="91254-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91254-168">在 [hello **UserEcho 組態**區段中，按一下**設定 UserEcho** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="91254-168">On hello **UserEcho Configuration** section, click **Configure UserEcho** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="91254-169">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="91254-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_configure.png) 

7. <span data-ttu-id="91254-171">在另一個瀏覽器視窗中，系統管理員身分登入 tooyour UserEcho 公司網站。</span><span class="sxs-lookup"><span data-stu-id="91254-171">In another browser window, sign on tooyour UserEcho company site as an administrator.</span></span>

8. <span data-ttu-id="91254-172">在 hello 最上層顯示 hello 工具列中，按一下 [使用者名稱 tooexpand hello 功能表中，，然後按一下 [**安裝**。</span><span class="sxs-lookup"><span data-stu-id="91254-172">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 

9. <span data-ttu-id="91254-174">按一下 [整合] 。</span><span class="sxs-lookup"><span data-stu-id="91254-174">Click **Integrations**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 

10. <span data-ttu-id="91254-176">按一下 [網站]，然後按一下 [單一登入 (SAML2)]。</span><span class="sxs-lookup"><span data-stu-id="91254-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 

11. <span data-ttu-id="91254-178">在 [hello**單一登入 (SAML)**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="91254-178">On hello **Single sign-on (SAML)** page, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="91254-180">a.</span><span class="sxs-lookup"><span data-stu-id="91254-180">a.</span></span> <span data-ttu-id="91254-181">在 [已啟用 SAML] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="91254-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="91254-182">b.</span><span class="sxs-lookup"><span data-stu-id="91254-182">b.</span></span> <span data-ttu-id="91254-183">貼上**SAML 單一登入服務 URL**，其中您從 hello Azure 入口網站複製到 hello **SAML SSO URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="91254-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="91254-184">c.</span><span class="sxs-lookup"><span data-stu-id="91254-184">c.</span></span> <span data-ttu-id="91254-185">貼上**登出 URL**，其中您從 hello Azure 入口網站複製到 hello**遠端 logoout URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="91254-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="91254-186">d.</span><span class="sxs-lookup"><span data-stu-id="91254-186">d.</span></span> <span data-ttu-id="91254-187">開啟 [記事本]，複製 hello 內容，您所下載的憑證，然後將它貼到 hello **X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="91254-187">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="91254-188">e.</span><span class="sxs-lookup"><span data-stu-id="91254-188">e.</span></span> <span data-ttu-id="91254-189">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="91254-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="91254-190">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="91254-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="91254-191">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="91254-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="91254-192">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91254-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91254-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91254-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="91254-194">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="91254-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="91254-196">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91254-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="91254-197">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="91254-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="91254-199">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="91254-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="91254-201">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="91254-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="91254-203">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="91254-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91254-205">a.</span><span class="sxs-lookup"><span data-stu-id="91254-205">a.</span></span> <span data-ttu-id="91254-206">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="91254-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91254-207">b.</span><span class="sxs-lookup"><span data-stu-id="91254-207">b.</span></span> <span data-ttu-id="91254-208">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="91254-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91254-209">c.</span><span class="sxs-lookup"><span data-stu-id="91254-209">c.</span></span> <span data-ttu-id="91254-210">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="91254-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="91254-211">d.</span><span class="sxs-lookup"><span data-stu-id="91254-211">d.</span></span> <span data-ttu-id="91254-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="91254-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="91254-213">建立 UserEcho 測試使用者</span><span class="sxs-lookup"><span data-stu-id="91254-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="91254-214">hello 本節目標在於 toocreate UserEcho 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="91254-214">hello objective of this section is toocreate a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="91254-215">**toocreate 呼叫許 Simon UserEcho，在使用者執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91254-215">**toocreate a user called Britta Simon in UserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="91254-216">以系統管理員身分登入 tooyour UserEcho 公司網站。</span><span class="sxs-lookup"><span data-stu-id="91254-216">Sign-on tooyour UserEcho company site as an administrator.</span></span>

2. <span data-ttu-id="91254-217">在 hello 最上層顯示 hello 工具列中，按一下 [使用者名稱 tooexpand hello 功能表中，，然後按一下 [**安裝**。</span><span class="sxs-lookup"><span data-stu-id="91254-217">In hello toolbar on hello top, click your user name tooexpand hello menu, and then click **Setup**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png)

3. <span data-ttu-id="91254-219">按一下**使用者**，tooexpand hello**使用者**> 一節。</span><span class="sxs-lookup"><span data-stu-id="91254-219">Click **Users**, tooexpand hello **Users** section.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png)

4. <span data-ttu-id="91254-221">按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="91254-221">Click **Users**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png)

5. <span data-ttu-id="91254-223">按一下 [邀請新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="91254-223">Click **Invite a new user**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)

6. <span data-ttu-id="91254-225">在 [hello**邀請新使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="91254-225">On hello **Invite a new user** dialog, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="91254-227">a.</span><span class="sxs-lookup"><span data-stu-id="91254-227">a.</span></span> <span data-ttu-id="91254-228">在 [hello**名稱**文字方塊中，例如許 Simon hello 使用者類型名稱。</span><span class="sxs-lookup"><span data-stu-id="91254-228">In hello **Name** textbox, type name of hello user like Britta Simon.</span></span>
    
    <span data-ttu-id="91254-229">b.</span><span class="sxs-lookup"><span data-stu-id="91254-229">b.</span></span>  <span data-ttu-id="91254-230">在 [hello**電子郵件**文字方塊中，輸入 hello 電子郵件地址的使用者喜歡Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="91254-230">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="91254-231">c.</span><span class="sxs-lookup"><span data-stu-id="91254-231">c.</span></span> <span data-ttu-id="91254-232">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="91254-232">Click **Invite**.</span></span>

<span data-ttu-id="91254-233">TooBritta，可讓使用 UserEcho 她 toostart 已傳送邀請。</span><span class="sxs-lookup"><span data-stu-id="91254-233">An invitation is sent tooBritta, which enables her toostart using UserEcho.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="91254-234">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="91254-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="91254-235">在本節中，您可以授與存取 tooUserEcho 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="91254-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserEcho.</span></span>

![指派使用者][200] 

<span data-ttu-id="91254-237">**tooassign 許 Simon tooUserEcho，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="91254-237">**tooassign Britta Simon tooUserEcho, perform hello following steps:**</span></span>

1. <span data-ttu-id="91254-238">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="91254-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="91254-240">在 [hello] 應用程式清單中，選取**UserEcho**。</span><span class="sxs-lookup"><span data-stu-id="91254-240">In hello applications list, select **UserEcho**.</span></span>

    ![設定單一登入](./media/active-directory-saas-userecho-tutorial/tutorial_userecho_app.png) 

3. <span data-ttu-id="91254-242">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="91254-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="91254-244">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91254-244">Click **Add** button.</span></span> <span data-ttu-id="91254-245">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="91254-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="91254-247">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="91254-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="91254-248">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91254-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91254-249">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="91254-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91254-250">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="91254-250">Testing single sign-on</span></span>

<span data-ttu-id="91254-251">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="91254-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="91254-252">當您按一下 hello UserEcho 磚 hello 存取面板中的時，您應該取得自動登入 tooyour UserEcho 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91254-252">When you click hello UserEcho tile in hello Access Panel, you should get automatically signed-on tooyour UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91254-253">其他資源</span><span class="sxs-lookup"><span data-stu-id="91254-253">Additional resources</span></span>

* [<span data-ttu-id="91254-254">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91254-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91254-255">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="91254-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_203.png

