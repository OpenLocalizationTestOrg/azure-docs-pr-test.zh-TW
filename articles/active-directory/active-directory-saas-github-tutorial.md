---
title: "教學課程：Azure Active Directory 與 GitHub 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 GitHub 之間的單一登入。"
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
ms.openlocfilehash: 9dc12bc2e313bcb2000724d035156c5054d14e1c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="082d0-103">教學課程：Azure Active Directory 與 GitHub 整合</span><span class="sxs-lookup"><span data-stu-id="082d0-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="082d0-104">在本教學課程中，您將了解如何整合 GitHub 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="082d0-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="082d0-105">GitHub 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="082d0-105">Integrating GitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="082d0-106">您可以在 Azure AD 中控制可存取 GitHub 的人員</span><span class="sxs-lookup"><span data-stu-id="082d0-106">You can control in Azure AD who has access to GitHub</span></span>
- <span data-ttu-id="082d0-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 GitHub (單一登入)</span><span class="sxs-lookup"><span data-stu-id="082d0-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="082d0-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="082d0-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="082d0-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="082d0-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="082d0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="082d0-110">Prerequisites</span></span>

<span data-ttu-id="082d0-111">若要設定 Azure AD 與 GitHub 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="082d0-111">To configure Azure AD integration with GitHub, you need the following items:</span></span>

- <span data-ttu-id="082d0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="082d0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="082d0-113">已啟用 GitHub 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="082d0-113">A GitHub single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="082d0-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="082d0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="082d0-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="082d0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="082d0-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="082d0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="082d0-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="082d0-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="082d0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="082d0-118">Scenario description</span></span>
<span data-ttu-id="082d0-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="082d0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="082d0-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="082d0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="082d0-121">從資源庫新增 GitHub</span><span class="sxs-lookup"><span data-stu-id="082d0-121">Adding GitHub from the gallery</span></span>
2. <span data-ttu-id="082d0-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="082d0-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-github-from-the-gallery"></a><span data-ttu-id="082d0-123">從資源庫新增 GitHub</span><span class="sxs-lookup"><span data-stu-id="082d0-123">Adding GitHub from the gallery</span></span>
<span data-ttu-id="082d0-124">若要設定將 GitHub 整合到 Azure AD 中，您需要從資源庫將 GitHub 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="082d0-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="082d0-125">**若要從資源庫新增 GitHub，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="082d0-125">**To add GitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="082d0-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="082d0-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="082d0-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="082d0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="082d0-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="082d0-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="082d0-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="082d0-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="082d0-133">在搜尋方塊中，輸入 **GitHub.com**。</span><span class="sxs-lookup"><span data-stu-id="082d0-133">In the search box, type **GitHub.com**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. <span data-ttu-id="082d0-135">在結果窗格中，選取 [GitHub]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="082d0-135">In the results panel, select **GitHub**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="082d0-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="082d0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="082d0-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 GitHub 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="082d0-138">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="082d0-139">若要讓單一登入運作，Azure AD 必須知道 GitHub 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="082d0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span></span> <span data-ttu-id="082d0-140">換句話說，必須建立 Azure AD 使用者和 GitHub 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="082d0-140">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span></span>

<span data-ttu-id="082d0-141">建立此連結關聯性的方法，就是指派 Azure AD 中**使用者名稱**的值做為 GitHub 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="082d0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in GitHub.</span></span>

<span data-ttu-id="082d0-142">若要設定及測試與 GitHub 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="082d0-142">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="082d0-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="082d0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="082d0-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="082d0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="082d0-145">**[建立 GitHub 測試使用者](#creating-a-GitHub-test-user)** - 讓 GitHub 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="082d0-145">**[Creating a GitHub test user](#creating-a-GitHub-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="082d0-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="082d0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="082d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="082d0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="082d0-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="082d0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="082d0-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 GitHub 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="082d0-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="082d0-150">**若要設定與 GitHub 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="082d0-150">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="082d0-151">在 Azure 管理入口網站的 [GitHub] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="082d0-151">In the Azure Management portal, on the **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="082d0-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="082d0-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. <span data-ttu-id="082d0-155">在 [GitHub 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="082d0-155">On the **GitHub Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    <span data-ttu-id="082d0-157">a.</span><span class="sxs-lookup"><span data-stu-id="082d0-157">a.</span></span> <span data-ttu-id="082d0-158">在 [登入 URL] 文字方塊中，輸入下列值：`https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="082d0-158">In the **Sign-on URL** textbox, type the value as: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="082d0-159">b.</span><span class="sxs-lookup"><span data-stu-id="082d0-159">b.</span></span> <span data-ttu-id="082d0-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="082d0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="082d0-161">請注意這些不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="082d0-161">Please note that these are not the real values.</span></span> <span data-ttu-id="082d0-162">您必須使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="082d0-162">You have to update these values with the actual Sing-on URL and Identifier.</span></span> <span data-ttu-id="082d0-163">在此建議您在 [識別碼] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="082d0-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="082d0-164">移至 [GitHub 管理] 區段來擷取這些值。</span><span class="sxs-lookup"><span data-stu-id="082d0-164">Go to GitHub Admin section to retrieve these values.</span></span> 

4. <span data-ttu-id="082d0-165">在 [使用者屬性] 區段中，選取 [user.mail] 做為 [使用者識別碼]。</span><span class="sxs-lookup"><span data-stu-id="082d0-165">On the **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. <span data-ttu-id="082d0-167">在 [SAML 簽署憑證] 區段中，按一下 [建立新憑證]。</span><span class="sxs-lookup"><span data-stu-id="082d0-167">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. <span data-ttu-id="082d0-169">在 [建立新憑證] 對話方塊中，按一下行事曆圖示並選取 [到期日]。</span><span class="sxs-lookup"><span data-stu-id="082d0-169">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="082d0-170">然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="082d0-170">Then click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="082d0-172">在 [SAML 簽署憑證] 區段中，選取 [啟用新憑證] 並按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="082d0-172">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. <span data-ttu-id="082d0-174">在 [變換憑證] 快顯視窗上，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="082d0-174">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="082d0-176">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="082d0-176">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. <span data-ttu-id="082d0-178">在 [GitHub 組態] 區段上，按一下 [設定 GitHub] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="082d0-178">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. <span data-ttu-id="082d0-181">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 GitHub 組織網站。</span><span class="sxs-lookup"><span data-stu-id="082d0-181">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

12. <span data-ttu-id="082d0-182">瀏覽至 [設定]，然後按一下 [安全性]</span><span class="sxs-lookup"><span data-stu-id="082d0-182">Navigate to **Settings** and click **Security**</span></span>

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. <span data-ttu-id="082d0-184">勾選 [啟用 SAML 驗證]方塊，以顯示單一登入設定欄位。</span><span class="sxs-lookup"><span data-stu-id="082d0-184">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span></span> <span data-ttu-id="082d0-185">然後，使用單一登入 URL 值來更新 Azure AD 組態上的單一登入 URL。</span><span class="sxs-lookup"><span data-stu-id="082d0-185">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span></span>

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. <span data-ttu-id="082d0-187">設定下列欄位：</span><span class="sxs-lookup"><span data-stu-id="082d0-187">Configure the following fields:</span></span>

    <span data-ttu-id="082d0-188">a.</span><span class="sxs-lookup"><span data-stu-id="082d0-188">a.</span></span> <span data-ttu-id="082d0-189">**登入 URL**：從 Azure AD 的 [設定 GitHub] 區段中，輸入 [SAML 單一登入服務 URL]</span><span class="sxs-lookup"><span data-stu-id="082d0-189">**Sign on URL**: Enter **SAML Single sign-on Service URL** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="082d0-190">b.</span><span class="sxs-lookup"><span data-stu-id="082d0-190">b.</span></span> <span data-ttu-id="082d0-191">**簽發者**︰從 Azure AD 的 [設定 GitHub] 區段中，輸入 [SAML 實體識別碼]</span><span class="sxs-lookup"><span data-stu-id="082d0-191">**Issuer**: Enter **SAML Entity ID** from the **Configure GitHub** section on Azure AD</span></span>

    <span data-ttu-id="082d0-192">c.</span><span class="sxs-lookup"><span data-stu-id="082d0-192">c.</span></span> <span data-ttu-id="082d0-193">**公開憑證**：在記事本中開啟已從 Azure AD 下載的憑證並複製內容，包括 "BEGIN CERTIFICATE" 和 "END CERTIFICATE"</span><span class="sxs-lookup"><span data-stu-id="082d0-193">**Public Certificate**: Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE"</span></span>

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. <span data-ttu-id="082d0-195">按一下 [測試 SAML 組態]，確認 SSO 期間沒有驗證失敗或錯誤。</span><span class="sxs-lookup"><span data-stu-id="082d0-195">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span></span>

    ![設定](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. <span data-ttu-id="082d0-197">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="082d0-197">Click **Save**</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="082d0-198">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="082d0-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="082d0-199">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="082d0-199">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="082d0-201">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="082d0-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="082d0-202">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="082d0-202">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="082d0-204">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="082d0-204">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="082d0-206">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="082d0-206">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="082d0-208">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="082d0-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="082d0-210">a.</span><span class="sxs-lookup"><span data-stu-id="082d0-210">a.</span></span> <span data-ttu-id="082d0-211">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="082d0-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="082d0-212">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="082d0-212">b.</span></span> <span data-ttu-id="082d0-213">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="082d0-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="082d0-214">c.</span><span class="sxs-lookup"><span data-stu-id="082d0-214">c.</span></span> <span data-ttu-id="082d0-215">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="082d0-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="082d0-216">d.</span><span class="sxs-lookup"><span data-stu-id="082d0-216">d.</span></span> <span data-ttu-id="082d0-217">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="082d0-217">Click **Create**.</span></span> 


### <a name="creating-a-github-test-user"></a><span data-ttu-id="082d0-218">建立 GitHub 測試使用者</span><span class="sxs-lookup"><span data-stu-id="082d0-218">Creating a GitHub test user</span></span>

<span data-ttu-id="082d0-219">若要讓 Azure AD 使用者能夠登入 GitHub，則必須將他們佈建到 GitHub。</span><span class="sxs-lookup"><span data-stu-id="082d0-219">In order to enable Azure AD users to log into GitHub, they must be provisioned into GitHub.</span></span>  
<span data-ttu-id="082d0-220">GitHub 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="082d0-220">In the case of GitHub, provisioning is a manual task.</span></span>

<span data-ttu-id="082d0-221">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="082d0-221">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="082d0-222">以系統管理員身分登入您的 GitHub 公司網站。</span><span class="sxs-lookup"><span data-stu-id="082d0-222">Log in to your GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="082d0-223">按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="082d0-223">Click **People**.</span></span>

    <span data-ttu-id="082d0-224">![人員](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "人員")</span><span class="sxs-lookup"><span data-stu-id="082d0-224">![People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="082d0-225">按一下 [邀請成員]。</span><span class="sxs-lookup"><span data-stu-id="082d0-225">Click **Invite member**.</span></span>

    <span data-ttu-id="082d0-226">![邀請使用者](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "邀請使用者")</span><span class="sxs-lookup"><span data-stu-id="082d0-226">![Invite Users](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="082d0-227">在 [邀請成員] 對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="082d0-227">On the **Invite member** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="082d0-228">a.</span><span class="sxs-lookup"><span data-stu-id="082d0-228">a.</span></span> <span data-ttu-id="082d0-229">在 [電子郵件] 文字方塊中，輸入 Britta Simon 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="082d0-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="082d0-230">![邀請人員](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="082d0-230">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>
    
    <span data-ttu-id="082d0-231">b.</span><span class="sxs-lookup"><span data-stu-id="082d0-231">b.</span></span> <span data-ttu-id="082d0-232">按一下 [傳送邀請]。</span><span class="sxs-lookup"><span data-stu-id="082d0-232">Click **Send Invitation**.</span></span>

    <span data-ttu-id="082d0-233">![邀請人員](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "邀請人員")</span><span class="sxs-lookup"><span data-stu-id="082d0-233">![Invite People](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="082d0-234">Azure Active Directory 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="082d0-234">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="082d0-235">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="082d0-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="082d0-236">在本節中，您會將 GitHub 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="082d0-236">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to GitHub.</span></span>

![指派使用者][200] 

<span data-ttu-id="082d0-238">**若要將 Britta Simon 指派給 GitHub，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="082d0-238">**To assign Britta Simon to GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="082d0-239">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="082d0-239">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="082d0-241">在應用程式清單中，選取 [GitHub.com]。</span><span class="sxs-lookup"><span data-stu-id="082d0-241">In the applications list, select **GitHub.com**.</span></span>

    ![設定單一登入](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. <span data-ttu-id="082d0-243">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="082d0-243">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="082d0-245">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="082d0-245">Click **Add** button.</span></span> <span data-ttu-id="082d0-246">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="082d0-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="082d0-248">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="082d0-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="082d0-249">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="082d0-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="082d0-250">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="082d0-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="082d0-251">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="082d0-251">Testing single sign-on</span></span>

<span data-ttu-id="082d0-252">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="082d0-252">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="082d0-253">當您在存取面板中按一下 [GitHub] 圖格時，應該會登入您的 GitHub 應用程式。</span><span class="sxs-lookup"><span data-stu-id="082d0-253">When you click the GitHub tile in the Access Panel, you should get signed-on to your GitHub application.</span></span> <span data-ttu-id="082d0-254">您將會以組織帳戶登入，但隨後需要以您的個人帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="082d0-254">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="082d0-255">其他資源</span><span class="sxs-lookup"><span data-stu-id="082d0-255">Additional resources</span></span>

* [<span data-ttu-id="082d0-256">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="082d0-256">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="082d0-257">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="082d0-257">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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
