---
title: "教學課程：Azure Active Directory 與 Clarizen 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Clarizen 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="27884-103">教學課程：Azure Active Directory 與 Clarizen 整合</span><span class="sxs-lookup"><span data-stu-id="27884-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="27884-104">在此教學課程中，您學會如何 toointegrate Azure Active Directory (Azure AD)，與 Clarizen。</span><span class="sxs-lookup"><span data-stu-id="27884-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="27884-105">此整合提供下列您 hello 下列優點：</span><span class="sxs-lookup"><span data-stu-id="27884-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="27884-106">您可以控制，在 Azure AD 中擁有存取 tooClarizen。</span><span class="sxs-lookup"><span data-stu-id="27884-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="27884-107">您可以啟用自動登入 （單一登入） 的 tooClarizen 其 Azure AD 帳戶與您使用者 toobe。</span><span class="sxs-lookup"><span data-stu-id="27884-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="27884-108">您可以管理您的帳戶，在單一中央位置，hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="27884-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="27884-109">本教學課程中的 hello 案例包含兩個主要工作：</span><span class="sxs-lookup"><span data-stu-id="27884-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="27884-110">從 hello 圖庫新增 Clarizen。</span><span class="sxs-lookup"><span data-stu-id="27884-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="27884-111">設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27884-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="27884-112">若您想了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合的更多詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="27884-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27884-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="27884-113">Prerequisites</span></span>
<span data-ttu-id="27884-114">tooconfigure 與 Clarizen 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="27884-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="27884-115">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27884-115">An Azure AD subscription</span></span>
- <span data-ttu-id="27884-116">啟用單一登入的 Clarizen 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27884-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="27884-117">tootest hello 步驟在本教學課程，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="27884-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="27884-118">在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27884-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27884-119">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="27884-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="27884-120">如果您沒有 Azure AD 測試環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="27884-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="27884-121">從 hello 圖庫新增 Clarizen</span><span class="sxs-lookup"><span data-stu-id="27884-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="27884-122">tooconfigure hello 整合 Clarizen 的 Azure AD 中，從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單加入 Clarizen。</span><span class="sxs-lookup"><span data-stu-id="27884-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="27884-123">在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左的窗格中按一下 hello **Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="27884-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 圖示][1]

2. <span data-ttu-id="27884-125">按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="27884-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="27884-126">然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="27884-126">Then click **All applications**.</span></span>

    ![按一下 [企業應用程式] 和 [所有應用程式]][2]

3. <span data-ttu-id="27884-128">按一下 hello**新增**在 hello hello 對話方塊頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="27884-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![hello [新增] 按鈕][3]

4. <span data-ttu-id="27884-130">在 [hello] 搜尋方塊中，輸入**Clarizen**。</span><span class="sxs-lookup"><span data-stu-id="27884-130">In hello search box, type **Clarizen**.</span></span>

    ![Hello 搜尋方塊中輸入"Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="27884-132">在 [hello] 結果窗格中，選取 [ **Clarizen**，然後按一下 [**新增**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27884-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Hello 結果窗格中，選取 Clarizen](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="27884-134">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="27884-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="27884-135">在下列各節的 hello，設定並測試 Azure AD 單一登入 Clarizen 根據 hello 許 Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="27884-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="27884-136">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Clarizen 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="27884-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="27884-137">換句話說，Azure AD 使用者與 Clarizen 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="27884-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="27884-138">您建立此連結關聯性 hello 將值指派為**使用者名稱**做為 hello 值的 Azure AD 中**Username** Clarizen 中。</span><span class="sxs-lookup"><span data-stu-id="27884-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="27884-139">tooconfigure 和測試 Azure AD 單一登入與 Clarizen，完成下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="27884-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="27884-140">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="27884-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="27884-141">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)**許 Simon 與 Azure AD 單一登入 tootest。</span><span class="sxs-lookup"><span data-stu-id="27884-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27884-142">**[建立測試使用者 Clarizen](#create-a-clarizen-test-user) ** toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Clarizen 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="27884-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="27884-143">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27884-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27884-144">**[測試單一登入](#test-single-sign-on)** tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="27884-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="27884-145">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="27884-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="27884-146">啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Clarizen 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="27884-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="27884-147">在 Azure 入口網站上 hello hello **Clarizen**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="27884-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![按一下 [單一登入]][4]

2. <span data-ttu-id="27884-149">在 [hello**單一登入**對話方塊中，如**模式**，選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27884-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![選取 [SAML 登入]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="27884-151">在 [hello **Clarizen 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="27884-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![識別碼和回覆 URL 方塊](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="27884-153">a.</span><span class="sxs-lookup"><span data-stu-id="27884-153">a.</span></span> <span data-ttu-id="27884-154">在 [hello**識別碼**方塊中，做為型別 hello 值： **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="27884-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="27884-155">b.</span><span class="sxs-lookup"><span data-stu-id="27884-155">b.</span></span> <span data-ttu-id="27884-156">在 [hello**回覆 URL**方塊中，輸入 URL，使用下列模式的 hello: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="27884-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="27884-157">這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="27884-157">These are not hello real values.</span></span> <span data-ttu-id="27884-158">您已 toouse hello 實際識別項，而且回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="27884-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="27884-159">這裡我們建議您使用 hello 唯一字串值，如 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="27884-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="27884-160">tooget hello 實際的值，請連絡 hello [Clarizen 支援小組](https://success.clarizen.com/hc/en-us/requests/new)。</span><span class="sxs-lookup"><span data-stu-id="27884-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="27884-161">在 [hello **SAML 簽章憑證**區段中，按一下**建立新憑證**。</span><span class="sxs-lookup"><span data-stu-id="27884-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![按一下 [建立新的憑證]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="27884-163">在 [hello**建立新的憑證**對話方塊，按一下 hello 日曆圖示，然後選取到期日。</span><span class="sxs-lookup"><span data-stu-id="27884-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="27884-164">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="27884-164">Then click **Save**.</span></span>

    ![選取並儲存到期日](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="27884-166">在 [hello **SAML 簽章憑證**區段中，選取**啟用新的憑證**，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="27884-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![選取使 hello 新的憑證處於作用中的 hello 核取方塊](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="27884-168">在 [hello**變換憑證**對話方塊中，按一下 [**確定**。</span><span class="sxs-lookup"><span data-stu-id="27884-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![按一下 [確定] 您想 toomake hello 憑證 active tooconfirm](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="27884-170">在 [hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="27884-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![按一下 [憑證 (Base64)] toostart hello 下載](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="27884-172">在 [hello **Clarizen 組態**區段中，按一下**設定 Clarizen** tooopen hello**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="27884-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    ![按一下 [設定 Clarizen]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![[登入設定] 視窗，包括檔案和 URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="27884-175">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour Clarizen 公司網站。</span><span class="sxs-lookup"><span data-stu-id="27884-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="27884-176">按一下您的使用者名稱，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="27884-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="27884-177">![按一下您的使用者名稱底下的 [設定]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "設定")</span><span class="sxs-lookup"><span data-stu-id="27884-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="27884-178">按一下 hello**通用設定**] 索引標籤。然後下, 一步太**同盟驗證**，按一下 [**編輯**。</span><span class="sxs-lookup"><span data-stu-id="27884-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="27884-179">![[全域設定] 索引標籤](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "全域設定")</span><span class="sxs-lookup"><span data-stu-id="27884-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="27884-180">在 [hello**同盟驗證**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="27884-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="27884-181">![[同盟驗證] 對話方塊](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "同盟驗證")</span><span class="sxs-lookup"><span data-stu-id="27884-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="27884-182">a.</span><span class="sxs-lookup"><span data-stu-id="27884-182">a.</span></span> <span data-ttu-id="27884-183">選取 [啟用同盟驗證]。</span><span class="sxs-lookup"><span data-stu-id="27884-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="27884-184">b.</span><span class="sxs-lookup"><span data-stu-id="27884-184">b.</span></span> <span data-ttu-id="27884-185">按一下**上傳**tooupload 下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="27884-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="27884-186">c.</span><span class="sxs-lookup"><span data-stu-id="27884-186">c.</span></span> <span data-ttu-id="27884-187">在 [hello**登入 URL**方塊中，輸入 hello 值**SAML 單一登入服務 URL**從 hello Azure AD 應用程式設定] 視窗。</span><span class="sxs-lookup"><span data-stu-id="27884-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="27884-188">d.</span><span class="sxs-lookup"><span data-stu-id="27884-188">d.</span></span> <span data-ttu-id="27884-189">在 [hello**登出 URL**方塊中，輸入 hello 值**登出 URL**從 hello Azure AD 應用程式設定] 視窗。</span><span class="sxs-lookup"><span data-stu-id="27884-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="27884-190">e.</span><span class="sxs-lookup"><span data-stu-id="27884-190">e.</span></span> <span data-ttu-id="27884-191">選取 [使用 POST] 。</span><span class="sxs-lookup"><span data-stu-id="27884-191">Select **Use POST**.</span></span>

    <span data-ttu-id="27884-192">f.</span><span class="sxs-lookup"><span data-stu-id="27884-192">f.</span></span> <span data-ttu-id="27884-193">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="27884-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="27884-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="27884-194">Create an Azure AD test user</span></span>
<span data-ttu-id="27884-195">在 hello Azure 入口網站，建立稱為許 Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="27884-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Hello Azure AD 的測試使用者名稱和電子郵件地址][100]

1. <span data-ttu-id="27884-197">在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="27884-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 圖示](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="27884-199">按一下**使用者和群組**，然後按一下 [**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="27884-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    ![按一下 [使用者和群組] 與 [所有使用者]](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="27884-201">在 hello hello] 對話方塊的頂端，按一下**新增**tooopen hello**使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="27884-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="27884-203">在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="27884-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![在 [使用者] 對話方塊中填入名稱、電子郵件地址和密碼](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="27884-205">a.</span><span class="sxs-lookup"><span data-stu-id="27884-205">a.</span></span> <span data-ttu-id="27884-206">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="27884-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27884-207">b.</span><span class="sxs-lookup"><span data-stu-id="27884-207">b.</span></span> <span data-ttu-id="27884-208">在 [hello**使用者名**] 方塊中的 hello 許 Simon 帳戶類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="27884-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="27884-209">c.</span><span class="sxs-lookup"><span data-stu-id="27884-209">c.</span></span> <span data-ttu-id="27884-210">選取**顯示密碼**記下的 hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="27884-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="27884-211">d.</span><span class="sxs-lookup"><span data-stu-id="27884-211">d.</span></span> <span data-ttu-id="27884-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="27884-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="27884-213">建立 Clarizen 測試使用者</span><span class="sxs-lookup"><span data-stu-id="27884-213">Create a Clarizen test user</span></span>
<span data-ttu-id="27884-214">tooenable Azure AD 使用者 toosign tooClarizen 中的，您必須佈建使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="27884-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="27884-215">在 Clarizen 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="27884-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="27884-216">Tooyour Clarizen 公司網站管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="27884-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="27884-217">按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="27884-217">Click **People**.</span></span>

    <span data-ttu-id="27884-218">![按一下 [人員]](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "人員")</span><span class="sxs-lookup"><span data-stu-id="27884-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="27884-219">按一下 [邀請使用者] 。</span><span class="sxs-lookup"><span data-stu-id="27884-219">Click **Invite User**.</span></span>

    <span data-ttu-id="27884-220">![[邀請使用者] 按鈕](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "邀請使用者")</span><span class="sxs-lookup"><span data-stu-id="27884-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="27884-221">在 [hello**邀請人員**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="27884-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="27884-222">![[邀請人員] 對話方塊](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="27884-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="27884-223">a.</span><span class="sxs-lookup"><span data-stu-id="27884-223">a.</span></span> <span data-ttu-id="27884-224">在 [hello**電子郵件**] 方塊中的 hello 許 Simon 帳戶類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="27884-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="27884-225">b.</span><span class="sxs-lookup"><span data-stu-id="27884-225">b.</span></span> <span data-ttu-id="27884-226">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="27884-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="27884-227">hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="27884-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="27884-228">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="27884-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="27884-229">藉由授與他們存取 tooClarizen 可讓許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27884-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![已指派測試使用者][200]

1. <span data-ttu-id="27884-231">在 [hello Azure 入口網站，開啟 hello 應用程式檢視，瀏覽 toohello 目錄檢視，按一下 [**企業應用程式**，然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="27884-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![按一下 [企業應用程式] 和 [所有應用程式]][201]

2. <span data-ttu-id="27884-233">在 [hello] 應用程式清單中，選取**Clarizen**。</span><span class="sxs-lookup"><span data-stu-id="27884-233">In hello applications list, select **Clarizen**.</span></span>

    ![Hello 清單中選取 Clarizen](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="27884-235">在 [hello] 左窗格中，按一下 [**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="27884-235">In hello left pane, click **Users and groups**.</span></span>

    ![按一下 [使用者和群組]][202]

4. <span data-ttu-id="27884-237">按一下 hello**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27884-237">Click hello **Add** button.</span></span> <span data-ttu-id="27884-238">然後，在 hello**將作業加入**對話方塊中，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="27884-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![hello [新增] 按鈕和 hello"新增指派] 對話方塊][203]

5. <span data-ttu-id="27884-240">在 [hello**使用者和群組**對話方塊中，選取**許 Simon** hello 的使用者清單中。</span><span class="sxs-lookup"><span data-stu-id="27884-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="27884-241">在 [hello**使用者和群組**對話方塊方塊中，按一下 hello**選取**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27884-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="27884-242">在 [hello**將作業加入**對話方塊方塊中，按一下 hello**指派**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27884-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="27884-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="27884-243">Test single sign-on</span></span>
<span data-ttu-id="27884-244">使用存取面板 hello 測試 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="27884-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="27884-245">當您按一下 hello Clarizen 磚 hello 存取面板中的時，您應該會自動登入 tooyour Clarizen 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="27884-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27884-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="27884-246">Additional resources</span></span>

* [<span data-ttu-id="27884-247">如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="27884-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27884-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="27884-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
