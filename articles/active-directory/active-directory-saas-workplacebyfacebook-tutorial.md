---
title: "教學課程：Azure Active Directory 與 Workplace by Facebook 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與工作地點的 Facebook 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="01ca6-103">教學課程：Azure Active Directory 與 Workplace by Facebook 整合</span><span class="sxs-lookup"><span data-stu-id="01ca6-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="01ca6-104">在此教學課程中，您學會如何 toointegrate 由 Facebook 與 Azure Active Directory (Azure AD) 的工作場所。</span><span class="sxs-lookup"><span data-stu-id="01ca6-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01ca6-105">與 Azure AD 整合的 Facebook 的工作地點可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="01ca6-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="01ca6-106">您可以控制存取 tooWorkplace 由 Facebook 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="01ca6-106">You can control in Azure AD who has access tooWorkplace by Facebook</span></span>
- <span data-ttu-id="01ca6-107">您可以啟用您的使用者 tooautomatically get 登入 tooWorkplace 由 Facebook （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="01ca6-107">You can enable your users tooautomatically get signed-on tooWorkplace by Facebook (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01ca6-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="01ca6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="01ca6-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="01ca6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01ca6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="01ca6-110">Prerequisites</span></span>

<span data-ttu-id="01ca6-111">tooconfigure 由 Facebook 的工作場所的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="01ca6-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="01ca6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="01ca6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01ca6-113">已啟用 Workplace by Facebook 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="01ca6-113">A Workplace by Facebook single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="01ca6-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="01ca6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="01ca6-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="01ca6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01ca6-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="01ca6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="01ca6-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="01ca6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01ca6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="01ca6-118">Scenario description</span></span>
<span data-ttu-id="01ca6-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="01ca6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="01ca6-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="01ca6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01ca6-121">由 Facebook 從 hello 組件庫加入工作地點</span><span class="sxs-lookup"><span data-stu-id="01ca6-121">Adding Workplace by Facebook from hello gallery</span></span>
2. <span data-ttu-id="01ca6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="01ca6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="01ca6-123">由 Facebook 從 hello 組件庫加入工作地點</span><span class="sxs-lookup"><span data-stu-id="01ca6-123">Adding Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="01ca6-124">tooconfigure hello 整合工作地點的 Facebook 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd 由 Facebook 的工作場所。</span><span class="sxs-lookup"><span data-stu-id="01ca6-124">tooconfigure hello integration of Workplace by Facebook into Azure AD, you need tooadd Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="01ca6-125">**由 Facebook hello 圖庫中，從工作場所 tooadd 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="01ca6-125">**tooadd Workplace by Facebook from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="01ca6-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="01ca6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="01ca6-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="01ca6-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="01ca6-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="01ca6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="01ca6-133">在 [hello] 搜尋方塊中，輸入**工作地點的 Facebook**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-133">In hello search box, type **Workplace by Facebook**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. <span data-ttu-id="01ca6-135">在 hello [結果] 窗格中，選取**工作地點的 Facebook**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01ca6-135">In hello results panel, select **Workplace by Facebook**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01ca6-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="01ca6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="01ca6-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Workplace by Facebook 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="01ca6-138">In this section, you configure and test Azure AD single sign-on with Workplace by Facebook based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="01ca6-139">單一登入 toowork，Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者工作地點的 Facebook 都 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="01ca6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="01ca6-140">換句話說，Azure AD 使用者與工作地點的 Facebook 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="01ca6-140">In other words, a link relationship between an Azure AD user and hello related user in Workplace by Facebook needs toobe established.</span></span>

<span data-ttu-id="01ca6-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**由 Facebook 的工作地點中。</span><span class="sxs-lookup"><span data-stu-id="01ca6-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

<span data-ttu-id="01ca6-142">tooconfigure 和測試 Azure AD 單一登入的 Facebook 的工作場所，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="01ca6-142">tooconfigure and test Azure AD single sign-on with Workplace by Facebook, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="01ca6-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="01ca6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="01ca6-144">**[設定重新驗證頻率](#configuring-reauthentication-frequency)** -tooconfigure 工作場所 tooprompt SAML 檢查。</span><span class="sxs-lookup"><span data-stu-id="01ca6-144">**[Configuring Reauthentication Frequency](#configuring-reauthentication-frequency)** - tooconfigure Workplace tooprompt for a SAML check.</span></span>
3. <span data-ttu-id="01ca6-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="01ca6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="01ca6-146">**[建立 Facebook 測試使用者工作地點](#creating-a-workplace-by-facebook-test-user)** -toohave 許 Simon 由是連結的 toohello Azure AD 使用者表示法的 Facebook 的工作地點中對應項目。</span><span class="sxs-lookup"><span data-stu-id="01ca6-146">**[Creating a Workplace by Facebook test user](#creating-a-workplace-by-facebook-test-user)** - toohave a counterpart of Britta Simon in Workplace by Facebook that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="01ca6-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="01ca6-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="01ca6-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="01ca6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01ca6-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="01ca6-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="01ca6-150">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您工作地點中的 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01ca6-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workplace by Facebook application.</span></span>

<span data-ttu-id="01ca6-151">**tooconfigure Azure AD 單一登入的工作地點網路，由 Facebook，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="01ca6-151">**tooconfigure Azure AD single sign-on with Workplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="01ca6-152">在 Azure 入口網站上 hello hello**工作地點的 Facebook**應用程式整合頁面上，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-152">In hello Azure portal, on hello **Workplace by Facebook** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="01ca6-154">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="01ca6-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="01ca6-156">在 hello **Facebook 網域和 Url 的工作場所**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="01ca6-156">On hello **Workplace by Facebook Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    <span data-ttu-id="01ca6-158">a.</span><span class="sxs-lookup"><span data-stu-id="01ca6-158">a.</span></span> <span data-ttu-id="01ca6-159">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="01ca6-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.facebook.com`</span></span>

    <span data-ttu-id="01ca6-160">b.</span><span class="sxs-lookup"><span data-stu-id="01ca6-160">b.</span></span> <span data-ttu-id="01ca6-161">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://www.facebook.com/company/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="01ca6-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.facebook.com/company/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="01ca6-162">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="01ca6-162">These values are not hello real.</span></span> <span data-ttu-id="01ca6-163">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="01ca6-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="01ca6-164">請連絡[Facebook 用戶端支援小組的工作場所](https://workplace.fb.com/faq/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="01ca6-164">Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="01ca6-165">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="01ca6-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="01ca6-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="01ca6-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="01ca6-169">在 hello **Facebook 組態的工作場所**區段中，按一下**Facebook 所設定的工作場所**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="01ca6-169">On hello **Workplace by Facebook Configuration** section, click **Configure Workplace by Facebook** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="01ca6-170">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="01ca6-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. <span data-ttu-id="01ca6-172">在不同的網頁瀏覽器視窗中，登入 tooyour 由系統管理員身分的 Facebook 公司網站的工作場所。</span><span class="sxs-lookup"><span data-stu-id="01ca6-172">In a different web browser window, login tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="01ca6-173">Hello SAML 驗證程序的一部分，工作地點可能利用向上 too2.5 kb 大小順序 toopass 參數 tooAzure AD 中的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="01ca6-173">As part of hello SAML authentication process, Workplace may utilize query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="01ca6-174">在 [hello**公司儀表板**，go toohello**驗證**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="01ca6-174">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="01ca6-175">在下**SAML 驗證**，選取**只有 SSO** hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="01ca6-175">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="01ca6-176">從複製輸入的 hello 值**Facebook 組態的工作場所**hello hello 對應欄位中的 Azure 入口網站的區段：</span><span class="sxs-lookup"><span data-stu-id="01ca6-176">Input hello values copied from **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="01ca6-177">在**SAML URL**文字方塊中，貼上 hello 值**單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="01ca6-177">In **SAML URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="01ca6-178">在**SAML 簽發者 URL 文字方塊中**，貼上的 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="01ca6-178">In **SAML Issuer URL textbox**, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="01ca6-179">在**SAML 登出重新導向**（選擇性），貼上的 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="01ca6-179">In **SAML Logout Redirect** (Optional), paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
    *   <span data-ttu-id="01ca6-180">開啟您**base 64 編碼憑證**從 Azure 入口網站下載 [記事本] 中的 hello 內容複製到剪貼簿，並貼 toothe **SAML 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="01ca6-180">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** textbox.</span></span>

11. <span data-ttu-id="01ca6-181">您可能需要 tooenter hello 觀眾 URL 收件者 URL 和 ACS （判斷提示取用者服務） 的 URL 列在 hello **SAML 設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="01ca6-181">You may need tooenter hello Audience URL, Recipient URL, and ACS (Assertion Consumer Service) URL listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="01ca6-182">捲動 toohello hello 區段的底部，按一下 [hello**測試 SSO** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="01ca6-182">Scroll toohello bottom of hello section and click hello **Test SSO** button.</span></span> <span data-ttu-id="01ca6-183">快顯視窗中的這個結果隨即顯示，並會出現 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="01ca6-183">This results in a popup window appearing with Azure AD login page presented.</span></span> <span data-ttu-id="01ca6-184">輸入您的認證，在做為一般 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="01ca6-184">Enter your credentials in as normal tooauthenticate.</span></span> 

    <span data-ttu-id="01ca6-185">**疑難排解：**請從 Azure AD 傳回的 hello 電子郵件地址是 hello 與 hello 您用來登入的工作場所帳戶相同。</span><span class="sxs-lookup"><span data-stu-id="01ca6-185">**Troubleshooting:** Ensure hello email address being returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="01ca6-186">一旦 hello 測試已順利完成，請捲動 toohello hello 頁面的底部，然後按一下 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="01ca6-186">Once hello test has been completed successfully, scroll toohello bottom of hello page and click hello **Save** button.</span></span>

14. <span data-ttu-id="01ca6-187">現在，使用 Workplace 的所有使用者都將會看到進行驗證的 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="01ca6-187">All users using Workplace will now be presented with Azure AD login page for authentication.</span></span>

15. <span data-ttu-id="01ca6-188">**SAML 登出重新導向 (選擇性)** -</span><span class="sxs-lookup"><span data-stu-id="01ca6-188">**SAML Logout Redirect (optional)** -</span></span> 

    <span data-ttu-id="01ca6-189">您可以選擇 toooptionally 設定 SAML 登出 Url，可能會在 Azure AD 的登出頁面使用的 toopoint。</span><span class="sxs-lookup"><span data-stu-id="01ca6-189">You can choose toooptionally configure a SAML Logout Url, which can be used toopoint at Azure AD's logout page.</span></span> <span data-ttu-id="01ca6-190">當此設定已啟用並設定時，hello 使用者將無法再導向的 toohello 工作場所登出頁面。</span><span class="sxs-lookup"><span data-stu-id="01ca6-190">When this setting is enabled and configured, hello user will no longer be directed toohello Workplace logout page.</span></span> <span data-ttu-id="01ca6-191">相反地，hello 使用者將其加入 hello SAML 登出重新導向設定中的重新導向的 toohello url。</span><span class="sxs-lookup"><span data-stu-id="01ca6-191">Instead, hello user will be redirected toohello url that was added in hello SAML Logout Redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="01ca6-192">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="01ca6-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="01ca6-193">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="01ca6-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="01ca6-194">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="01ca6-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="configuring-reauthentication-frequency"></a><span data-ttu-id="01ca6-195">設定重新驗證頻率</span><span class="sxs-lookup"><span data-stu-id="01ca6-195">Configuring Reauthentication Frequency</span></span>

<span data-ttu-id="01ca6-196">您可以設定工作地點 tooprompt 的 SAML 檢查每一天，三天、 週、 兩週、 月或永遠不會。</span><span class="sxs-lookup"><span data-stu-id="01ca6-196">You can configure Workplace tooprompt for a SAML check every day, three days, week, two weeks, month or never.</span></span>

> [!NOTE] 
><span data-ttu-id="01ca6-197">hello hello SAML 檢查行動應用程式的最小值設定 tooone 週。</span><span class="sxs-lookup"><span data-stu-id="01ca6-197">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="01ca6-198">您也可以強制所有使用者使用 hello 按鈕重設 SAML： 需要 SAML 驗證所有使用者現在。</span><span class="sxs-lookup"><span data-stu-id="01ca6-198">You can also force a SAML reset for all users using hello button: Require SAML authentication for all users now.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01ca6-199">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="01ca6-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="01ca6-200">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="01ca6-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="01ca6-202">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="01ca6-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="01ca6-203">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="01ca6-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="01ca6-205">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="01ca6-207">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="01ca6-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01ca6-209">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="01ca6-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="01ca6-211">a.</span><span class="sxs-lookup"><span data-stu-id="01ca6-211">a.</span></span> <span data-ttu-id="01ca6-212">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01ca6-213">b.</span><span class="sxs-lookup"><span data-stu-id="01ca6-213">b.</span></span> <span data-ttu-id="01ca6-214">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="01ca6-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="01ca6-215">c.</span><span class="sxs-lookup"><span data-stu-id="01ca6-215">c.</span></span> <span data-ttu-id="01ca6-216">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="01ca6-217">d.</span><span class="sxs-lookup"><span data-stu-id="01ca6-217">d.</span></span> <span data-ttu-id="01ca6-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="01ca6-218">Click **Create**.</span></span>
 
### <a name="creating-a-workplace-by-facebook-test-user"></a><span data-ttu-id="01ca6-219">建立 Workplace by Facebook 測試使用者</span><span class="sxs-lookup"><span data-stu-id="01ca6-219">Creating a Workplace by Facebook test user</span></span>

<span data-ttu-id="01ca6-220">本節會在 Workplace by Facebook 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="01ca6-220">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="01ca6-221">Workplace by Facebook 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="01ca6-221">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="01ca6-222">在這一節沒有您需要進行的動作。</span><span class="sxs-lookup"><span data-stu-id="01ca6-222">There is no action for you in this section.</span></span> <span data-ttu-id="01ca6-223">如果使用者不存在的 Facebook 的工作地點中，建立一個新是當您嘗試 tooaccess 工作地點的 Facebook。</span><span class="sxs-lookup"><span data-stu-id="01ca6-223">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="01ca6-224">如果您需要以手動方式，請連絡使用者 toocreate [Facebook 用戶端支援小組的工作場所](https://workplace.fb.com/faq/)</span><span class="sxs-lookup"><span data-stu-id="01ca6-224">If you need toocreate a user manually, Contact [Workplace by Facebook Client support team](https://workplace.fb.com/faq/)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="01ca6-225">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="01ca6-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="01ca6-226">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooWorkplace 由 Facebook。</span><span class="sxs-lookup"><span data-stu-id="01ca6-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkplace by Facebook.</span></span>

![指派使用者][200] 

<span data-ttu-id="01ca6-228">**tooassign 許 Simon tooWorkplace 由 Facebook，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="01ca6-228">**tooassign Britta Simon tooWorkplace by Facebook, perform hello following steps:**</span></span>

1. <span data-ttu-id="01ca6-229">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="01ca6-231">在 [hello] 應用程式清單中，選取**工作地點的 Facebook**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-231">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![設定單一登入](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="01ca6-233">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="01ca6-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="01ca6-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="01ca6-235">Click **Add** button.</span></span> <span data-ttu-id="01ca6-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="01ca6-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="01ca6-238">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="01ca6-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="01ca6-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="01ca6-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="01ca6-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="01ca6-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="01ca6-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="01ca6-241">Testing single sign-on</span></span>

<span data-ttu-id="01ca6-242">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="01ca6-242">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>
<span data-ttu-id="01ca6-243">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="01ca6-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="01ca6-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="01ca6-244">Additional resources</span></span>

* [<span data-ttu-id="01ca6-245">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01ca6-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01ca6-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="01ca6-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="01ca6-247">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="01ca6-247">Configure User Provisioning</span></span>](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

