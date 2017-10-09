---
title: "教學課程：Azure Active Directory 與 Kantega SSO for JIRA 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 JIRA 的 Kantega SSO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 67894cc55ef91d0991c62e0e4f1be712723cb474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="1915b-103">教學課程：Azure Active Directory 與 Kantega SSO for JIRA 整合</span><span class="sxs-lookup"><span data-stu-id="1915b-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="1915b-104">在此教學課程中，您學會如何 toointegrate JIRA 與 Azure Active Directory (Azure AD) 的 Kantega SSO。</span><span class="sxs-lookup"><span data-stu-id="1915b-104">In this tutorial, you learn how toointegrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1915b-105">與 Azure AD 整合的 JIRA Kantega SSO 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1915b-105">Integrating Kantega SSO for JIRA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1915b-106">您可以控制存取 tooKantega SSO JIRA 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="1915b-106">You can control in Azure AD who has access tooKantega SSO for JIRA</span></span>
- <span data-ttu-id="1915b-107">您可以啟用您使用者 tooautomatically get 登入 tooKantega SSO （單一登入） JIRA 使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="1915b-107">You can enable your users tooautomatically get signed-on tooKantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1915b-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1915b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1915b-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1915b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1915b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1915b-110">Prerequisites</span></span>

<span data-ttu-id="1915b-111">tooconfigure JIRA 的 Kantega SSO 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1915b-111">tooconfigure Azure AD integration with Kantega SSO for JIRA, you need hello following items:</span></span>

- <span data-ttu-id="1915b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1915b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1915b-113">啟用 Kantega SSO for JIRA 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1915b-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1915b-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1915b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1915b-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1915b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1915b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1915b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1915b-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1915b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1915b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1915b-118">Scenario description</span></span>
<span data-ttu-id="1915b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1915b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1915b-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1915b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1915b-121">從 hello 圖庫新增為 JIRA Kantega SSO</span><span class="sxs-lookup"><span data-stu-id="1915b-121">Adding Kantega SSO for JIRA from hello gallery</span></span>
2. <span data-ttu-id="1915b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1915b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-hello-gallery"></a><span data-ttu-id="1915b-123">從 hello 圖庫新增為 JIRA Kantega SSO</span><span class="sxs-lookup"><span data-stu-id="1915b-123">Adding Kantega SSO for JIRA from hello gallery</span></span>
<span data-ttu-id="1915b-124">tooconfigure hello 整合 JIRA 的 Kantega SSO 至 Azure AD，您需要 tooadd Kantega SSO JIRA hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1915b-124">tooconfigure hello integration of Kantega SSO for JIRA into Azure AD, you need tooadd Kantega SSO for JIRA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1915b-125">**tooadd Kantega SSO 的 JIRA hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1915b-125">**tooadd Kantega SSO for JIRA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1915b-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1915b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1915b-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1915b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1915b-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1915b-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1915b-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1915b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1915b-133">在 [hello] 搜尋方塊中，輸入**JIRA 的 Kantega SSO**。</span><span class="sxs-lookup"><span data-stu-id="1915b-133">In hello search box, type **Kantega SSO for JIRA**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. <span data-ttu-id="1915b-135">在 hello 結果 窗格中，選取  **JIRA 的 Kantega SSO**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1915b-135">In hello results panel, select **Kantega SSO for JIRA**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1915b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1915b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1915b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kantega SSO for JIRA 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1915b-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1915b-139">單一登入 toowork，Azure AD 需要 tooknow JIRA 的 Kantega SSO 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1915b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kantega SSO for JIRA is tooa user in Azure AD.</span></span> <span data-ttu-id="1915b-140">換句話說，Azure AD 使用者與 hello JIRA 的 Kantega SSO 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1915b-140">In other words, a link relationship between an Azure AD user and hello related user in Kantega SSO for JIRA needs toobe established.</span></span>

<span data-ttu-id="1915b-141">JIRA 的 Kantega SSO 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1915b-141">In Kantega SSO for JIRA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1915b-142">tooconfigure 及測試 Azure AD 單一登入使用 Kantega SSO JIRA，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1915b-142">tooconfigure and test Azure AD single sign-on with Kantega SSO for JIRA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1915b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1915b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1915b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1915b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1915b-145">**[建立 JIRA 測試使用者 Kantega SSO](#creating-a-kantega-sso-for-jira-test-user)**  -toohave 許 Simon 的是連結的 toohello Azure AD 使用者表示法的 JIRA Kantega SSO 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="1915b-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - toohave a counterpart of Britta Simon in Kantega SSO for JIRA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1915b-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1915b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1915b-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1915b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1915b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1915b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1915b-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的 Kantega SSO JIRA 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1915b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="1915b-150">**Azure AD 單一登入的 tooconfigure JIRA 的 Kantega sso 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1915b-150">**tooconfigure Azure AD single sign-on with Kantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="1915b-151">在 Azure 入口網站上 hello hello **JIRA 的 Kantega SSO**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1915b-151">In hello Azure portal, on hello **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1915b-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1915b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. <span data-ttu-id="1915b-155">在**IDP**起始模式，在 hello **JIRA 網域和 Url Kantega SSO**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1915b-155">In **IDP** initiated mode, on hello **Kantega SSO for JIRA Domain and URLs** section perform hello following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="1915b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1915b-157">a.</span></span> <span data-ttu-id="1915b-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="1915b-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="1915b-159">b.</span><span class="sxs-lookup"><span data-stu-id="1915b-159">b.</span></span> <span data-ttu-id="1915b-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="1915b-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="1915b-161">在**SP**初始的模式中，核取**顯示進階的 URL 設定**並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1915b-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform hello following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="1915b-163">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="1915b-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1915b-164">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="1915b-164">These values are not real.</span></span> <span data-ttu-id="1915b-165">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="1915b-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1915b-166">Hello Jira 外掛程式，在 hello 教學課程稍後會說明設定期間，會收到這些值。</span><span class="sxs-lookup"><span data-stu-id="1915b-166">These values are received during hello configuration of Jira plugin, which is explained later in hello tutorial.</span></span>

5. <span data-ttu-id="1915b-167">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="1915b-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. <span data-ttu-id="1915b-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1915b-169">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1915b-171">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour JIRA 內部部署伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1915b-171">In a different web browser window, log in tooyour JIRA on premise server as an administrator.</span></span>

8. <span data-ttu-id="1915b-172">將滑鼠停留在齒輪，然後按一下 hello**附加元件**。</span><span class="sxs-lookup"><span data-stu-id="1915b-172">Hover on cog and click hello **Add-ons**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. <span data-ttu-id="1915b-174">在附加元件索引標籤區段下，按一下 [尋找新的附加元件]。</span><span class="sxs-lookup"><span data-stu-id="1915b-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="1915b-175">搜尋**JIRA SAML & Kerberos 的 Kantega SSO**按一下**安裝**按鈕 tooinstall hello 新 SAML 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1915b-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. <span data-ttu-id="1915b-177">啟動 hello 外掛程式安裝。</span><span class="sxs-lookup"><span data-stu-id="1915b-177">hello plugin installation starts.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. <span data-ttu-id="1915b-179">一旦 hello 安裝已完成。</span><span class="sxs-lookup"><span data-stu-id="1915b-179">Once hello installation is complete.</span></span> <span data-ttu-id="1915b-180">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="1915b-180">Click **Close**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. <span data-ttu-id="1915b-182">按一下 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="1915b-182">Click **Manage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. <span data-ttu-id="1915b-184">[整合] 下會列出新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1915b-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="1915b-185">按一下**設定**tooconfigure hello 新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1915b-185">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. <span data-ttu-id="1915b-187">在 hello **SAML** > 一節。</span><span class="sxs-lookup"><span data-stu-id="1915b-187">In hello **SAML** section.</span></span> <span data-ttu-id="1915b-188">選取**Azure Active Directory (Azure AD)**從 hello**新增身分識別提供者**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="1915b-188">Select **Azure Active Directory (Azure AD)** from hello **Add identity provider** dropdown.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. <span data-ttu-id="1915b-190">選取 [基本] 作為訂用帳戶層級。</span><span class="sxs-lookup"><span data-stu-id="1915b-190">Select subscription level as **Basic**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. <span data-ttu-id="1915b-192">在 hello**應用程式屬性**區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1915b-192">On hello **App properties** section, perform following steps:</span></span> 

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="1915b-194">a.</span><span class="sxs-lookup"><span data-stu-id="1915b-194">a.</span></span> <span data-ttu-id="1915b-195">複製 hello**應用程式識別碼 URI**值，並使用它作為**識別碼、 回覆 URL 和登入 URL**上 hello **JIRA 網域和 Url Kantega SSO** Azure 入口網站中的區段。</span><span class="sxs-lookup"><span data-stu-id="1915b-195">Copy hello **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on hello **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="1915b-196">b.</span><span class="sxs-lookup"><span data-stu-id="1915b-196">b.</span></span> <span data-ttu-id="1915b-197">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1915b-197">Click **Next**.</span></span>

17. <span data-ttu-id="1915b-198">在 hello**中繼資料匯入**區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1915b-198">On hello **Metadata import** section, perform following steps:</span></span> 

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="1915b-200">a.</span><span class="sxs-lookup"><span data-stu-id="1915b-200">a.</span></span> <span data-ttu-id="1915b-201">選取 [我的電腦上的中繼資料檔案]，上傳您從 Azure 入口網站下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="1915b-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="1915b-202">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1915b-202">b.</span></span> <span data-ttu-id="1915b-203">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1915b-203">Click **Next**.</span></span>

18. <span data-ttu-id="1915b-204">在 hello**名稱和 SSO 位置**區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1915b-204">On hello **Name and SSO location** section, perform following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="1915b-206">a.</span><span class="sxs-lookup"><span data-stu-id="1915b-206">a.</span></span> <span data-ttu-id="1915b-207">Hello 身分識別提供者的名稱新增在**身分識別提供者名稱**文字方塊中 （例如 Azure AD）。</span><span class="sxs-lookup"><span data-stu-id="1915b-207">Add Name of hello Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="1915b-208">b.</span><span class="sxs-lookup"><span data-stu-id="1915b-208">b.</span></span> <span data-ttu-id="1915b-209">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1915b-209">Click **Next**.</span></span>

19. <span data-ttu-id="1915b-210">請確認 hello 簽章憑證，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="1915b-210">Verify hello Signing certificate and click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. <span data-ttu-id="1915b-212">在 hello **JIRA 使用者帳戶**區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1915b-212">On hello **JIRA user accounts** section, perform following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="1915b-214">a.</span><span class="sxs-lookup"><span data-stu-id="1915b-214">a.</span></span> <span data-ttu-id="1915b-215">選取**JIRA 的內部目錄中建立使用者，視**，然後輸入 hello 適當 hello 群組的使用者名稱 (可以是多個否。</span><span class="sxs-lookup"><span data-stu-id="1915b-215">Select **Create users in JIRA's internal Directory if needed** and enter hello appropriate name of hello group for users (can be multiple no.</span></span> <span data-ttu-id="1915b-216">群組，以逗號分隔)。</span><span class="sxs-lookup"><span data-stu-id="1915b-216">of groups separated by comma).</span></span>

    <span data-ttu-id="1915b-217">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1915b-217">b.</span></span> <span data-ttu-id="1915b-218">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="1915b-218">Click **Next**.</span></span>

21. <span data-ttu-id="1915b-219">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="1915b-219">Click **Finish**.</span></span>   

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. <span data-ttu-id="1915b-221">在 hello**已知的 Azure AD 網域**區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1915b-221">On hello **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="1915b-223">a.</span><span class="sxs-lookup"><span data-stu-id="1915b-223">a.</span></span> <span data-ttu-id="1915b-224">選取**已知網域**hello 的 hello 頁面的左面板中。</span><span class="sxs-lookup"><span data-stu-id="1915b-224">Select **Known domains** from hello left panel of hello page.</span></span>

    <span data-ttu-id="1915b-225">b.</span><span class="sxs-lookup"><span data-stu-id="1915b-225">b.</span></span> <span data-ttu-id="1915b-226">輸入網域名稱在 hello**已知網域**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1915b-226">Enter domain name in hello **Known domains** textbox.</span></span>

    <span data-ttu-id="1915b-227">c.</span><span class="sxs-lookup"><span data-stu-id="1915b-227">c.</span></span> <span data-ttu-id="1915b-228">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1915b-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="1915b-229">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1915b-229">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1915b-230">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1915b-230">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1915b-231">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1915b-231">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1915b-232">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1915b-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="1915b-233">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1915b-233">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1915b-235">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1915b-235">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1915b-236">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1915b-236">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1915b-238">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1915b-238">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1915b-240">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="1915b-240">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1915b-242">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1915b-242">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1915b-244">a.</span><span class="sxs-lookup"><span data-stu-id="1915b-244">a.</span></span> <span data-ttu-id="1915b-245">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1915b-245">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1915b-246">b.</span><span class="sxs-lookup"><span data-stu-id="1915b-246">b.</span></span> <span data-ttu-id="1915b-247">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="1915b-247">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1915b-248">c.</span><span class="sxs-lookup"><span data-stu-id="1915b-248">c.</span></span> <span data-ttu-id="1915b-249">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1915b-249">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1915b-250">d.</span><span class="sxs-lookup"><span data-stu-id="1915b-250">d.</span></span> <span data-ttu-id="1915b-251">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1915b-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="1915b-252">建立 Kantega SSO for JIRA 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1915b-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="1915b-253">tooenable Azure AD 使用者 toolog 中 tooJIRA，它們必須佈建到 JIRA。</span><span class="sxs-lookup"><span data-stu-id="1915b-253">tooenable Azure AD users toolog in tooJIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="1915b-254">在 Kantega SSO for JIRA 中，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="1915b-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="1915b-255">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1915b-255">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1915b-256">系統管理員身分登入 tooyour JIRA 內部部署伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1915b-256">Log in tooyour JIRA on premise server as an administrator.</span></span>

2. <span data-ttu-id="1915b-257">將滑鼠停留在齒輪，然後按一下 hello**使用者管理**。</span><span class="sxs-lookup"><span data-stu-id="1915b-257">Hover on cog and click hello **User management**.</span></span>

    ![新增員工](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. <span data-ttu-id="1915b-259">在 [使用者管理] 索引標籤區段下，按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="1915b-259">Under **User management** tab section, click **Create user**.</span></span>

    ![新增員工](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. <span data-ttu-id="1915b-261">在 hello **「 建立新的使用者 」**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1915b-261">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![新增員工](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="1915b-263">a.</span><span class="sxs-lookup"><span data-stu-id="1915b-263">a.</span></span> <span data-ttu-id="1915b-264">在 hello**電子郵件地址**文字方塊中，輸入 hello 電子郵件地址的使用者喜歡Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="1915b-264">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1915b-265">b.</span><span class="sxs-lookup"><span data-stu-id="1915b-265">b.</span></span> <span data-ttu-id="1915b-266">在 hello**全名**文字方塊中，例如許 Simon 的 hello 使用者類型完整名稱。</span><span class="sxs-lookup"><span data-stu-id="1915b-266">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="1915b-267">c.</span><span class="sxs-lookup"><span data-stu-id="1915b-267">c.</span></span> <span data-ttu-id="1915b-268">在 hello **Username**文字方塊中，型別 hello 電子郵件的使用者要Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="1915b-268">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="1915b-269">d.</span><span class="sxs-lookup"><span data-stu-id="1915b-269">d.</span></span> <span data-ttu-id="1915b-270">在 hello**密碼**文字方塊中，輸入 hello 密碼的使用者。</span><span class="sxs-lookup"><span data-stu-id="1915b-270">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="1915b-271">e.</span><span class="sxs-lookup"><span data-stu-id="1915b-271">e.</span></span> <span data-ttu-id="1915b-272">按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="1915b-272">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1915b-273">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="1915b-273">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1915b-274">在本節中，您可以授與存取 tooKantega SSO JIRA 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1915b-274">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKantega SSO for JIRA.</span></span>

![指派使用者][200] 

<span data-ttu-id="1915b-276">**tooassign 許 Simon tooKantega SSO 的 JIRA，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1915b-276">**tooassign Britta Simon tooKantega SSO for JIRA, perform hello following steps:**</span></span>

1. <span data-ttu-id="1915b-277">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1915b-277">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1915b-279">在 [hello] 應用程式清單中，選取**JIRA 的 Kantega SSO**。</span><span class="sxs-lookup"><span data-stu-id="1915b-279">In hello applications list, select **Kantega SSO for JIRA**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. <span data-ttu-id="1915b-281">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1915b-281">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1915b-283">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1915b-283">Click **Add** button.</span></span> <span data-ttu-id="1915b-284">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1915b-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1915b-286">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="1915b-286">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1915b-287">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1915b-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1915b-288">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1915b-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1915b-289">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1915b-289">Testing single sign-on</span></span>

<span data-ttu-id="1915b-290">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="1915b-290">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1915b-291">當您按一下 hello Kantega SSO JIRA 磚 hello 存取面板中時，您應該取得自動登入 tooyour Kantega SSO JIRA 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1915b-291">When you click hello Kantega SSO for JIRA tile in hello Access Panel, you should get automatically signed-on tooyour Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="1915b-292">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1915b-292">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1915b-293">其他資源</span><span class="sxs-lookup"><span data-stu-id="1915b-293">Additional resources</span></span>

* [<span data-ttu-id="1915b-294">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1915b-294">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1915b-295">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1915b-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_203.png

