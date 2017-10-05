---
title: "教學課程：Azure Active Directory 與 JIRA SAML SSO by Microsoft 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 JIRA SAML SSO by Microsoft 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b5f7813c8244d2964b6894ae49cd64e0ee71b704
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="e6d77-103">教學課程：Azure Active Directory 與 JIRA SAML SSO by Microsoft 整合</span><span class="sxs-lookup"><span data-stu-id="e6d77-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="e6d77-104">在本教學課程中，您會了解如何整合 JIRA SAML SSO by Microsoft 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e6d77-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e6d77-105">JIRA SAML SSO by Microsoft 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e6d77-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e6d77-106">您可以在 Azure AD 中控制可存取 JIRA SAML SSO by Microsoft 的人員</span><span class="sxs-lookup"><span data-stu-id="e6d77-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="e6d77-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 JIRA SAML SSO by Microsoft (單一登入)</span><span class="sxs-lookup"><span data-stu-id="e6d77-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e6d77-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e6d77-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e6d77-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e6d77-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6d77-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e6d77-110">Prerequisites</span></span>

<span data-ttu-id="e6d77-111">若要設定 Azure AD 與 JIRA SAML SSO by Microsoft 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e6d77-111">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="e6d77-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e6d77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e6d77-113">安裝在 Windows 64 位元伺服器 (在內部部署或雲端 IaaS 基礎結構上) 的 JIRA 伺服器應用程式</span><span class="sxs-lookup"><span data-stu-id="e6d77-113">JIRA server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="e6d77-114">JIRA 伺服器已啟用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="e6d77-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="e6d77-115">請注意下一節提及支援的 JIRA 外掛程式版本。</span><span class="sxs-lookup"><span data-stu-id="e6d77-115">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="e6d77-116">JIRA 伺服器可從網際網路連上，特別是連線至 Azure AD 登入頁面來進行驗證，且應該能夠接收來自 Azure AD 的權杖</span><span class="sxs-lookup"><span data-stu-id="e6d77-116">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="e6d77-117">JIRA 中已設定管理員認證</span><span class="sxs-lookup"><span data-stu-id="e6d77-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="e6d77-118">JIRA 中已停用 WebSudo</span><span class="sxs-lookup"><span data-stu-id="e6d77-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="e6d77-119">JIRA 伺服器應用程式中建立的測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6d77-119">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="e6d77-120">若要測試本教學課程中的步驟，我們不建議使用 JIRA 的生產環境。</span><span class="sxs-lookup"><span data-stu-id="e6d77-120">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="e6d77-121">先在應用程式的開發或預備環境中測試整合，然後使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e6d77-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="e6d77-122">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e6d77-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e6d77-123">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e6d77-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e6d77-124">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e6d77-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="e6d77-125">支援的 JIRA 版本</span><span class="sxs-lookup"><span data-stu-id="e6d77-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="e6d77-126">目前支援下列 JIRA 版本：</span><span class="sxs-lookup"><span data-stu-id="e6d77-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="e6d77-127">JIRA 核心和軟體：6.0 至 7.2.0</span><span class="sxs-lookup"><span data-stu-id="e6d77-127">JIRA Core and Software: 6.0 to 7.2.0</span></span>
- <span data-ttu-id="e6d77-128">JIRA 服務台：3.0 至 3.2</span><span class="sxs-lookup"><span data-stu-id="e6d77-128">JIRA Service Desk: 3.0 to 3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e6d77-129">案例描述</span><span class="sxs-lookup"><span data-stu-id="e6d77-129">Scenario description</span></span>
<span data-ttu-id="e6d77-130">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6d77-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e6d77-131">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e6d77-131">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e6d77-132">從資源庫新增 JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="e6d77-132">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="e6d77-133">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e6d77-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="e6d77-134">從資源庫新增 JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="e6d77-134">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="e6d77-135">如要設定將 JIRA SAML SSO by Microsoft 整合到 Azure AD 中，您需要從資源庫將 JIRA SAML SSO by Microsoft 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="e6d77-135">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e6d77-136">**若要從資源庫新增 JIRA SAML SSO by Microsoft，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6d77-136">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e6d77-137">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e6d77-137">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e6d77-139">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-139">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e6d77-140">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-140">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e6d77-142">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6d77-142">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e6d77-144">在搜尋方塊中，輸入 **JIRA SAML SSO by Microsoft**。</span><span class="sxs-lookup"><span data-stu-id="e6d77-144">In the search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="e6d77-146">在結果面板中，選取 [JIRA SAML SSO by Microsoft]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6d77-146">In the results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e6d77-148">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e6d77-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e6d77-149">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 JIRA SAML SSO by Microsoft 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6d77-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e6d77-150">若要讓單一登入運作，Azure AD 必須知道 JIRA SAML SSO by Microsoft 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e6d77-150">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="e6d77-151">換句話說，必須在 Azure AD 使用者和 JIRA SAML SSO by Microsoft 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e6d77-151">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="e6d77-152">在 JIRA SAML SSO by Microsoft 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e6d77-152">In JIRA SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e6d77-153">若要設定及測試與 JIRA SAML SSO by Microsoft 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e6d77-153">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e6d77-154">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e6d77-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e6d77-155">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6d77-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e6d77-156">**[建立 JIRA SAML SSO by Microsoft 測試使用者](#creating-a-jira-saml-sso-by-microsoft-test-user)** - 使 JIRA SAML SSO by Microsoft 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="e6d77-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e6d77-157">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6d77-157">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e6d77-158">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e6d77-158">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e6d77-159">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e6d77-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e6d77-160">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 JIRA SAML SSO by Microsoft 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6d77-160">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="e6d77-161">**若要設定與 JIRA SAML SSO by Microsoft 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6d77-161">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="e6d77-162">在 Azure 入口網站的 [JIRA SAML SSO by Microsoft] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-162">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e6d77-164">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6d77-164">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="e6d77-166">在 [JIRA SAML SSO by Microsoft 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e6d77-166">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="e6d77-168">a.</span><span class="sxs-lookup"><span data-stu-id="e6d77-168">a.</span></span> <span data-ttu-id="e6d77-169">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="e6d77-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="e6d77-170">b.</span><span class="sxs-lookup"><span data-stu-id="e6d77-170">b.</span></span> <span data-ttu-id="e6d77-171">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="e6d77-171">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="e6d77-172">c.</span><span class="sxs-lookup"><span data-stu-id="e6d77-172">c.</span></span> <span data-ttu-id="e6d77-173">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="e6d77-173">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e6d77-174">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="e6d77-174">These values are not real.</span></span> <span data-ttu-id="e6d77-175">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="e6d77-175">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e6d77-176">如果連接埠是具名 URL，則為選擇性。</span><span class="sxs-lookup"><span data-stu-id="e6d77-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="e6d77-177">在設定 Jira 外掛程式 (本教學課程稍後會說明) 期間會收到這些值。</span><span class="sxs-lookup"><span data-stu-id="e6d77-177">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="e6d77-178">若要產生**中繼資料** URL，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="e6d77-178">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="e6d77-179">a.</span><span class="sxs-lookup"><span data-stu-id="e6d77-179">a.</span></span> <span data-ttu-id="e6d77-180">按一下 [應用程式註冊]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-180">Click **App registrations**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="e6d77-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6d77-182">b.</span></span> <span data-ttu-id="e6d77-183">按一下 [端點] 以開啟 [端點] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e6d77-183">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="e6d77-185">c.</span><span class="sxs-lookup"><span data-stu-id="e6d77-185">c.</span></span> <span data-ttu-id="e6d77-186">按一下複製按鈕複製 [同盟中繼資料文件] URL，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-186">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="e6d77-188">d.</span><span class="sxs-lookup"><span data-stu-id="e6d77-188">d.</span></span> <span data-ttu-id="e6d77-189">現在，移至 [JIRA SAML SSO by Microsoft] 的屬性頁面，使用 [複製] 按鈕複製 [應用程式識別碼]，並將它貼到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-189">Now go to the property page of **JIRA SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="e6d77-191">e.</span><span class="sxs-lookup"><span data-stu-id="e6d77-191">e.</span></span> <span data-ttu-id="e6d77-192">使用下列模式產生**中繼資料 URL**：`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`，並將此值複製到 [記事本]，稍後會用來設定外掛程式。</span><span class="sxs-lookup"><span data-stu-id="e6d77-192">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="e6d77-193">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6d77-193">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e6d77-195">請連絡 [Microsoft](mailto:waadpartners@microsoft.com) 並提供下列 JIRA 外掛程式資訊。</span><span class="sxs-lookup"><span data-stu-id="e6d77-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the JIRA plugin.</span></span>
    
    *   <span data-ttu-id="e6d77-196">客戶名稱：</span><span class="sxs-lookup"><span data-stu-id="e6d77-196">Customer Name:</span></span>
    *   <span data-ttu-id="e6d77-197">主要網域名稱：</span><span class="sxs-lookup"><span data-stu-id="e6d77-197">Primary domain name:</span></span>
    *   <span data-ttu-id="e6d77-198">Azure AD Premium：是/否 (外掛程式適用於所有客戶：免費、基本和進階 SKU)</span><span class="sxs-lookup"><span data-stu-id="e6d77-198">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="e6d77-199">將會使用這項整合的使用者數目：</span><span class="sxs-lookup"><span data-stu-id="e6d77-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="e6d77-200">JIRA 版本：</span><span class="sxs-lookup"><span data-stu-id="e6d77-200">JIRA Version:</span></span>
    *   <span data-ttu-id="e6d77-201">註解：</span><span class="sxs-lookup"><span data-stu-id="e6d77-201">Comments:</span></span>

7. <span data-ttu-id="e6d77-202">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 JIRA 執行個體。</span><span class="sxs-lookup"><span data-stu-id="e6d77-202">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="e6d77-203">將滑鼠停留在 cog 上，然後按一下 [附加元件]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-203">Hover on cog and click the **Add-ons**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="e6d77-205">在 [附加元件] 索引標籤區段下，按一下 [管理附加元件]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="e6d77-207">手動上傳 Microsoft 所提供的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="e6d77-207">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="e6d77-208">安裝外掛程式之後，它會出現在 [管理附加元件] 區段的 [使用者安裝的附加元件] 區段中。</span><span class="sxs-lookup"><span data-stu-id="e6d77-208">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="e6d77-209">按一下 [設定] 來設定新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="e6d77-209">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="e6d77-210">在設定頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e6d77-210">Perform following steps on configuration page:</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="e6d77-212">a.</span><span class="sxs-lookup"><span data-stu-id="e6d77-212">a.</span></span> <span data-ttu-id="e6d77-213">在 [中繼資料 URL] 中，貼上從 Azure AD 產生的**中繼資料 URL**，然後按一下 [解析] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6d77-213">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="e6d77-214">這樣會讀取 IdP 中繼資料 URL 並填入所有欄位資訊。</span><span class="sxs-lookup"><span data-stu-id="e6d77-214">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="e6d77-215">預設 SAML 使用者識別碼位置是名稱識別碼。</span><span class="sxs-lookup"><span data-stu-id="e6d77-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="e6d77-216">您可以將它變更為屬性選項，並輸入適當的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="e6d77-216">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="e6d77-217">請確定只有一個對應至應用程式的憑證，解析中繼資料時就不會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="e6d77-217">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="e6d77-218">如果有多個憑證，則解析中繼資料時，管理員會遇到錯誤。</span><span class="sxs-lookup"><span data-stu-id="e6d77-218">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="e6d77-219">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6d77-219">b.</span></span> <span data-ttu-id="e6d77-220">複製 [識別碼]、[回覆 URL] 和 [登入 URL] 值，然後在 Azure 入口網站的 [JIRA SAML SSO by Microsoft 網域及 URL] 中，分別貼到 [識別碼]、[回覆 URL] 和 [登入 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="e6d77-220">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="e6d77-221">c.</span><span class="sxs-lookup"><span data-stu-id="e6d77-221">c.</span></span> <span data-ttu-id="e6d77-222">在 [登入按鈕名稱] 中，輸入您的組織要讓使用者在登入畫面上看到的按鈕名稱。</span><span class="sxs-lookup"><span data-stu-id="e6d77-222">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="e6d77-223">d.</span><span class="sxs-lookup"><span data-stu-id="e6d77-223">d.</span></span> <span data-ttu-id="e6d77-224">在 [SAML 使用者識別碼位置] 中，選取 [使用者識別碼在 Subject 陳述式的 NameIdentifier 元素中] 或 [使用者識別碼在 Attribute 元素中]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-224">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="e6d77-225">此識別碼必須為 JIRA 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="e6d77-225">This ID has to be the JIRA user id.</span></span> <span data-ttu-id="e6d77-226">如果使用者識別碼不符，系統將不會允許使用者登入。</span><span class="sxs-lookup"><span data-stu-id="e6d77-226">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="e6d77-227">e.</span><span class="sxs-lookup"><span data-stu-id="e6d77-227">e.</span></span> <span data-ttu-id="e6d77-228">如果您選取 [使用者識別碼在 Attribute 元素中] 選項，請在 [屬性名稱] 文字方塊中，輸入需要使用者識別碼的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="e6d77-228">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="e6d77-229">f.</span><span class="sxs-lookup"><span data-stu-id="e6d77-229">f.</span></span> <span data-ttu-id="e6d77-230">如果您使用同盟網域 (例如 ADFS 等) 搭配 Azure AD，請按一下 [啟用主領域探索] 選項，並設定 [網域名稱]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-230">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="e6d77-231">g.</span><span class="sxs-lookup"><span data-stu-id="e6d77-231">g.</span></span> <span data-ttu-id="e6d77-232">在 [網域名稱] 中，如果是使用以 ADFS 為基礎的登入，請在此輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="e6d77-232">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="e6d77-233">h.</span><span class="sxs-lookup"><span data-stu-id="e6d77-233">h.</span></span> <span data-ttu-id="e6d77-234">如果您想要在使用者登出 JIRA 時登出 Azure AD，請勾選 [啟用單一登出]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-234">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="e6d77-235">i.</span><span class="sxs-lookup"><span data-stu-id="e6d77-235">i.</span></span> <span data-ttu-id="e6d77-236">按一下 [儲存] 按鈕以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="e6d77-236">Click **Save** button to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="e6d77-237">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="e6d77-237">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e6d77-238">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="e6d77-238">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e6d77-239">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e6d77-239">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e6d77-240">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6d77-240">Creating an Azure AD test user</span></span>
<span data-ttu-id="e6d77-241">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e6d77-241">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e6d77-243">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6d77-243">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e6d77-244">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e6d77-244">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e6d77-246">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-246">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e6d77-248">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-248">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e6d77-250">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e6d77-250">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e6d77-252">a.</span><span class="sxs-lookup"><span data-stu-id="e6d77-252">a.</span></span> <span data-ttu-id="e6d77-253">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e6d77-253">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e6d77-254">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6d77-254">b.</span></span> <span data-ttu-id="e6d77-255">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="e6d77-255">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e6d77-256">c.</span><span class="sxs-lookup"><span data-stu-id="e6d77-256">c.</span></span> <span data-ttu-id="e6d77-257">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="e6d77-257">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e6d77-258">d.</span><span class="sxs-lookup"><span data-stu-id="e6d77-258">d.</span></span> <span data-ttu-id="e6d77-259">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e6d77-259">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="e6d77-260">建立 JIRA SAML SSO by Microsoft 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6d77-260">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="e6d77-261">若要讓 Azure AD 使用者能夠登入 JIRA 內部部署伺服器，必須將他們佈建到 JIRA SAML SSO by Microsoft。</span><span class="sxs-lookup"><span data-stu-id="e6d77-261">To enable Azure AD users to log in to JIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="e6d77-262">對於 JIRA SAML SSO by Microsoft，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="e6d77-262">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="e6d77-263">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6d77-263">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e6d77-264">以系統管理員身分登入您的 JIRA 內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="e6d77-264">Log in to your JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="e6d77-265">將滑鼠停留在 cog 上，然後按一下 [使用者管理]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-265">Hover on cog and click the **User management**.</span></span>

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="e6d77-267">系統會將您重新導向至 [系統管理員存取] 頁面，以輸入**密碼**，然後按一下 [確認] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6d77-267">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="e6d77-269">在 [使用者管理] 索引標籤區段下，按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-269">Under **User management** tab section, click **create user**.</span></span>

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="e6d77-271">在 [建立新的使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e6d77-271">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![新增員工](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="e6d77-273">a.</span><span class="sxs-lookup"><span data-stu-id="e6d77-273">a.</span></span> <span data-ttu-id="e6d77-274">在 [電子郵件地址] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e6d77-274">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="e6d77-275">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6d77-275">b.</span></span> <span data-ttu-id="e6d77-276">在 [全名] 文字方塊中，輸入像是 Britta Simon 的使用者全名。</span><span class="sxs-lookup"><span data-stu-id="e6d77-276">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="e6d77-277">c.</span><span class="sxs-lookup"><span data-stu-id="e6d77-277">c.</span></span> <span data-ttu-id="e6d77-278">在 [使用者名稱] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e6d77-278">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="e6d77-279">d.</span><span class="sxs-lookup"><span data-stu-id="e6d77-279">d.</span></span> <span data-ttu-id="e6d77-280">在 [密碼] 文字方塊中，輸入使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="e6d77-280">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="e6d77-281">e.</span><span class="sxs-lookup"><span data-stu-id="e6d77-281">e.</span></span> <span data-ttu-id="e6d77-282">按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-282">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e6d77-283">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e6d77-283">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e6d77-284">在本節中，您會將 JIRA SAML SSO by Microsoft 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e6d77-284">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span></span>

![指派使用者][200] 

<span data-ttu-id="e6d77-286">**若要將 Britta Simon 指派給 JIRA SAML SSO by Microsoft，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e6d77-286">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="e6d77-287">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-287">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e6d77-289">在應用程式清單中，選取 [JIRA SAML SSO by Microsoft]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-289">In the applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![設定單一登入](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="e6d77-291">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-291">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e6d77-293">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6d77-293">Click **Add** button.</span></span> <span data-ttu-id="e6d77-294">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-294">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e6d77-296">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e6d77-296">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e6d77-297">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6d77-297">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e6d77-298">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e6d77-298">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e6d77-299">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e6d77-299">Testing single sign-on</span></span>

<span data-ttu-id="e6d77-300">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="e6d77-300">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e6d77-301">當您在存取面板中按一下 [JIRA SAML SSO by Microsoft] 圖格時，應該會自動登入您的 JIRA SAML SSO by Microsoft 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e6d77-301">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="e6d77-302">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e6d77-302">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e6d77-303">其他資源</span><span class="sxs-lookup"><span data-stu-id="e6d77-303">Additional resources</span></span>

* [<span data-ttu-id="e6d77-304">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e6d77-304">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e6d77-305">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e6d77-305">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

