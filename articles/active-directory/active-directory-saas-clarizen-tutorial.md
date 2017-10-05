---
title: "教學課程：Azure Active Directory 與 Clarizen 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Clarizen 之間的單一登入。"
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
ms.openlocfilehash: 574c6877bddac8be7d6d541bfabbdc10f6be3101
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="9cbe9-103">教學課程：Azure Active Directory 與 Clarizen 整合</span><span class="sxs-lookup"><span data-stu-id="9cbe9-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="9cbe9-104">在本教學課程中，您會了解如何整合 Azure Active Directory (Azure AD) 與 Clarizen。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-104">In this tutorial, you learn how to integrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="9cbe9-105">這項整合提供下列優點︰</span><span class="sxs-lookup"><span data-stu-id="9cbe9-105">This integration gives you the following benefits:</span></span>

- <span data-ttu-id="9cbe9-106">您可以在 Azure AD 中控制可存取 Clarizen 的人員。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-106">You can control, in Azure AD, who has access to Clarizen.</span></span>
- <span data-ttu-id="9cbe9-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Clarizen (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-107">You can enable your users to be automatically signed in to Clarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9cbe9-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-108">You can manage your accounts in one central location, the Azure portal.</span></span>

<span data-ttu-id="9cbe9-109">本教學課程中的案例由二個主要工作組成：</span><span class="sxs-lookup"><span data-stu-id="9cbe9-109">The scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="9cbe9-110">從資源庫新增 Clarizen。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-110">Add Clarizen from the gallery.</span></span>
2. <span data-ttu-id="9cbe9-111">設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="9cbe9-112">若您想了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合的更多詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cbe9-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="9cbe9-113">Prerequisites</span></span>
<span data-ttu-id="9cbe9-114">若要設定與 Clarizen 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="9cbe9-114">To configure Azure AD integration with Clarizen, you need the following items:</span></span>

- <span data-ttu-id="9cbe9-115">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9cbe9-115">An Azure AD subscription</span></span>
- <span data-ttu-id="9cbe9-116">啟用單一登入的 Clarizen 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9cbe9-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="9cbe9-117">若要測試本教學課程中的步驟，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="9cbe9-117">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="9cbe9-118">在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cbe9-119">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9cbe9-120">如果您沒有 Azure AD 測試環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-the-gallery"></a><span data-ttu-id="9cbe9-121">從資源庫新增 Clarizen</span><span class="sxs-lookup"><span data-stu-id="9cbe9-121">Add Clarizen from the gallery</span></span>
<span data-ttu-id="9cbe9-122">若要設定 Clarizen 與 Azure AD 整合，從資源庫將 Clarizen 新增至受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-122">To configure the integration of Clarizen into Azure AD, add Clarizen from the gallery to your list of managed SaaS apps.</span></span>

1. <span data-ttu-id="9cbe9-123">在 [Azure 入口網站](https://portal.azure.com)的左窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 圖示][1]

2. <span data-ttu-id="9cbe9-125">按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="9cbe9-126">然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-126">Then click **All applications**.</span></span>

    ![按一下 [企業應用程式] 和 [所有應用程式]][2]

3. <span data-ttu-id="9cbe9-128">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-128">Click the **Add** button at the top of the dialog box.</span></span>

    ![[新增] 按鈕][3]

4. <span data-ttu-id="9cbe9-130">在搜尋方塊中，輸入 **Clarizen**。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-130">In the search box, type **Clarizen**.</span></span>

    ![在搜尋方塊中，輸入「Clarizen」](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="9cbe9-132">在結果窗格中，選取 [Clarizen]，然後按一下 [新增] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-132">In the results pane, select **Clarizen**, and then click **Add** to add the application.</span></span>

    ![在結果窗格中選取 Clarizen](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9cbe9-134">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9cbe9-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9cbe9-135">在下列章節中，您會以 Britta Simon 的測試使用者身分，使用 Clarizen 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-135">In the following sections, you configure and test Azure AD single sign-on with Clarizen based on the test user Britta Simon.</span></span>

<span data-ttu-id="9cbe9-136">若要讓單一登入運作，Azure AD 必須知道 Clarizen 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Clarizen is to a user in Azure AD.</span></span> <span data-ttu-id="9cbe9-137">換句話說，必須建立 Azure AD 使用者和 Clarizen 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-137">In other words, a link relationship between an Azure AD user and the related user in Clarizen needs to be established.</span></span> <span data-ttu-id="9cbe9-138">將 Azure AD 中**使用者名稱**的值指派為 Clarizen 中 **Username** 的值，即可建立此連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-138">You establish this link relationship by assigning the value of **user name** in Azure AD as the value of **Username** in Clarizen.</span></span>

<span data-ttu-id="9cbe9-139">若要設定及測試與 Clarizen 搭配運作的 Azure AD 單一登入，完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="9cbe9-139">To configure and test Azure AD single sign-on with Clarizen, complete the following building blocks:</span></span>

1. <span data-ttu-id="9cbe9-140">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)**，讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9cbe9-141">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)**，以使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cbe9-142">**[建立 Clarizen 測試使用者](#create-a-clarizen-test-user)**，使 Clarizen 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** to have a counterpart of Britta Simon in Clarizen that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9cbe9-143">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)**，讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cbe9-144">**[測試單一登入](#test-single-sign-on)**驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-144">**[Test single sign-on](#test-single-sign-on)** to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9cbe9-145">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9cbe9-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="9cbe9-146">在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Clarizen 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-146">Enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="9cbe9-147">在 Azure 入口網站的 [Clarizen] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-147">In the Azure portal, on the **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![按一下 [單一登入]][4]

2. <span data-ttu-id="9cbe9-149">在 [單一登入] 對話方塊上，選取 [SAML 登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-149">In the **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![選取 [SAML 登入]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="9cbe9-151">在 [Clarizen 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9cbe9-151">In the **Clarizen Domain and URLs** section, perform the following steps:</span></span>

    ![識別碼和回覆 URL 方塊](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="9cbe9-153">a.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-153">a.</span></span> <span data-ttu-id="9cbe9-154">在 [識別碼] 方塊中，以下列形式輸入值：[Clarizen]</span><span class="sxs-lookup"><span data-stu-id="9cbe9-154">In the **Identifier** box, type the value as: **Clarizen**</span></span>

    <span data-ttu-id="9cbe9-155">b.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-155">b.</span></span> <span data-ttu-id="9cbe9-156">在 [回覆 URL] 方塊中，使用下列模式輸入 URL：**https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="9cbe9-156">In the **Reply URL** box, type a URL by using the following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cbe9-157">這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-157">These are not the real values.</span></span> <span data-ttu-id="9cbe9-158">您必須使用實際的識別碼和回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-158">You have to use the actual identifier and reply URL.</span></span> <span data-ttu-id="9cbe9-159">在此建議您使用唯一的字串值做為識別碼。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-159">Here we suggest that you use the unique value of a string as the identifier.</span></span> <span data-ttu-id="9cbe9-160">若要取得實際的值，請連絡 [Clarizen 支援小組](https://success.clarizen.com/hc/en-us/requests/new)。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-160">To get the actual values, contact the [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="9cbe9-161">在 [SAML 簽署憑證] 區段中，按一下 [建立新憑證]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-161">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![按一下 [建立新的憑證]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="9cbe9-163">在 [建立新的憑證] 對話方塊中，按一下行事曆圖示並選取到期日。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-163">In the **Create New Certificate** dialog box, click the calendar icon and select an expiry date.</span></span> <span data-ttu-id="9cbe9-164">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-164">Then click **Save**.</span></span>

    ![選取並儲存到期日](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="9cbe9-166">在 [SAML 簽署憑證] 區段上，選取 [啟用新憑證]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-166">In the **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![選取核取方塊以啟用新憑證](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="9cbe9-168">在 [變換憑證] 對話方塊中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-168">In the **Rollover certificate** dialog box, click **OK**.</span></span>

    ![按一下 [確定] 確認您想要啟用憑證](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9cbe9-170">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-170">In the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![按一下 [憑證 (Base64)] 以開始下載](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="9cbe9-172">在 [Clarizen 組態] 區段上，按一下 [設定 Clarizen] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-172">In the **Clarizen Configuration** section, click **Configure Clarizen** to open the **Configure sign-on** window.</span></span>

    ![按一下 [設定 Clarizen]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![[登入設定] 視窗，包括檔案和 URL](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="9cbe9-175">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Clarizen 公司網站。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-175">In a different web browser window, sign in to your Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="9cbe9-176">按一下您的使用者名稱，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="9cbe9-177">![按一下您的使用者名稱底下的 [設定]](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "設定")</span><span class="sxs-lookup"><span data-stu-id="9cbe9-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="9cbe9-178">按一下 [全域設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-178">Click the **Global Settings** tab.</span></span> <span data-ttu-id="9cbe9-179">然後，在 [同盟驗證] 旁邊，按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-179">Then, next to **Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="9cbe9-180">![[全域設定] 索引標籤](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "全域設定")</span><span class="sxs-lookup"><span data-stu-id="9cbe9-180">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="9cbe9-181">在 [同盟驗證] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9cbe9-181">In the **Federated Authentication** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="9cbe9-182">![[同盟驗證] 對話方塊](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "同盟驗證")</span><span class="sxs-lookup"><span data-stu-id="9cbe9-182">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="9cbe9-183">a.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-183">a.</span></span> <span data-ttu-id="9cbe9-184">選取 [啟用同盟驗證]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-184">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="9cbe9-185">b.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-185">b.</span></span> <span data-ttu-id="9cbe9-186">按一下 [上傳]  來上傳您下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-186">Click **Upload** to upload your downloaded certificate.</span></span>

    <span data-ttu-id="9cbe9-187">c.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-187">c.</span></span> <span data-ttu-id="9cbe9-188">在 [單一登入 URL] 文字方塊中，輸入來自 Azure AD 應用程式組態視窗的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-188">In the **Sign-in URL** box, enter the value of **SAML Single Sign-On Service URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="9cbe9-189">d.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-189">d.</span></span> <span data-ttu-id="9cbe9-190">在 [單一登入 URL] 方塊中，輸入來自 Azure AD 應用程式組態視窗的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-190">In the **Sign-out URL** box, enter the value of **Sign-Out URL** from the Azure AD application configuration window.</span></span>

    <span data-ttu-id="9cbe9-191">e.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-191">e.</span></span> <span data-ttu-id="9cbe9-192">選取 [使用 POST] 。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-192">Select **Use POST**.</span></span>

    <span data-ttu-id="9cbe9-193">f.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-193">f.</span></span> <span data-ttu-id="9cbe9-194">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-194">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9cbe9-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9cbe9-195">Create an Azure AD test user</span></span>
<span data-ttu-id="9cbe9-196">在 Azure 入口網站中，建立名稱為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-196">In the Azure portal, create a test user called Britta Simon.</span></span>

![Azure AD 測試使用者的名稱和電子郵件地址][100]

1. <span data-ttu-id="9cbe9-198">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-198">In the Azure portal, in the left pane, click the **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 圖示](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9cbe9-200">按一下 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-200">Click **Users and groups**, and then click **All users** to display the list of users.</span></span>

    ![按一下 [使用者和群組] 與 [所有使用者]](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9cbe9-202">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-202">At the top of the dialog box, click **Add** to open the **User** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9cbe9-204">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9cbe9-204">In the **User** dialog box, perform the following steps:</span></span>

    ![在 [使用者] 對話方塊中填入名稱、電子郵件地址和密碼](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9cbe9-206">a.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-206">a.</span></span> <span data-ttu-id="9cbe9-207">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-207">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cbe9-208">b.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-208">b.</span></span> <span data-ttu-id="9cbe9-209">在 [使用者名稱] 方塊中，輸入 Britta Simon 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-209">In the **User name** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="9cbe9-210">c.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-210">c.</span></span> <span data-ttu-id="9cbe9-211">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-211">Select **Show Password** and write down the value of **Password**.</span></span>

    <span data-ttu-id="9cbe9-212">d.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-212">d.</span></span> <span data-ttu-id="9cbe9-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-213">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="9cbe9-214">建立 Clarizen 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9cbe9-214">Create a Clarizen test user</span></span>
<span data-ttu-id="9cbe9-215">若要讓 Azure AD 使用者登入 Clarizen，您必須佈建使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-215">To enable Azure AD users to sign in to Clarizen, you must provision user accounts.</span></span> <span data-ttu-id="9cbe9-216">Clarizen 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-216">In the case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="9cbe9-217">以系統管理員身分登入您的 Clarizen 公司網站。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-217">Sign in to your Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="9cbe9-218">按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-218">Click **People**.</span></span>

    <span data-ttu-id="9cbe9-219">![按一下 [人員]](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "人員")</span><span class="sxs-lookup"><span data-stu-id="9cbe9-219">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="9cbe9-220">按一下 [邀請使用者] 。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-220">Click **Invite User**.</span></span>

    <span data-ttu-id="9cbe9-221">![[邀請使用者] 按鈕](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "邀請使用者")</span><span class="sxs-lookup"><span data-stu-id="9cbe9-221">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="9cbe9-222">在 [邀請人員] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9cbe9-222">In the **Invite People** dialog box, perform the following steps:</span></span>

    <span data-ttu-id="9cbe9-223">![[邀請人員] 對話方塊](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="9cbe9-223">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="9cbe9-224">a.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-224">a.</span></span> <span data-ttu-id="9cbe9-225">在 [電子郵件] 方塊中，輸入 Britta Simon 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-225">In the **Email** box, type the email address of the Britta Simon account.</span></span>

    <span data-ttu-id="9cbe9-226">b.</span><span class="sxs-lookup"><span data-stu-id="9cbe9-226">b.</span></span> <span data-ttu-id="9cbe9-227">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-227">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9cbe9-228">Azure Active Directory 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-228">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9cbe9-229">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9cbe9-229">Assign the Azure AD test user</span></span>
<span data-ttu-id="9cbe9-230">您要把 Clarizen 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-230">Enable Britta Simon to use Azure single sign-on by granting her access to Clarizen.</span></span>

![已指派測試使用者][200]

1. <span data-ttu-id="9cbe9-232">在 Azure 入口網站中，開啟應用程式檢視，瀏覽至目錄檢視，按一下 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-232">In the Azure portal, open the applications view, browse to the directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![按一下 [企業應用程式] 和 [所有應用程式]][201]

2. <span data-ttu-id="9cbe9-234">在應用程式清單中，選取 [Clarizen]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-234">In the applications list, select **Clarizen**.</span></span>

    ![在清單中選取 Clarizen](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="9cbe9-236">在左窗格中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-236">In the left pane, click **Users and groups**.</span></span>

    ![按一下 [使用者和群組]][202]

4. <span data-ttu-id="9cbe9-238">按一下 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-238">Click the **Add** button.</span></span> <span data-ttu-id="9cbe9-239">然後，在 [新增指派] 對話方塊中，選取 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-239">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![[新增] 按鈕和 [新增指派] 對話方塊][203]

5. <span data-ttu-id="9cbe9-241">在 [使用者和群組] 對話方塊中，在使用者清單中選取 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-241">In the **Users and groups** dialog box, select **Britta Simon** in the list of users.</span></span>

6. <span data-ttu-id="9cbe9-242">在 [使用者和群組] 對話方塊中，按一下 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-242">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="9cbe9-243">在 [新增指派] 對話方塊中，按一下 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-243">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="9cbe9-244">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9cbe9-244">Test single sign-on</span></span>
<span data-ttu-id="9cbe9-245">使用存取面板來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-245">Test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="9cbe9-246">當您在 [存取面板] 中按一下 [Clarizen] 圖格時，應該會自動登入您的 Clarizen 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cbe9-246">When you click the Clarizen tile in the Access Panel, you should be automatically signed in to your Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9cbe9-247">其他資源</span><span class="sxs-lookup"><span data-stu-id="9cbe9-247">Additional resources</span></span>

* [<span data-ttu-id="9cbe9-248">如何整合 SaaS 應用程式與 Azure Active Directory 的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="9cbe9-248">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cbe9-249">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9cbe9-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
