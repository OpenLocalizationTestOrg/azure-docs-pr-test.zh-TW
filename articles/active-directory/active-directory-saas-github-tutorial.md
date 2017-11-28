---
title: "教學課程：Azure Active Directory 與 GitHub 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 GitHub 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="13637-103">教學課程：Azure Active Directory 與 GitHub 整合</span><span class="sxs-lookup"><span data-stu-id="13637-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="13637-104">在此教學課程中，您學會如何 toointegrate GitHub 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="13637-104">In this tutorial, you learn how toointegrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13637-105">與 Azure AD 整合 GitHub 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="13637-105">Integrating GitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="13637-106">您可以控制存取 tooGitHub Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="13637-106">You can control in Azure AD who has access tooGitHub</span></span>
- <span data-ttu-id="13637-107">您可以啟用您的使用者 tooautomatically get 登入 tooGitHub （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="13637-107">You can enable your users tooautomatically get signed-on tooGitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13637-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="13637-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="13637-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="13637-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13637-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="13637-110">Prerequisites</span></span>

<span data-ttu-id="13637-111">tooconfigure 與 GitHub 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="13637-111">tooconfigure Azure AD integration with GitHub, you need hello following items:</span></span>

- <span data-ttu-id="13637-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="13637-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13637-113">已啟用 GitHub 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="13637-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="13637-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="13637-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="13637-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="13637-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13637-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="13637-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="13637-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="13637-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="13637-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="13637-118">Scenario description</span></span>
<span data-ttu-id="13637-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13637-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13637-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="13637-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13637-121">從 hello 圖庫加入 GitHub</span><span class="sxs-lookup"><span data-stu-id="13637-121">Adding GitHub from hello gallery</span></span>
2. <span data-ttu-id="13637-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="13637-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-hello-gallery"></a><span data-ttu-id="13637-123">從 hello 圖庫加入 GitHub</span><span class="sxs-lookup"><span data-stu-id="13637-123">Adding GitHub from hello gallery</span></span>
<span data-ttu-id="13637-124">tooconfigure hello 整合 GitHub 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd GitHub。</span><span class="sxs-lookup"><span data-stu-id="13637-124">tooconfigure hello integration of GitHub into Azure AD, you need tooadd GitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="13637-125">**tooadd GitHub hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="13637-125">**tooadd GitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="13637-126">在 [hello ** [Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="13637-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13637-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="13637-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="13637-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="13637-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="13637-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="13637-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="13637-133">在 [hello] 搜尋方塊中，輸入**GitHub.com**。</span><span class="sxs-lookup"><span data-stu-id="13637-133">In hello search box, type **GitHub.com**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="13637-135">在 [hello [結果] 窗格中，選取 [ **GitHub**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="13637-135">In hello results panel, select **GitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13637-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="13637-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13637-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 GitHub 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13637-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="13637-139">單一登入 toowork，Azure AD 需要 tooknow hello 對應項目在 GitHub 中的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="13637-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="13637-140">換句話說，Azure AD 使用者與 GitHub 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="13637-140">In other words, a link relationship between an Azure AD user and hello related user in GitHub needs toobe established.</span></span>

<span data-ttu-id="13637-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** GitHub 中。</span><span class="sxs-lookup"><span data-stu-id="13637-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in GitHub.</span></span>

<span data-ttu-id="13637-142">tooconfigure 及測試 Azure AD 單一登入與 GitHub，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="13637-142">tooconfigure and test Azure AD single sign-on with GitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="13637-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="13637-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="13637-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="13637-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13637-145">**[建立 GitHub 測試使用者](#creating-a-GitHub-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 GitHub 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="13637-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - toohave a counterpart of Britta Simon in GitHub that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="13637-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13637-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13637-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="13637-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13637-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="13637-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13637-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入 GitHub 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="13637-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="13637-150">**tooconfigure Azure AD 單一登入與 GitHub，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="13637-150">**tooconfigure Azure AD single sign-on with GitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="13637-151">在 hello Azure 管理入口網站上 hello **GitHub**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="13637-151">In hello Azure Management portal, on hello **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="13637-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13637-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="13637-155">在 [hello **GitHub 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="13637-155">On hello **GitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="13637-157">a.</span><span class="sxs-lookup"><span data-stu-id="13637-157">a.</span></span> <span data-ttu-id="13637-158">在 [hello**登入 URL**文字方塊中，做為型別 hello 值：`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="13637-158">In hello **Sign-on URL** textbox, type hello value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="13637-159">b.</span><span class="sxs-lookup"><span data-stu-id="13637-159">b.</span></span> <span data-ttu-id="13637-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="13637-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="13637-161">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="13637-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="13637-162">您有 tooupdate hello 實際登入 URL 和識別碼具有這些值。</span><span class="sxs-lookup"><span data-stu-id="13637-162">You have tooupdate these values with hello actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="13637-163">這裡我們建議您 toouse hello 唯一字串的值在 hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="13637-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="13637-164">移 tooGitHub 管理 > 一節 tooretrieve 這些值。</span><span class="sxs-lookup"><span data-stu-id="13637-164">Go tooGitHub Admin section tooretrieve these values.</span></span> 

4. <span data-ttu-id="13637-165">在 [hello**使用者屬性**區段中，選取**使用者識別碼**user.mail 為。</span><span class="sxs-lookup"><span data-stu-id="13637-165">On hello **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="13637-167">在 [hello **SAML 簽章憑證**區段中，按一下**建立新憑證**。</span><span class="sxs-lookup"><span data-stu-id="13637-167">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="13637-169">在 [hello**建立新的憑證**] 對話方塊中，按一下 hello 日曆圖示，然後選取**到期日**。</span><span class="sxs-lookup"><span data-stu-id="13637-169">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="13637-170">然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13637-170">Then click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="13637-172">在 hello **SAML 簽章憑證**區段中，選取**啟用新的憑證**按一下**儲存**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13637-172">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="13637-174">Hello 快顯視窗上**變換憑證**視窗中，按一下 [**確定**。</span><span class="sxs-lookup"><span data-stu-id="13637-174">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="13637-176">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="13637-176">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="13637-178">在 [hello **GitHub 組態**區段中，按一下**設定 GitHub** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="13637-178">On hello **GitHub Configuration** section, click **Configure GitHub** tooopen **Configure sign-on** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="13637-181">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 GitHub 組織網站。</span><span class="sxs-lookup"><span data-stu-id="13637-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="13637-182">瀏覽過**設定**按一下**安全性**</span><span class="sxs-lookup"><span data-stu-id="13637-182">Navigate too**Settings** and click **Security**</span></span>

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="13637-184">檢查 hello**啟用 SAML 驗證**] 方塊中，顯示 hello 單一登入設定欄位。</span><span class="sxs-lookup"><span data-stu-id="13637-184">Check hello **Enable SAML authentication** box, revealing hello Single Sign-on configuration fields.</span></span> <span data-ttu-id="13637-185">然後，使用 Azure AD 組態 hello 單一登入 URL 值 tooupdate hello 單一登入的 URL。</span><span class="sxs-lookup"><span data-stu-id="13637-185">Then, use hello single sign-on URL value tooupdate hello Single sign-on URL on Azure AD configuration.</span></span>

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="13637-187">設定下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="13637-187">Configure hello following fields:</span></span>

    <span data-ttu-id="13637-188">a.</span><span class="sxs-lookup"><span data-stu-id="13637-188">a.</span></span> <span data-ttu-id="13637-189">**登入 URL**： 輸入**SAML 單一登入服務 URL**從 hello**設定 GitHub**上 Azure AD 區段</span><span class="sxs-lookup"><span data-stu-id="13637-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="13637-190">b.</span><span class="sxs-lookup"><span data-stu-id="13637-190">b.</span></span> <span data-ttu-id="13637-191">**簽發者**： 輸入**SAML 實體識別碼**從 hello**設定 GitHub**上 Azure AD 區段</span><span class="sxs-lookup"><span data-stu-id="13637-191">**Issuer**: Enter **SAML Entity ID** from hello **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="13637-192">c.</span><span class="sxs-lookup"><span data-stu-id="13637-192">c.</span></span> <span data-ttu-id="13637-193">**公開憑證**： 開啟 hello 從 Azure AD 中包括 「 開始憑證 」 和 「 結束憑證 」 為 「 記事本 」 並複製 hello 內容下載憑證</span><span class="sxs-lookup"><span data-stu-id="13637-193">**Public Certificate**: Open hello downloaded certificate from Azure AD in a notepad and copy hello content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="13637-195">按一下**測試 SAML 設定**tooconfirm 所沒有的驗證失敗或 SSO 期間發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="13637-195">Click on **Test SAML configuration** tooconfirm that no validation failures or errors during SSO.</span></span>

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="13637-197">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="13637-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13637-198">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="13637-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="13637-199">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="13637-199">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="13637-201">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="13637-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="13637-202">在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="13637-202">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13637-204">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="13637-204">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13637-206">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="13637-206">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13637-208">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="13637-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13637-210">a.</span><span class="sxs-lookup"><span data-stu-id="13637-210">a.</span></span> <span data-ttu-id="13637-211">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="13637-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13637-212">b.</span><span class="sxs-lookup"><span data-stu-id="13637-212">b.</span></span> <span data-ttu-id="13637-213">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="13637-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="13637-214">c.</span><span class="sxs-lookup"><span data-stu-id="13637-214">c.</span></span> <span data-ttu-id="13637-215">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="13637-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="13637-216">d.</span><span class="sxs-lookup"><span data-stu-id="13637-216">d.</span></span> <span data-ttu-id="13637-217">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="13637-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="13637-218">建立 GitHub 測試使用者</span><span class="sxs-lookup"><span data-stu-id="13637-218">Creating a GitHub test user</span></span>

<span data-ttu-id="13637-219">在訂單 tooenable Azure AD 使用者 toolog 到 GitHub，您必須是佈建到 GitHub。</span><span class="sxs-lookup"><span data-stu-id="13637-219">In order tooenable Azure AD users toolog into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="13637-220">在 GitHub 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="13637-220">In hello case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="13637-221">**tooprovision 使用者帳戶，執行下列步驟 hello:**</span><span class="sxs-lookup"><span data-stu-id="13637-221">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="13637-222">登入 tooyour GitHub 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="13637-222">Log in tooyour GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="13637-223">按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="13637-223">Click **People**.</span></span>

    <span data-ttu-id="13637-224">![人員](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "人員")</span><span class="sxs-lookup"><span data-stu-id="13637-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="13637-225">按一下 [邀請成員]。</span><span class="sxs-lookup"><span data-stu-id="13637-225">Click **Invite member**.</span></span>

    <span data-ttu-id="13637-226">![邀請使用者](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "邀請使用者")</span><span class="sxs-lookup"><span data-stu-id="13637-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="13637-227">在 [hello**邀請成員**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="13637-227">On hello **Invite member** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="13637-228">a.</span><span class="sxs-lookup"><span data-stu-id="13637-228">a.</span></span> <span data-ttu-id="13637-229">在 [hello**電子郵件**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="13637-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="13637-230">![邀請人員](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="13637-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="13637-231">b.</span><span class="sxs-lookup"><span data-stu-id="13637-231">b.</span></span> <span data-ttu-id="13637-232">按一下 [傳送邀請]。</span><span class="sxs-lookup"><span data-stu-id="13637-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="13637-233">![邀請人員](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="13637-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="13637-234">hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="13637-234">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="13637-235">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="13637-235">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="13637-236">在本節中，您可以授與他們存取 tooGitHub 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="13637-236">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooGitHub.</span></span>

![指派使用者][200] 

<span data-ttu-id="13637-238">**tooassign 許 Simon tooGitHub，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="13637-238">**tooassign Britta Simon tooGitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="13637-239">在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="13637-239">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="13637-241">在 [hello] 應用程式清單中，選取**GitHub.com**。</span><span class="sxs-lookup"><span data-stu-id="13637-241">In hello applications list, select **GitHub.com**.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="13637-243">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="13637-243">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="13637-245">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13637-245">Click **Add** button.</span></span> <span data-ttu-id="13637-246">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="13637-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="13637-248">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="13637-248">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="13637-249">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13637-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13637-250">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="13637-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="13637-251">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="13637-251">Testing single sign-on</span></span>

<span data-ttu-id="13637-252">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="13637-252">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="13637-253">當您按一下 hello GitHub 磚 hello 存取面板中的時，您應該取得已登入的 tooyour GitHub 應用程式。</span><span class="sxs-lookup"><span data-stu-id="13637-253">When you click hello GitHub tile in hello Access Panel, you should get signed-on tooyour GitHub application.</span></span> <span data-ttu-id="13637-254">您將會以登入組織帳戶但需要 toolog 使用您個人的帳戶。</span><span class="sxs-lookup"><span data-stu-id="13637-254">You'll be logging in as an Organization account but then need toolog in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="13637-255">其他資源</span><span class="sxs-lookup"><span data-stu-id="13637-255">Additional resources</span></span>

* [<span data-ttu-id="13637-256">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13637-256">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13637-257">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="13637-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
