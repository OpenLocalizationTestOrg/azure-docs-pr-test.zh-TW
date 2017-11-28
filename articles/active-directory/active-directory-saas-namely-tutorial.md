---
title: "教學課程：將 Azure Active Directory 與 Namely 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間，也就是。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="c2ace-103">教學課程：將 Azure Active Directory 與 Namely 整合</span><span class="sxs-lookup"><span data-stu-id="c2ace-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="c2ace-104">在此教學課程中，您學會如何 toointegrate 也就是向 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="c2ace-104">In this tutorial, you learn how toointegrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c2ace-105">也就整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="c2ace-105">Integrating Namely with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c2ace-106">您可以控制存取 tooNamely Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="c2ace-106">You can control in Azure AD who has access tooNamely</span></span>
- <span data-ttu-id="c2ace-107">您可以啟用您的使用者 tooautomatically get 登入 tooNamely （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="c2ace-107">You can enable your users tooautomatically get signed-on tooNamely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c2ace-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c2ace-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c2ace-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c2ace-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2ace-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c2ace-110">Prerequisites</span></span>

<span data-ttu-id="c2ace-111">tooconfigure Azure AD 整合與那就是，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c2ace-111">tooconfigure Azure AD integration with Namely, you need hello following items:</span></span>

- <span data-ttu-id="c2ace-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c2ace-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c2ace-113">已啟用 Namely 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c2ace-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c2ace-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c2ace-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c2ace-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c2ace-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c2ace-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="c2ace-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c2ace-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="c2ace-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c2ace-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="c2ace-118">Scenario description</span></span>
<span data-ttu-id="c2ace-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c2ace-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c2ace-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c2ace-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c2ace-121">也就加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="c2ace-121">Adding Namely from hello gallery</span></span>
2. <span data-ttu-id="c2ace-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c2ace-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-hello-gallery"></a><span data-ttu-id="c2ace-123">也就加入從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="c2ace-123">Adding Namely from hello gallery</span></span>
<span data-ttu-id="c2ace-124">tooconfigure hello 整合至 Azure AD 也就是，您需要 tooadd 也就是從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單。</span><span class="sxs-lookup"><span data-stu-id="c2ace-124">tooconfigure hello integration of Namely into Azure AD, you need tooadd Namely from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c2ace-125">**tooadd 也就是從 hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c2ace-125">**tooadd Namely from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2ace-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c2ace-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c2ace-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c2ace-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c2ace-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c2ace-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c2ace-133">在 [hello] 搜尋方塊中，輸入**即**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-133">In hello search box, type **Namely**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="c2ace-135">在 hello 結果 窗格中，選取 **也就是**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2ace-135">In hello results panel, select **Namely**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c2ace-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c2ace-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c2ace-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Namely 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c2ace-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c2ace-139">單一登入 toowork，Azure AD 需要 tooknow hello 對應項目中的使用者也就是為 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c2ace-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Namely is tooa user in Azure AD.</span></span> <span data-ttu-id="c2ace-140">換句話說，Azure AD 使用者與 hello 中相關的使用者之間的連結關聯性也就是需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="c2ace-140">In other words, a link relationship between an Azure AD user and hello related user in Namely needs toobe established.</span></span>

<span data-ttu-id="c2ace-141">中也就是指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="c2ace-141">In Namely, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c2ace-142">tooconfigure 和測試 Azure AD 單一登入與那就是，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c2ace-142">tooconfigure and test Azure AD single sign-on with Namely, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c2ace-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c2ace-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c2ace-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c2ace-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c2ace-145">**[建立也就是測試使用者](#creating-a-namely-test-user)** -toohave 也就是也就是連結 toohello Azure AD 使用者表示法的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="c2ace-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - toohave a counterpart of Britta Simon in Namely that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c2ace-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c2ace-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c2ace-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c2ace-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c2ace-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c2ace-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c2ace-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入，您也就是應用程式。</span><span class="sxs-lookup"><span data-stu-id="c2ace-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="c2ace-150">**tooconfigure Azure AD 單一登入也就是執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c2ace-150">**tooconfigure Azure AD single sign-on with Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2ace-151">在 Azure 入口網站上 hello hello**即**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-151">In hello Azure portal, on hello **Namely** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c2ace-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c2ace-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="c2ace-155">在 hello**也就是網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c2ace-155">On hello **Namely Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="c2ace-157">a.</span><span class="sxs-lookup"><span data-stu-id="c2ace-157">a.</span></span> <span data-ttu-id="c2ace-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="c2ace-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="c2ace-159">b.</span><span class="sxs-lookup"><span data-stu-id="c2ace-159">b.</span></span> <span data-ttu-id="c2ace-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="c2ace-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c2ace-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="c2ace-161">These values are not real.</span></span> <span data-ttu-id="c2ace-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="c2ace-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c2ace-163">請連絡[也就是用戶端支援小組](https://www.namely.com/contact/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="c2ace-163">Contact [Namely Client support team](https://www.namely.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="c2ace-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="c2ace-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="c2ace-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="c2ace-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c2ace-168">在 hello**也就是組態**區段中，按一下**即設定**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="c2ace-168">On hello **Namely Configuration** section, click **Configure Namely** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c2ace-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="c2ace-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="c2ace-171">在另一個瀏覽器視窗中，身分登入 tooyour 也就是公司網站的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="c2ace-171">In another browser window, sign on tooyour Namely company site as an administrator.</span></span>

8. <span data-ttu-id="c2ace-172">在 hello hello 上方的工具列中按一下**公司**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-172">In hello toolbar on hello top, click **Company**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="c2ace-174">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c2ace-174">Click hello **Settings** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="c2ace-176">按一下 [SAML] 。</span><span class="sxs-lookup"><span data-stu-id="c2ace-176">Click **SAML**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="c2ace-178">在 hello **SAML 設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c2ace-178">On hello **SAML Settings** page, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="c2ace-180">a.</span><span class="sxs-lookup"><span data-stu-id="c2ace-180">a.</span></span> <span data-ttu-id="c2ace-181">按一下 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="c2ace-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="c2ace-182">b.</span><span class="sxs-lookup"><span data-stu-id="c2ace-182">b.</span></span> <span data-ttu-id="c2ace-183">在 hello**身分識別提供者 SSO url**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="c2ace-183">In hello **Identity provider SSO url** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="c2ace-184">c.</span><span class="sxs-lookup"><span data-stu-id="c2ace-184">c.</span></span> <span data-ttu-id="c2ace-185">開啟 [記事本]，複製 hello 內容，您所下載的憑證，然後將它貼到 hello**身分識別提供者憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="c2ace-185">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="c2ace-186">d.</span><span class="sxs-lookup"><span data-stu-id="c2ace-186">d.</span></span> <span data-ttu-id="c2ace-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c2ace-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c2ace-188">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="c2ace-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c2ace-189">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="c2ace-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c2ace-190">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c2ace-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c2ace-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c2ace-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="c2ace-192">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="c2ace-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c2ace-194">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c2ace-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2ace-195">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c2ace-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c2ace-197">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c2ace-199">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="c2ace-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c2ace-201">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c2ace-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c2ace-203">a.</span><span class="sxs-lookup"><span data-stu-id="c2ace-203">a.</span></span> <span data-ttu-id="c2ace-204">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c2ace-205">b.</span><span class="sxs-lookup"><span data-stu-id="c2ace-205">b.</span></span> <span data-ttu-id="c2ace-206">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c2ace-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c2ace-207">c.</span><span class="sxs-lookup"><span data-stu-id="c2ace-207">c.</span></span> <span data-ttu-id="c2ace-208">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c2ace-209">d.</span><span class="sxs-lookup"><span data-stu-id="c2ace-209">d.</span></span> <span data-ttu-id="c2ace-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c2ace-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="c2ace-211">建立 Namely 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c2ace-211">Creating a Namely test user</span></span>

<span data-ttu-id="c2ace-212">hello 本節目標在於 toocreate 中也就是呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="c2ace-212">hello objective of this section is toocreate a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="c2ace-213">**toocreate 使用者，也就是呼叫許 Simon 執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c2ace-213">**toocreate a user called Britta Simon in Namely, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2ace-214">登入 tooyour 也就是公司系統管理員身分的站台。</span><span class="sxs-lookup"><span data-stu-id="c2ace-214">Sign-on tooyour Namely company site as an administrator.</span></span>

2. <span data-ttu-id="c2ace-215">在 hello hello 上方的工具列中按一下**人員**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-215">In hello toolbar on hello top, click **People**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="c2ace-217">按一下 hello**目錄** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c2ace-217">Click hello **Directory** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="c2ace-219">按一下 [ **新增人員**]。</span><span class="sxs-lookup"><span data-stu-id="c2ace-219">Click **Add New Person**.</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="c2ace-221">在 [hello**新增人員**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c2ace-221">On hello **Add New Person** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="c2ace-222">a.</span><span class="sxs-lookup"><span data-stu-id="c2ace-222">a.</span></span> <span data-ttu-id="c2ace-223">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-223">In hello **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="c2ace-224">b.</span><span class="sxs-lookup"><span data-stu-id="c2ace-224">b.</span></span> <span data-ttu-id="c2ace-225">在 hello**姓氏**文字方塊中，輸入**Simon**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-225">In hello **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="c2ace-226">c.</span><span class="sxs-lookup"><span data-stu-id="c2ace-226">c.</span></span> <span data-ttu-id="c2ace-227">在 hello**電子郵件**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c2ace-227">In hello **Email** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c2ace-228">d.</span><span class="sxs-lookup"><span data-stu-id="c2ace-228">d.</span></span> <span data-ttu-id="c2ace-229">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c2ace-229">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c2ace-230">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="c2ace-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c2ace-231">在本節中，您可以授與存取 tooNamely 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c2ace-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNamely.</span></span>

![指派使用者][200] 

<span data-ttu-id="c2ace-233">**tooassign 許 Simon tooNamely，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c2ace-233">**tooassign Britta Simon tooNamely, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2ace-234">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c2ace-236">在 [hello] 應用程式清單中，選取**即**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-236">In hello applications list, select **Namely**.</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="c2ace-238">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c2ace-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c2ace-240">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c2ace-240">Click **Add** button.</span></span> <span data-ttu-id="c2ace-241">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c2ace-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c2ace-243">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="c2ace-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c2ace-244">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c2ace-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c2ace-245">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c2ace-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c2ace-246">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c2ace-246">Testing single sign-on</span></span>

<span data-ttu-id="c2ace-247">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="c2ace-247">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c2ace-248">當您按一下 hello 也就是在 hello 存取面板 磚中，您應該取得自動登入 tooyour 也就是應用程式</span><span class="sxs-lookup"><span data-stu-id="c2ace-248">When you click hello Namely tile in hello Access Panel, you should get automatically signed-on tooyour Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c2ace-249">其他資源</span><span class="sxs-lookup"><span data-stu-id="c2ace-249">Additional resources</span></span>

* [<span data-ttu-id="c2ace-250">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2ace-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c2ace-251">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c2ace-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

