---
title: "教學課程：Azure Active Directory 與 Recognize 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和辨識之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="de585-103">教學課程：Azure Active Directory 與 Recognize 整合</span><span class="sxs-lookup"><span data-stu-id="de585-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="de585-104">在此教學課程中，您學會如何 toointegrate 辨識與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="de585-104">In this tutorial, you learn how toointegrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de585-105">與 Azure AD 整合辨識可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="de585-105">Integrating Recognize with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="de585-106">您可以控制存取 tooRecognize Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="de585-106">You can control in Azure AD who has access tooRecognize</span></span>
- <span data-ttu-id="de585-107">您可以啟用您的使用者 tooautomatically get 登入 tooRecognize （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="de585-107">You can enable your users tooautomatically get signed-on tooRecognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="de585-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="de585-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="de585-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="de585-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de585-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="de585-110">Prerequisites</span></span>

<span data-ttu-id="de585-111">tooconfigure Azure AD 整合辨識，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="de585-111">tooconfigure Azure AD integration with Recognize, you need hello following items:</span></span>

- <span data-ttu-id="de585-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de585-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de585-113">啟用 Recognize 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="de585-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de585-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="de585-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de585-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="de585-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de585-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="de585-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de585-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="de585-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de585-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="de585-118">Scenario description</span></span>
<span data-ttu-id="de585-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de585-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de585-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="de585-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de585-121">從 hello 圖庫加入辨識</span><span class="sxs-lookup"><span data-stu-id="de585-121">Adding Recognize from hello gallery</span></span>
2. <span data-ttu-id="de585-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de585-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-hello-gallery"></a><span data-ttu-id="de585-123">從 hello 圖庫加入辨識</span><span class="sxs-lookup"><span data-stu-id="de585-123">Adding Recognize from hello gallery</span></span>
<span data-ttu-id="de585-124">tooconfigure hello 整合辨識到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 辨識。</span><span class="sxs-lookup"><span data-stu-id="de585-124">tooconfigure hello integration of Recognize into Azure AD, you need tooadd Recognize from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="de585-125">**tooadd 辨識 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de585-125">**tooadd Recognize from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="de585-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="de585-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="de585-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="de585-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="de585-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="de585-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="de585-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="de585-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="de585-133">在 [hello] 搜尋方塊中，輸入**辨識**。</span><span class="sxs-lookup"><span data-stu-id="de585-133">In hello search box, type **Recognize**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="de585-135">在 hello 結果 窗格中，選取 **辨識**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="de585-135">In hello results panel, select **Recognize**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="de585-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de585-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="de585-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Recognize 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de585-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de585-139">單一登入 toowork，Azure AD 需要 tooknow hello 對應項目中辨識的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="de585-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Recognize is tooa user in Azure AD.</span></span> <span data-ttu-id="de585-140">換句話說，Azure AD 使用者與 hello 中辨識的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="de585-140">In other words, a link relationship between an Azure AD user and hello related user in Recognize needs toobe established.</span></span>

<span data-ttu-id="de585-141">辨識中, 指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="de585-141">In Recognize, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="de585-142">tooconfigure 和測試 Azure AD 單一登入辨識，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="de585-142">tooconfigure and test Azure AD single sign-on with Recognize, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="de585-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="de585-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="de585-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="de585-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de585-145">**[建立測試使用者辨識](#creating-a-recognize-test-user)** -toohave 許 Simon 辨識所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="de585-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - toohave a counterpart of Britta Simon in Recognize that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="de585-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de585-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de585-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="de585-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="de585-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="de585-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="de585-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並辨識應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="de585-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="de585-150">**tooconfigure Azure AD 單一登入以辨識，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de585-150">**tooconfigure Azure AD single sign-on with Recognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="de585-151">在 Azure 入口網站上 hello hello**辨識**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="de585-151">In hello Azure portal, on hello **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="de585-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de585-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="de585-155">在 hello**辨識的網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de585-155">On hello **Recognize Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="de585-157">a.</span><span class="sxs-lookup"><span data-stu-id="de585-157">a.</span></span> <span data-ttu-id="de585-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="de585-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="de585-159">b.</span><span class="sxs-lookup"><span data-stu-id="de585-159">b.</span></span> <span data-ttu-id="de585-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="de585-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="de585-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="de585-161">These values are not real.</span></span> <span data-ttu-id="de585-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="de585-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="de585-163">請連絡[辨識用戶端支援小組](mailto:support@recognizeapp.com)取得登入 URL，而且您可以從 hello SSO 設定 > 一節將說明在 hello 教學課程稍後開啟 hello 服務提供者中繼資料 URL 取得識別碼值。</span><span class="sxs-lookup"><span data-stu-id="de585-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening hello Service Provider Metadata URL from hello SSO Settings section that is explained later in hello tutorial.</span></span> <span data-ttu-id="de585-164">.</span><span class="sxs-lookup"><span data-stu-id="de585-164">.</span></span> 
 
4. <span data-ttu-id="de585-165">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="de585-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="de585-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="de585-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de585-169">在 hello**辨識組態**區段中，按一下**設定辨識**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="de585-169">On hello **Recognize Configuration** section, click **Configure Recognize** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="de585-170">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="de585-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="de585-172">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour 辨識租用戶。</span><span class="sxs-lookup"><span data-stu-id="de585-172">In a different web browser window, sign-on tooyour Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="de585-173">在 hello 右上角，按一下 **功能表**。</span><span class="sxs-lookup"><span data-stu-id="de585-173">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="de585-174">跳過**公司系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="de585-174">Go too**Company Admin**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="de585-176">在 hello 左側瀏覽窗格中，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="de585-176">On hello left navigation pane, click **Settings**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="de585-178">執行下列步驟 hello **SSO 設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="de585-178">Perform hello following steps on **SSO Settings** section.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="de585-180">a.</span><span class="sxs-lookup"><span data-stu-id="de585-180">a.</span></span> <span data-ttu-id="de585-181">將 **[啟用 SSO]** 選取為 **ON**。</span><span class="sxs-lookup"><span data-stu-id="de585-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="de585-182">b.</span><span class="sxs-lookup"><span data-stu-id="de585-182">b.</span></span> <span data-ttu-id="de585-183">在 hello **IDP 實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="de585-183">In hello **IDP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="de585-184">c.</span><span class="sxs-lookup"><span data-stu-id="de585-184">c.</span></span> <span data-ttu-id="de585-185">在 hello **Sso 目標 url**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="de585-185">In hello **Sso target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="de585-186">d.</span><span class="sxs-lookup"><span data-stu-id="de585-186">d.</span></span> <span data-ttu-id="de585-187">在 hello **Slo 目標 url**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="de585-187">In hello **Slo target url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="de585-188">e.</span><span class="sxs-lookup"><span data-stu-id="de585-188">e.</span></span> <span data-ttu-id="de585-189">開啟您下載**憑證 (Base64)** [記事本]，複製 hello 到剪貼簿，它的內容中，然後將它貼入 toohello**憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="de585-189">Open your downloaded **Certificate (Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="de585-190">f.</span><span class="sxs-lookup"><span data-stu-id="de585-190">f.</span></span> <span data-ttu-id="de585-191">按一下 hello**儲存設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de585-191">Click hello **Save settings** button.</span></span> 

11. <span data-ttu-id="de585-192">Hello 旁邊**SSO 設定**區段中，複製下的 hello URL**服務提供者中繼資料 url**。</span><span class="sxs-lookup"><span data-stu-id="de585-192">Beside hello **SSO Settings** section, copy hello URL under **Service Provider Metadata url**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="de585-194">開啟 hello**中繼資料 URL 連結**下空白瀏覽器 toodownload hello 中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="de585-194">Open hello **Metadata URL link** under a blank browser toodownload hello metadata document.</span></span> <span data-ttu-id="de585-195">然後從 hello 檔複製 hello EntityDescriptor value(entityID) 和中貼上**識別碼** 文字方塊中的**辨識的網域和 Url 的區段**Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="de585-195">Then copy hello EntityDescriptor value(entityID) from hello file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="de585-197">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="de585-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="de585-198">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="de585-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="de585-199">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="de585-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="de585-200">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de585-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="de585-201">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="de585-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="de585-203">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de585-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="de585-204">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="de585-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="de585-206">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="de585-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="de585-208">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="de585-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="de585-210">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="de585-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="de585-212">a.</span><span class="sxs-lookup"><span data-stu-id="de585-212">a.</span></span> <span data-ttu-id="de585-213">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="de585-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de585-214">b.</span><span class="sxs-lookup"><span data-stu-id="de585-214">b.</span></span> <span data-ttu-id="de585-215">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="de585-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="de585-216">c.</span><span class="sxs-lookup"><span data-stu-id="de585-216">c.</span></span> <span data-ttu-id="de585-217">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="de585-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="de585-218">d.</span><span class="sxs-lookup"><span data-stu-id="de585-218">d.</span></span> <span data-ttu-id="de585-219">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="de585-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="de585-220">建立 Recognize 測試使用者</span><span class="sxs-lookup"><span data-stu-id="de585-220">Creating a Recognize test user</span></span>

<span data-ttu-id="de585-221">在訂單 tooenable Azure AD 使用者 toolog 辨識成，它們必須佈建到辨識。</span><span class="sxs-lookup"><span data-stu-id="de585-221">In order tooenable Azure AD users toolog into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="de585-222">中的辨識 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="de585-222">In hello case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="de585-223">此應用程式不支援 SCIM 佈建，但有能夠佈建使用者的替代使用者同步處理作業。</span><span class="sxs-lookup"><span data-stu-id="de585-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="de585-224">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de585-224">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="de585-225">以管理員身分登入您的 Recognize 公司網站。</span><span class="sxs-lookup"><span data-stu-id="de585-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="de585-226">在 hello 右上角，按一下 **功能表**。</span><span class="sxs-lookup"><span data-stu-id="de585-226">On hello upper right corner, click **Menu**.</span></span> <span data-ttu-id="de585-227">跳過**公司系統管理員**。</span><span class="sxs-lookup"><span data-stu-id="de585-227">Go too**Company Admin**.</span></span>

3. <span data-ttu-id="de585-228">在 hello 左側瀏覽窗格中，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="de585-228">On hello left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="de585-229">執行下列步驟 hello**使用者同步**> 一節。</span><span class="sxs-lookup"><span data-stu-id="de585-229">Perform hello following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="de585-230">![新增使用者](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="de585-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="de585-231">a.</span><span class="sxs-lookup"><span data-stu-id="de585-231">a.</span></span> <span data-ttu-id="de585-232">對於 [已啟用同步處理] 選取 **ON**。</span><span class="sxs-lookup"><span data-stu-id="de585-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="de585-233">b.</span><span class="sxs-lookup"><span data-stu-id="de585-233">b.</span></span> <span data-ttu-id="de585-234">對於 [Choose sync provider] (選擇同步處理提供者)，選取 [Microsoft / Office 365]。</span><span class="sxs-lookup"><span data-stu-id="de585-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="de585-235">c.</span><span class="sxs-lookup"><span data-stu-id="de585-235">c.</span></span> <span data-ttu-id="de585-236">按一下 [Run User Sync] \(執行使用者同步處理)。</span><span class="sxs-lookup"><span data-stu-id="de585-236">Click **Run User Sync**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="de585-237">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="de585-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="de585-238">在本節中，您可以授與存取 tooRecognize 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="de585-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRecognize.</span></span>

![指派使用者][200] 

<span data-ttu-id="de585-240">**tooassign 許 Simon tooRecognize，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="de585-240">**tooassign Britta Simon tooRecognize, perform hello following steps:**</span></span>

1. <span data-ttu-id="de585-241">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="de585-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="de585-243">在 [hello] 應用程式清單中，選取**辨識**。</span><span class="sxs-lookup"><span data-stu-id="de585-243">In hello applications list, select **Recognize**.</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="de585-245">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="de585-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="de585-247">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de585-247">Click **Add** button.</span></span> <span data-ttu-id="de585-248">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="de585-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="de585-250">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="de585-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="de585-251">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de585-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de585-252">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="de585-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="de585-253">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="de585-253">Testing single sign-on</span></span>

<span data-ttu-id="de585-254">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="de585-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="de585-255">當您按一下 hello 辨識磚 hello 存取面板中的時，您應該取得自動登入 tooyour 辨識應用程式。</span><span class="sxs-lookup"><span data-stu-id="de585-255">When you click hello Recognize tile in hello Access Panel, you should get automatically signed-on tooyour Recognize application.</span></span> <span data-ttu-id="de585-256">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="de585-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="de585-257">其他資源</span><span class="sxs-lookup"><span data-stu-id="de585-257">Additional resources</span></span>

* [<span data-ttu-id="de585-258">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de585-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="de585-259">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="de585-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

