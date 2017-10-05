---
title: "教學課程：Azure Active Directory 與 Kantega SSO for JIRA 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Kantega SSO for JIRA 之間的單一登入。"
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
ms.openlocfilehash: 06a1d301818f025270137f7eaa9f40e5e4503112
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a><span data-ttu-id="08879-103">教學課程：Azure Active Directory 與 Kantega SSO for JIRA 整合</span><span class="sxs-lookup"><span data-stu-id="08879-103">Tutorial: Azure Active Directory integration with Kantega SSO for JIRA</span></span>

<span data-ttu-id="08879-104">在本教學課程中，您會了解如何整合 Kantega SSO for JIRA 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="08879-104">In this tutorial, you learn how to integrate Kantega SSO for JIRA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08879-105">Kantega SSO for JIRA 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="08879-105">Integrating Kantega SSO for JIRA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="08879-106">您可以在 Azure AD 中控制可存取 Kantega SSO for JIRA 的人員</span><span class="sxs-lookup"><span data-stu-id="08879-106">You can control in Azure AD who has access to Kantega SSO for JIRA</span></span>
- <span data-ttu-id="08879-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Kantega SSO for JIRA (單一登入)</span><span class="sxs-lookup"><span data-stu-id="08879-107">You can enable your users to automatically get signed-on to Kantega SSO for JIRA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="08879-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="08879-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="08879-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="08879-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08879-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="08879-110">Prerequisites</span></span>

<span data-ttu-id="08879-111">若要設定 Azure AD 與 Kantega SSO for JIRA 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="08879-111">To configure Azure AD integration with Kantega SSO for JIRA, you need the following items:</span></span>

- <span data-ttu-id="08879-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="08879-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08879-113">啟用 Kantega SSO for JIRA 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="08879-113">A Kantega SSO for JIRA single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08879-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="08879-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08879-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="08879-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08879-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="08879-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08879-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="08879-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08879-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="08879-118">Scenario description</span></span>
<span data-ttu-id="08879-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="08879-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08879-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="08879-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08879-121">從資源庫新增 Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="08879-121">Adding Kantega SSO for JIRA from the gallery</span></span>
2. <span data-ttu-id="08879-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="08879-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-jira-from-the-gallery"></a><span data-ttu-id="08879-123">從資源庫新增 Kantega SSO for JIRA</span><span class="sxs-lookup"><span data-stu-id="08879-123">Adding Kantega SSO for JIRA from the gallery</span></span>
<span data-ttu-id="08879-124">若要設定將 Kantega SSO for JIRA 整合到 Azure AD 中，您需要從資源庫將 Kantega SSO for JIRA 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="08879-124">To configure the integration of Kantega SSO for JIRA into Azure AD, you need to add Kantega SSO for JIRA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="08879-125">**若要從資源庫新增 Kantega SSO for JIRA，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="08879-125">**To add Kantega SSO for JIRA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="08879-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="08879-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="08879-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="08879-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="08879-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="08879-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="08879-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="08879-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="08879-133">在搜尋方塊中，輸入 **Kantega SSO for JIRA**。</span><span class="sxs-lookup"><span data-stu-id="08879-133">In the search box, type **Kantega SSO for JIRA**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. <span data-ttu-id="08879-135">在結果面板中，選取 [Kantega SSO for JIRA]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="08879-135">In the results panel, select **Kantega SSO for JIRA**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="08879-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="08879-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="08879-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kantega SSO for JIRA 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="08879-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for JIRA based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="08879-139">若要讓單一登入運作，Azure AD 必須知道 Kantega SSO for JIRA 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="08879-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for JIRA is to a user in Azure AD.</span></span> <span data-ttu-id="08879-140">換句話說，必須在 Azure AD 使用者和 Kantega SSO for JIRA 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="08879-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for JIRA needs to be established.</span></span>

<span data-ttu-id="08879-141">在 Kantega SSO for JIRA 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="08879-141">In Kantega SSO for JIRA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="08879-142">若要設定及測試與 Kantega SSO for JIRA 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="08879-142">To configure and test Azure AD single sign-on with Kantega SSO for JIRA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="08879-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="08879-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="08879-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="08879-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08879-145">**[建立 Kantega SSO for JIRA 測試使用者](#creating-a-kantega-sso-for-jira-test-user)** - 使 Kantega SSO for JIRA 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="08879-145">**[Creating a Kantega SSO for JIRA test user](#creating-a-kantega-sso-for-jira-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for JIRA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="08879-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="08879-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08879-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="08879-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="08879-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="08879-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="08879-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Kantega SSO for JIRA 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="08879-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for JIRA application.</span></span>

<span data-ttu-id="08879-150">**若要設定與 Kantega SSO for JIRA 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="08879-150">**To configure Azure AD single sign-on with Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="08879-151">在 Azure 入口網站的 [Kantega SSO for JIRA] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="08879-151">In the Azure portal, on the **Kantega SSO for JIRA** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="08879-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="08879-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. <span data-ttu-id="08879-155">在 **IDP** 起始模式下，在 [Kantega SSO for JIRA 網域及 URL] 區段中執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08879-155">In **IDP** initiated mode, on the **Kantega SSO for JIRA Domain and URLs** section perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    <span data-ttu-id="08879-157">a.</span><span class="sxs-lookup"><span data-stu-id="08879-157">a.</span></span> <span data-ttu-id="08879-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="08879-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="08879-159">b.</span><span class="sxs-lookup"><span data-stu-id="08879-159">b.</span></span> <span data-ttu-id="08879-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="08879-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="08879-161">在 **SP** 起始模式下，勾選 [顯示進階 URL 設定]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08879-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    <span data-ttu-id="08879-163">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="08879-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08879-164">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="08879-164">These values are not real.</span></span> <span data-ttu-id="08879-165">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="08879-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="08879-166">在設定 Jira 外掛程式 (本教學課程稍後會說明) 期間會收到這些值。</span><span class="sxs-lookup"><span data-stu-id="08879-166">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="08879-167">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="08879-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. <span data-ttu-id="08879-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="08879-169">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="08879-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 JIRA 內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="08879-171">In a different web browser window, log in to your JIRA on premise server as an administrator.</span></span>

8. <span data-ttu-id="08879-172">將滑鼠停留在 cog 上，然後按一下 [附加元件]。</span><span class="sxs-lookup"><span data-stu-id="08879-172">Hover on cog and click the **Add-ons**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. <span data-ttu-id="08879-174">在附加元件索引標籤區段下，按一下 [尋找新的附加元件]。</span><span class="sxs-lookup"><span data-stu-id="08879-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="08879-175">搜尋 **Kantega SSO for JIRA (SAML & Kerberos)**，然後按一下 [安裝] 按鈕以安裝新的 SAML 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="08879-175">Search **Kantega SSO for JIRA (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. <span data-ttu-id="08879-177">外掛程式會開始安裝。</span><span class="sxs-lookup"><span data-stu-id="08879-177">The plugin installation starts.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. <span data-ttu-id="08879-179">當安裝完成時。</span><span class="sxs-lookup"><span data-stu-id="08879-179">Once the installation is complete.</span></span> <span data-ttu-id="08879-180">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="08879-180">Click **Close**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. <span data-ttu-id="08879-182">按一下 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="08879-182">Click **Manage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. <span data-ttu-id="08879-184">[整合] 下會列出新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="08879-184">New plugin is listed under **INTEGRATIONS**.</span></span> <span data-ttu-id="08879-185">按一下 [設定] 來設定新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="08879-185">Click **Configure** to configure the new plugin.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. <span data-ttu-id="08879-187">在 [SAML] 區段中。</span><span class="sxs-lookup"><span data-stu-id="08879-187">In the **SAML** section.</span></span> <span data-ttu-id="08879-188">從 [新增識別提供者] 下拉式清單中，選取 [Azure Active Directory]\(Azure AD\)。</span><span class="sxs-lookup"><span data-stu-id="08879-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. <span data-ttu-id="08879-190">選取 [基本] 作為訂用帳戶層級。</span><span class="sxs-lookup"><span data-stu-id="08879-190">Select subscription level as **Basic**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. <span data-ttu-id="08879-192">在 [應用程式屬性] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08879-192">On the **App properties** section, perform following steps:</span></span> 

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    <span data-ttu-id="08879-194">a.</span><span class="sxs-lookup"><span data-stu-id="08879-194">a.</span></span> <span data-ttu-id="08879-195">複製 [應用程式識別碼 URI] 值，然後在 Azure 入口網站的 [Kantega SSO for JIRA 網域及 URL] 區段上，使用此 URI 作為 [識別碼]、[回覆 URL] 和 [登入 URL]。</span><span class="sxs-lookup"><span data-stu-id="08879-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for JIRA Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="08879-196">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="08879-196">b.</span></span> <span data-ttu-id="08879-197">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="08879-197">Click **Next**.</span></span>

17. <span data-ttu-id="08879-198">在 [中繼資料匯入] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08879-198">On the **Metadata import** section, perform following steps:</span></span> 

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    <span data-ttu-id="08879-200">a.</span><span class="sxs-lookup"><span data-stu-id="08879-200">a.</span></span> <span data-ttu-id="08879-201">選取 [我的電腦上的中繼資料檔案]，上傳您從 Azure 入口網站下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="08879-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="08879-202">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="08879-202">b.</span></span> <span data-ttu-id="08879-203">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="08879-203">Click **Next**.</span></span>

18. <span data-ttu-id="08879-204">在 [名稱和 SSO 位置] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08879-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    <span data-ttu-id="08879-206">a.</span><span class="sxs-lookup"><span data-stu-id="08879-206">a.</span></span> <span data-ttu-id="08879-207">在 [識別提供者名稱] 文字方塊中，新增識別提供者的名稱 (例如 Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="08879-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="08879-208">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="08879-208">b.</span></span> <span data-ttu-id="08879-209">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="08879-209">Click **Next**.</span></span>

19. <span data-ttu-id="08879-210">確認簽署憑證，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="08879-210">Verify the Signing certificate and click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. <span data-ttu-id="08879-212">在 [JIRA 使用者帳戶] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08879-212">On the **JIRA user accounts** section, perform following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    <span data-ttu-id="08879-214">a.</span><span class="sxs-lookup"><span data-stu-id="08879-214">a.</span></span> <span data-ttu-id="08879-215">選取 [如果需要，在 JIRA 的內部目錄中建立使用者]，然後輸入使用者群組的適當名稱 (可以是多個</span><span class="sxs-lookup"><span data-stu-id="08879-215">Select **Create users in JIRA's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="08879-216">群組，以逗號分隔)。</span><span class="sxs-lookup"><span data-stu-id="08879-216">of groups separated by comma).</span></span>

    <span data-ttu-id="08879-217">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="08879-217">b.</span></span> <span data-ttu-id="08879-218">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="08879-218">Click **Next**.</span></span>

21. <span data-ttu-id="08879-219">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="08879-219">Click **Finish**.</span></span>   

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. <span data-ttu-id="08879-221">在 [Azure AD 的已知網域] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08879-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    <span data-ttu-id="08879-223">a.</span><span class="sxs-lookup"><span data-stu-id="08879-223">a.</span></span> <span data-ttu-id="08879-224">從頁面的左面板中，選取 [已知網域]。</span><span class="sxs-lookup"><span data-stu-id="08879-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="08879-225">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="08879-225">b.</span></span> <span data-ttu-id="08879-226">在 [已知網域] 文字方塊中，輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="08879-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="08879-227">c.</span><span class="sxs-lookup"><span data-stu-id="08879-227">c.</span></span> <span data-ttu-id="08879-228">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="08879-228">Click **Save**.</span></span> 

> [!TIP]
> <span data-ttu-id="08879-229">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="08879-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="08879-230">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="08879-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="08879-231">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08879-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="08879-232">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="08879-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="08879-233">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="08879-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="08879-235">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="08879-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="08879-236">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="08879-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="08879-238">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="08879-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="08879-240">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="08879-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08879-242">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08879-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08879-244">a.</span><span class="sxs-lookup"><span data-stu-id="08879-244">a.</span></span> <span data-ttu-id="08879-245">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="08879-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08879-246">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="08879-246">b.</span></span> <span data-ttu-id="08879-247">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="08879-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08879-248">c.</span><span class="sxs-lookup"><span data-stu-id="08879-248">c.</span></span> <span data-ttu-id="08879-249">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="08879-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="08879-250">d.</span><span class="sxs-lookup"><span data-stu-id="08879-250">d.</span></span> <span data-ttu-id="08879-251">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="08879-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a><span data-ttu-id="08879-252">建立 Kantega SSO for JIRA 測試使用者</span><span class="sxs-lookup"><span data-stu-id="08879-252">Creating a Kantega SSO for JIRA test user</span></span>

<span data-ttu-id="08879-253">若要讓 Azure AD 使用者能夠登入 JIRA，必須將他們佈建到 JIRA。</span><span class="sxs-lookup"><span data-stu-id="08879-253">To enable Azure AD users to log in to JIRA, they must be provisioned into JIRA.</span></span> <span data-ttu-id="08879-254">在 Kantega SSO for JIRA 中，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="08879-254">In Kantega SSO for JIRA, provisioning is a manual task.</span></span>

<span data-ttu-id="08879-255">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="08879-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="08879-256">以系統管理員身分登入您的 JIRA 內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="08879-256">Log in to your JIRA on premise server as an administrator.</span></span>

2. <span data-ttu-id="08879-257">將滑鼠停留在 cog 上，然後按一下 [使用者管理]。</span><span class="sxs-lookup"><span data-stu-id="08879-257">Hover on cog and click the **User management**.</span></span>

    ![新增員工](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. <span data-ttu-id="08879-259">在 [使用者管理] 索引標籤區段下，按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="08879-259">Under **User management** tab section, click **Create user**.</span></span>

    ![新增員工](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. <span data-ttu-id="08879-261">在 [建立新的使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="08879-261">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![新增員工](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    <span data-ttu-id="08879-263">a.</span><span class="sxs-lookup"><span data-stu-id="08879-263">a.</span></span> <span data-ttu-id="08879-264">在 [電子郵件地址] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="08879-264">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="08879-265">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="08879-265">b.</span></span> <span data-ttu-id="08879-266">在 [全名] 文字方塊中，輸入像是 Britta Simon 的使用者全名。</span><span class="sxs-lookup"><span data-stu-id="08879-266">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="08879-267">c.</span><span class="sxs-lookup"><span data-stu-id="08879-267">c.</span></span> <span data-ttu-id="08879-268">在 [使用者名稱] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件。</span><span class="sxs-lookup"><span data-stu-id="08879-268">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="08879-269">d.</span><span class="sxs-lookup"><span data-stu-id="08879-269">d.</span></span> <span data-ttu-id="08879-270">在 [密碼] 文字方塊中，輸入使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="08879-270">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="08879-271">e.</span><span class="sxs-lookup"><span data-stu-id="08879-271">e.</span></span> <span data-ttu-id="08879-272">按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="08879-272">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="08879-273">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="08879-273">Assigning the Azure AD test user</span></span>

<span data-ttu-id="08879-274">在本節中，您會將 Kantega SSO for JIRA 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="08879-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for JIRA.</span></span>

![指派使用者][200] 

<span data-ttu-id="08879-276">**若要將 Britta Simon 指派給 Kantega SSO for JIRA，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="08879-276">**To assign Britta Simon to Kantega SSO for JIRA, perform the following steps:**</span></span>

1. <span data-ttu-id="08879-277">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="08879-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="08879-279">在應用程式清單中，選取 [Kantega SSO for JIRA]。</span><span class="sxs-lookup"><span data-stu-id="08879-279">In the applications list, select **Kantega SSO for JIRA**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. <span data-ttu-id="08879-281">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="08879-281">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="08879-283">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="08879-283">Click **Add** button.</span></span> <span data-ttu-id="08879-284">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="08879-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="08879-286">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="08879-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="08879-287">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="08879-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08879-288">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="08879-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="08879-289">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="08879-289">Testing single sign-on</span></span>

<span data-ttu-id="08879-290">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="08879-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="08879-291">當您在存取面板中按一下 Kantega SSO for JIRA 圖格時，應該會自動登入您的 Kantega SSO for JIRA 應用程式。</span><span class="sxs-lookup"><span data-stu-id="08879-291">When you click the Kantega SSO for JIRA tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for JIRA application.</span></span>
<span data-ttu-id="08879-292">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="08879-292">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="08879-293">其他資源</span><span class="sxs-lookup"><span data-stu-id="08879-293">Additional resources</span></span>

* [<span data-ttu-id="08879-294">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="08879-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08879-295">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="08879-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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

