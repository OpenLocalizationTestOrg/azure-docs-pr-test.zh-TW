---
title: "教學課程：Azure Active Directory 與 Workplace by Facebook 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與工作地點的 Facebook 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a><span data-ttu-id="769bf-103">教學課程：Azure Active Directory 與 Workplace by Facebook 整合</span><span class="sxs-lookup"><span data-stu-id="769bf-103">Tutorial: Azure Active Directory integration with Workplace by Facebook</span></span>

<span data-ttu-id="769bf-104">在此教學課程中，您學會如何 toointegrate 由 Facebook 與 Azure Active Directory (Azure AD) 的工作場所。</span><span class="sxs-lookup"><span data-stu-id="769bf-104">In this tutorial, you learn how toointegrate Workplace by Facebook with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="769bf-105">與 Azure AD 整合的 Facebook 的工作地點可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="769bf-105">Integrating Workplace by Facebook with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="769bf-106">您可以控制存取 tooWorkplace 由 Facebook 的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="769bf-106">You can control in Azure AD who has access tooWorkplace by Facebook.</span></span>
- <span data-ttu-id="769bf-107">您可以啟用您 tooautomatically 取得以登入 tooWorkplace Facebook （單一登入） 透過其 Azure AD 帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="769bf-107">You can enable your users tooautomatically get signed on tooWorkplace by Facebook (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="769bf-108">您可以管理您的帳戶，在單一中央位置： hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="769bf-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="769bf-109">如需軟體即服務 (SaaS) 應用程式與 Azure AD 整合的更多詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="769bf-109">For more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="769bf-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="769bf-110">Prerequisites</span></span>

<span data-ttu-id="769bf-111">tooconfigure 由 Facebook 的工作場所的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="769bf-111">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="769bf-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="769bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="769bf-113">已啟用 Workplace by Facebook (SSO) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="769bf-113">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="769bf-114">tootest hello 步驟在本教學課程，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="769bf-114">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="769bf-115">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="769bf-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="769bf-116">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="769bf-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="769bf-117">案例描述</span><span class="sxs-lookup"><span data-stu-id="769bf-117">Scenario description</span></span>
<span data-ttu-id="769bf-118">在本教學課程中，您會在測試環境中測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="769bf-118">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="769bf-119">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="769bf-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="769bf-120">加入工作地點的 Facebook 從 hello 組件庫。</span><span class="sxs-lookup"><span data-stu-id="769bf-120">Add Workplace by Facebook from hello gallery.</span></span>
2. <span data-ttu-id="769bf-121">設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="769bf-121">Configure and test Azure AD single sign-on.</span></span>

## <a name="add-workplace-by-facebook-from-hello-gallery"></a><span data-ttu-id="769bf-122">加入工作地點的 Facebook 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="769bf-122">Add Workplace by Facebook from hello gallery</span></span>
<span data-ttu-id="769bf-123">tooconfigure hello 整合工作地點的 Facebook 到 Azure AD 中，加入工作地點的 Facebook hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="769bf-123">tooconfigure hello integration of Workplace by Facebook into Azure AD, add Workplace by Facebook from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="769bf-124">在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左的窗格中選取**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="769bf-124">In hello [Azure portal](https://portal.azure.com), in hello left pane, select **Azure Active Directory**.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="769bf-126">瀏覽過**企業應用程式** > **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="769bf-126">Browse too**Enterprise applications** > **All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="769bf-128">tooadd hello 新應用程式，選取**新的應用程式**hello 最上層顯示 hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="769bf-128">tooadd hello new application, select **New application** on hello top of hello dialog box.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="769bf-130">Hello 搜尋方塊中，輸入**工作地點的 Facebook**，然後選取**工作地點的 Facebook**從結果中。</span><span class="sxs-lookup"><span data-stu-id="769bf-130">In hello search box, type **Workplace by Facebook**, and select **Workplace by Facebook** from results.</span></span> <span data-ttu-id="769bf-131">然後選取**新增**，tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="769bf-131">Then select **Add**, tooadd hello application.</span></span>

    ![由 Facebook hello [結果] 清單中的工作場所](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="769bf-133">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="769bf-133">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="769bf-134">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Workplace by Facebook 搭配運作的 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="769bf-134">In this section, you configure and test Azure AD SSO with Workplace by Facebook, based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="769bf-135">SSO toowork Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者工作地點的 Facebook 都 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="769bf-135">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Workplace by Facebook is tooa user in Azure AD.</span></span> <span data-ttu-id="769bf-136">換句話說，您應該建立 Azure AD 使用者與工作地點的 Facebook 中的 hello 相關的使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="769bf-136">In other words, a linked relationship between an Azure AD user and hello related user in Workplace by Facebook should be established.</span></span>

<span data-ttu-id="769bf-137">此關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**由 Facebook 的工作地點中。</span><span class="sxs-lookup"><span data-stu-id="769bf-137">Establish this relationship by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workplace by Facebook.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="769bf-138">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="769bf-138">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="769bf-139">在本節中，hello Azure 入口網站中啟用 Azure AD 的 SSO 與您工作地點中設定 SSO 的 Facebook 應用程式。</span><span class="sxs-lookup"><span data-stu-id="769bf-139">In this section, you enable Azure AD SSO in hello Azure portal, and you configure SSO in your Workplace by Facebook application.</span></span>

1. <span data-ttu-id="769bf-140">在 Azure 入口網站上 hello hello**工作地點的 Facebook**應用程式整合頁面上，選取**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="769bf-140">In hello Azure portal, on hello **Workplace by Facebook** application integration page, select **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="769bf-142">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable SSO。</span><span class="sxs-lookup"><span data-stu-id="769bf-142">In hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. <span data-ttu-id="769bf-144">在 hello **Facebook 網域和 Url 的工作場所**區段中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="769bf-144">In hello **Workplace by Facebook Domain and URLs** section, do hello following:</span></span>

    <span data-ttu-id="769bf-145">a.</span><span class="sxs-lookup"><span data-stu-id="769bf-145">a.</span></span> <span data-ttu-id="769bf-146">在 hello**登入 URL**文字方塊中，輸入使用下列模式的 hello 的 URL:`https://<company subdomain>.facebook.com`</span><span class="sxs-lookup"><span data-stu-id="769bf-146">In hello **Sign-on URL** text box, type a URL that uses hello following pattern: `https://<company subdomain>.facebook.com`</span></span>

    <span data-ttu-id="769bf-147">b.</span><span class="sxs-lookup"><span data-stu-id="769bf-147">b.</span></span> <span data-ttu-id="769bf-148">在 hello**識別碼**文字方塊中，輸入使用下列模式的 hello 的 URL:`https://www.facebook.com/company/<scim company id>`</span><span class="sxs-lookup"><span data-stu-id="769bf-148">In hello **Identifier** text box, type a URL that uses hello following pattern: `https://www.facebook.com/company/<scim company id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="769bf-149">這些值僅為範例。</span><span class="sxs-lookup"><span data-stu-id="769bf-149">These values are an example only.</span></span> <span data-ttu-id="769bf-150">更新這些值與 hello 實際登入 URL 和識別碼。</span><span class="sxs-lookup"><span data-stu-id="769bf-150">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="769bf-151">連絡 hello [Facebook 用戶端支援小組的工作場所](https://workplace.fb.com/faq/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="769bf-151">Contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/) tooget these values.</span></span> 

4. <span data-ttu-id="769bf-152">在 hello **SAML 簽章憑證**區段中，選取**憑證 (Base64)**，然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="769bf-152">In hello **SAML Signing Certificate** section, select **Certificate (Base64)**, and then save hello certificate file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. <span data-ttu-id="769bf-154">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="769bf-154">Select **Save**.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="769bf-156">在 hello **Facebook 組態的工作場所**區段中，選取**Facebook 所設定的工作場所**tooopen hello**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="769bf-156">In hello **Workplace by Facebook Configuration** section, select **Configure Workplace by Facebook** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="769bf-157">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考**> 一節。</span><span class="sxs-lookup"><span data-stu-id="769bf-157">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Workplace by Facebook 設定](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. <span data-ttu-id="769bf-159">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Facebook 公司網站的工作場所。</span><span class="sxs-lookup"><span data-stu-id="769bf-159">In a different web browser window, sign in tooyour Workplace by Facebook company site as an administrator.</span></span>
  
   > [!NOTE] 
   > <span data-ttu-id="769bf-160">Hello SAML 驗證程序的一部分，工作地點可以使用向上 too2.5 kb 為單位的查詢字串的大小順序 toopass 參數 tooAzure AD 中。</span><span class="sxs-lookup"><span data-stu-id="769bf-160">As part of hello SAML authentication process, Workplace can use query strings of up too2.5 kilobytes in size in order toopass parameters tooAzure AD.</span></span>

8. <span data-ttu-id="769bf-161">在 [hello**公司儀表板**，go toohello**驗證**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="769bf-161">In hello **Company Dashboard**, go toohello **Authentication** tab.</span></span>

9. <span data-ttu-id="769bf-162">在下**SAML 驗證**，選取**只有 SSO** hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="769bf-162">Under **SAML Authentication**, select **SSO Only** from hello drop-down list.</span></span>

10. <span data-ttu-id="769bf-163">輸入 hello 值從 hello 複製**Facebook 組態的工作場所**hello hello 對應欄位中的 Azure 入口網站的區段：</span><span class="sxs-lookup"><span data-stu-id="769bf-163">Enter hello values copied from hello **Workplace by Facebook Configuration** section of hello Azure portal into hello corresponding fields:</span></span>

    *   <span data-ttu-id="769bf-164">在**SAML URL**  文字方塊中，貼上 hello 值**單一登入服務 URL**，從 hello Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="769bf-164">In the **SAML URL** text box, paste hello value of **Single Sign-On Service URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="769bf-165">在**SAML 簽發者 URL**  文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 hello Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="769bf-165">In the **SAML Issuer URL** text box, paste hello value of **SAML Entity ID**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="769bf-166">在**SAML 登出重新導向 （選擇性）**，貼上的 hello 值**登出 URL**，從 hello Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="769bf-166">In **SAML Logout Redirect (optional)**, paste hello value of **Sign-Out URL**, which you have copied from hello Azure portal.</span></span>
    *   <span data-ttu-id="769bf-167">開啟您**base 64 編碼憑證**，在 [記事本]，從 hello Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="769bf-167">Open your **base-64 encoded certificate** in Notepad, downloaded from hello Azure portal.</span></span> <span data-ttu-id="769bf-168">Hello 內容複製到剪貼簿，然後將它貼入 toothe **SAML 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="769bf-168">Copy hello content of it into your clipboard, and then paste it toothe **SAML Certificate** text box.</span></span>

11. <span data-ttu-id="769bf-169">您可能需要 tooenter hello 觀眾 URL、 收件者的 URL 和 ACS （判斷提示取用者服務） URL，列在 hello **SAML 設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="769bf-169">You might need tooenter hello audience URL, recipient URL, and ACS (Assertion Consumer Service) URL, listed under hello **SAML Configuration** section.</span></span>

12. <span data-ttu-id="769bf-170">捲動 toohello 底部 hello 區段中，並選取**測試 SSO**。</span><span class="sxs-lookup"><span data-stu-id="769bf-170">Scroll toohello bottom of hello section, and select **Test SSO**.</span></span> <span data-ttu-id="769bf-171">快顯視窗隨即出現，並 hello Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="769bf-171">A pop-up window appears, with hello Azure AD sign-in page.</span></span> <span data-ttu-id="769bf-172">tooauthenticate，像平常一樣，輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="769bf-172">tooauthenticate, enter your credentials as normal.</span></span> <span data-ttu-id="769bf-173">請從 Azure AD 傳回的 hello 電子郵件地址是 hello 與 hello 您用來登入的工作場所帳戶相同。</span><span class="sxs-lookup"><span data-stu-id="769bf-173">Ensure hello email address returned back from Azure AD is hello same as hello Workplace account you are logged in with.</span></span>

13. <span data-ttu-id="769bf-174">如果 hello 測試成功完成後，捲動 toohello hello 頁面並選取底部**儲存**。</span><span class="sxs-lookup"><span data-stu-id="769bf-174">If hello test has finished successfully, scroll toohello bottom of hello page and select **Save**.</span></span>

14. <span data-ttu-id="769bf-175">使用 Workplace 的所有使用者現在都會看到進行驗證的 Azure AD 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="769bf-175">Anyone using Workplace is now presented with Azure AD sign-in page for authentication.</span></span>

<span data-ttu-id="769bf-176">您可以選擇 tooconfigure URL，可以在 hello Azure AD 的登出頁面使用的 toopoint SAML 登出。</span><span class="sxs-lookup"><span data-stu-id="769bf-176">You can choose tooconfigure a SAML sign out URL, which can be used toopoint at hello Azure AD sign-out page.</span></span> <span data-ttu-id="769bf-177">當此設定已啟用並設定時，hello 使用者已不再導向的 toohello 工作地點的登出頁面。</span><span class="sxs-lookup"><span data-stu-id="769bf-177">When this setting is enabled and configured, hello user is no longer directed toohello Workplace sign-out page.</span></span> <span data-ttu-id="769bf-178">相反地，hello 使用者是已加入 hello SAML 登出重新導向設定中的重新導向的 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="769bf-178">Instead, hello user is redirected toohello URL that was added in hello SAML sign-out redirect setting.</span></span>


> [!TIP]
> <span data-ttu-id="769bf-179">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="769bf-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app.</span></span> <span data-ttu-id="769bf-180">加入此應用程式從 hello 之後**Active Directory** > **企業應用程式**區段中，只需選取 hello**單一登入** 索引標籤，並存取 hello內嵌文件，透過 hello**組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="769bf-180">After adding this app from hello **Active Directory** > **Enterprise Applications** section, simply select hello **Single Sign-On** tab, and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="769bf-181">閱讀更多有關 hello embedded 文件功能的 hello [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="769bf-181">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="configure-reauthentication-frequency"></a><span data-ttu-id="769bf-182">設定重新驗證頻率</span><span class="sxs-lookup"><span data-stu-id="769bf-182">Configure reauthentication frequency</span></span>

<span data-ttu-id="769bf-183">您可以設定 SAML 檢查每一天，三天一週、 兩週，一個月的工作場所 tooprompt 或永遠不會。</span><span class="sxs-lookup"><span data-stu-id="769bf-183">You can configure Workplace tooprompt for a SAML check every day, three days, one week, two weeks, one month, or never.</span></span>

> [!NOTE] 
><span data-ttu-id="769bf-184">hello hello SAML 檢查行動應用程式的最小值設定 tooone 週。</span><span class="sxs-lookup"><span data-stu-id="769bf-184">hello minimum value for hello SAML check on mobile applications is set tooone week.</span></span>

<span data-ttu-id="769bf-185">您也可以強制所有使用者重設 SAML。</span><span class="sxs-lookup"><span data-stu-id="769bf-185">You can also force a SAML reset for all users.</span></span> <span data-ttu-id="769bf-186">toodo，使用 hello**需要 SAML 驗證所有使用者現在** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="769bf-186">toodo this, use hello **Require SAML authentication for all users now** button.</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="769bf-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="769bf-187">Create an Azure AD test user</span></span>
<span data-ttu-id="769bf-188">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="769bf-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

1. <span data-ttu-id="769bf-190">在 hello **Azure 入口網站**，在 hello 左的窗格中選取**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="769bf-190">In hello **Azure portal**, in hello left pane, select **Azure Active Directory**.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="769bf-192">toodisplay hello 使用者清單，請移過**使用者和群組**，然後選取**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="769bf-192">toodisplay hello list of users, go too**Users and groups**, and select **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="769bf-194">tooopen hello**使用者**對話方塊中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="769bf-194">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="769bf-196">在 hello**使用者**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="769bf-196">In hello **User** dialog box, do hello following:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="769bf-198">a.</span><span class="sxs-lookup"><span data-stu-id="769bf-198">a.</span></span> <span data-ttu-id="769bf-199">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="769bf-199">In hello **Name** text box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="769bf-200">b.</span><span class="sxs-lookup"><span data-stu-id="769bf-200">b.</span></span> <span data-ttu-id="769bf-201">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="769bf-201">In hello **User name** text box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="769bf-202">c.</span><span class="sxs-lookup"><span data-stu-id="769bf-202">c.</span></span> <span data-ttu-id="769bf-203">選取 [顯示密碼]，並將它寫下來。</span><span class="sxs-lookup"><span data-stu-id="769bf-203">Select **Show Password**, and write it down.</span></span>

    <span data-ttu-id="769bf-204">d.</span><span class="sxs-lookup"><span data-stu-id="769bf-204">d.</span></span> <span data-ttu-id="769bf-205">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="769bf-205">Select **Create**.</span></span>
 
### <a name="create-a-workplace-by-facebook-test-user"></a><span data-ttu-id="769bf-206">建立 Workplace by Facebook 測試使用者</span><span class="sxs-lookup"><span data-stu-id="769bf-206">Create a Workplace by Facebook test user</span></span>

<span data-ttu-id="769bf-207">本節會在 Workplace by Facebook 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="769bf-207">In this section, a user called Britta Simon is created in Workplace by Facebook.</span></span> <span data-ttu-id="769bf-208">Workplace by Facebook 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="769bf-208">Workplace by Facebook supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="769bf-209">在這一節沒有您需要進行的動作。</span><span class="sxs-lookup"><span data-stu-id="769bf-209">There is no action for you in this section.</span></span> <span data-ttu-id="769bf-210">如果使用者不存在的 Facebook 的工作地點中，建立一個新是當您嘗試 tooaccess 工作地點的 Facebook。</span><span class="sxs-lookup"><span data-stu-id="769bf-210">If a user doesn't exist in Workplace by Facebook, a new one is created when you attempt tooaccess Workplace by Facebook.</span></span>

>[!Note]
><span data-ttu-id="769bf-211">若要手動 toocreate 使用者，請連絡 hello [Facebook 用戶端支援小組的工作場所](https://workplace.fb.com/faq/)。</span><span class="sxs-lookup"><span data-stu-id="769bf-211">If you need toocreate a user manually, contact hello [Workplace by Facebook Client support team](https://workplace.fb.com/faq/).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="769bf-212">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="769bf-212">Assign hello Azure AD test user</span></span>

<span data-ttu-id="769bf-213">在本節中，以啟用許 Simon toouse Azure SSO 授與存取 tooWorkplace 由 Facebook。</span><span class="sxs-lookup"><span data-stu-id="769bf-213">In this section, you enable Britta Simon toouse Azure SSO by granting access tooWorkplace by Facebook.</span></span>

![指派使用者][200] 

1. <span data-ttu-id="769bf-215">在 hello Azure 入口網站，開啟 hello 應用程式檢視。</span><span class="sxs-lookup"><span data-stu-id="769bf-215">In hello Azure portal, open hello applications view.</span></span> <span data-ttu-id="769bf-216">移 toohello 目錄檢視，請移過**企業應用程式**，然後選取**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="769bf-216">Go toohello directory view, go too**Enterprise applications**, and then select **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="769bf-218">在 [hello] 應用程式清單中，選取**工作地點的 Facebook**。</span><span class="sxs-lookup"><span data-stu-id="769bf-218">In hello applications list, select **Workplace by Facebook**.</span></span>

    ![Facebook hello 應用程式清單中每個連結的 hello 工作場所](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. <span data-ttu-id="769bf-220">在左側 hello hello 功能表中選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="769bf-220">In hello menu on hello left, select **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="769bf-222">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="769bf-222">Select **Add**.</span></span> <span data-ttu-id="769bf-223">然後，在 hello**將作業加入**窗格中，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="769bf-223">Then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="769bf-225">在 [hello**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="769bf-225">In hello **Users and groups** dialog box, select **Britta Simon** in hello users list.</span></span>

6. <span data-ttu-id="769bf-226">在 hello**使用者和群組**對話方塊中，選取**選取**。</span><span class="sxs-lookup"><span data-stu-id="769bf-226">In hello **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="769bf-227">在 hello**將作業加入**對話方塊中，選取**指派**。</span><span class="sxs-lookup"><span data-stu-id="769bf-227">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="769bf-228">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="769bf-228">Test single sign-on</span></span>

<span data-ttu-id="769bf-229">如果您想 tootest SSO 設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="769bf-229">If you want tootest your SSO settings, open hello Access Panel.</span></span>
<span data-ttu-id="769bf-230">如需詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="769bf-230">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="769bf-231">後續步驟</span><span class="sxs-lookup"><span data-stu-id="769bf-231">Next steps</span></span>

* <span data-ttu-id="769bf-232">請參閱 hello[如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory](active-directory-saas-tutorial-list.md)。</span><span class="sxs-lookup"><span data-stu-id="769bf-232">See hello [list of tutorials on how toointegrate SaaS Apps with Azure Active Directory](active-directory-saas-tutorial-list.md).</span></span>
* <span data-ttu-id="769bf-233">閱讀[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="769bf-233">Read [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>
* <span data-ttu-id="769bf-234">深入了解如何太[設定使用者佈建](active-directory-saas-facebook-at-work-provisioning-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="769bf-234">Learn more about how too[configure user provisioning](active-directory-saas-facebook-at-work-provisioning-tutorial.md).</span></span>



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

