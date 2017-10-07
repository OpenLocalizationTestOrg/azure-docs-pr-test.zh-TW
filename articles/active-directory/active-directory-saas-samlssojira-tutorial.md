---
title: "教學課程：Azure Active Directory 與 SAML SSO for Jira by resolution GmbH 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與解析 GmbH Jira 的 SAML SSO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="db4e1-103">教學課程：Azure Active Directory 與 SAML SSO for Jira by resolution GmbH 整合</span><span class="sxs-lookup"><span data-stu-id="db4e1-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="db4e1-104">在此教學課程中，您學會如何解析與 Azure Active Directory (Azure AD) GmbH toointegrate Jira 的 SAML SSO。</span><span class="sxs-lookup"><span data-stu-id="db4e1-104">In this tutorial, you learn how toointegrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="db4e1-105">解析 GmbH 與 Azure AD 整合的 Jira SAML SSO 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="db4e1-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="db4e1-106">您可以控制存取 tooSAML SSO 的 Jira 解析 GmbH Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="db4e1-106">You can control in Azure AD who has access tooSAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="db4e1-107">您可以啟用您的使用者 tooautomatically get 登入 tooSAML SSO Jira 的解析度 GmbH （單一登入），其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="db4e1-107">You can enable your users tooautomatically get signed-on tooSAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="db4e1-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="db4e1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="db4e1-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="db4e1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db4e1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="db4e1-110">Prerequisites</span></span>

<span data-ttu-id="db4e1-111">tooconfigure 解析 GmbH Jira 的 SAML sso 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="db4e1-111">tooconfigure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need hello following items:</span></span>

- <span data-ttu-id="db4e1-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="db4e1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="db4e1-113">SAML SSO for Jira by resolution GmbH 單一登入已啟用的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="db4e1-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="db4e1-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="db4e1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="db4e1-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="db4e1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="db4e1-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="db4e1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="db4e1-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="db4e1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="db4e1-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="db4e1-118">Scenario description</span></span>
<span data-ttu-id="db4e1-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="db4e1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="db4e1-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="db4e1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="db4e1-121">解析 GmbH 加入 Jira 的 SAML SSO，從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="db4e1-121">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
2. <span data-ttu-id="db4e1-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="db4e1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a><span data-ttu-id="db4e1-123">解析 GmbH 加入 Jira 的 SAML SSO，從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="db4e1-123">Adding SAML SSO for Jira by resolution GmbH from hello gallery</span></span>
<span data-ttu-id="db4e1-124">tooconfigure hello 整合 Jira 的 SAML SSO 解析 GmbH 到 Azure AD，您需要 tooadd SAML SSO Jira 解析 GmbH hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="db4e1-124">tooconfigure hello integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need tooadd SAML SSO for Jira by resolution GmbH from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="db4e1-125">**解析從 hello 圖庫 GmbH tooadd Jira 的 SAML SSO 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="db4e1-125">**tooadd SAML SSO for Jira by resolution GmbH from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="db4e1-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="db4e1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="db4e1-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="db4e1-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="db4e1-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="db4e1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="db4e1-133">在 [hello] 搜尋方塊中，輸入**解析 GmbH Jira 的 SAML SSO**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-133">In hello search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="db4e1-135">在 hello 結果 窗格中，選取 **解析 GmbH Jira 的 SAML SSO**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="db4e1-135">In hello results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="db4e1-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="db4e1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="db4e1-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAML SSO for Jira by resolution GmbH 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="db4e1-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="db4e1-139">針對單一登入 toowork，Azure AD 需要 tooknow Jira 的 SAML sso GmbH 是 tooa 使用者在 Azure AD 中解析何種 hello 對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="db4e1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAML SSO for Jira by resolution GmbH is tooa user in Azure AD.</span></span> <span data-ttu-id="db4e1-140">換句話說，Azure AD 使用者與 hello 相關的使用者 Jira 的 SAML SSO 中解析之間的連結關聯性 GmbH 需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="db4e1-140">In other words, a link relationship between an Azure AD user and hello related user in SAML SSO for Jira by resolution GmbH needs toobe established.</span></span>

<span data-ttu-id="db4e1-141">解析 GmbH Jira 的 SAML SSO 中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="db4e1-141">In SAML SSO for Jira by resolution GmbH, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="db4e1-142">tooconfigure 及測試 Azure AD 單一登入與 SAML SSO Jira 解析 GmbH，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="db4e1-142">tooconfigure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="db4e1-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="db4e1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="db4e1-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="db4e1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="db4e1-145">**[建立 Jira 解析 GmbH 測試使用者的 SAML SSO](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave 解析是連結的 toohello Azure AD 使用者表示法的 GmbH 許 Simon Jira 的 SAML SSO 中的對應。</span><span class="sxs-lookup"><span data-stu-id="db4e1-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - toohave a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="db4e1-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="db4e1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="db4e1-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="db4e1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="db4e1-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="db4e1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="db4e1-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並解析 GmbH 應用程式設定單一登入的 Jira 您 SAML SSO 中。</span><span class="sxs-lookup"><span data-stu-id="db4e1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="db4e1-150">**tooconfigure Azure AD 單一登入使用 Jira 的 SAML SSO 解析 GmbH，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="db4e1-150">**tooconfigure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="db4e1-151">在 Azure 入口網站上 hello hello**解析 GmbH Jira 的 SAML SSO**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-151">In hello Azure portal, on hello **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="db4e1-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="db4e1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="db4e1-155">在 hello **Jira 解析 GmbH 網域和 Url 的 SAML SSO**區段中，如果您想 tooconfigure hello 應用程式中的**IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="db4e1-155">On hello **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="db4e1-157">a.</span><span class="sxs-lookup"><span data-stu-id="db4e1-157">a.</span></span> <span data-ttu-id="db4e1-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="db4e1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="db4e1-159">b.</span><span class="sxs-lookup"><span data-stu-id="db4e1-159">b.</span></span> <span data-ttu-id="db4e1-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="db4e1-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="db4e1-161">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="db4e1-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="db4e1-162">如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="db4e1-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="db4e1-164">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="db4e1-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="db4e1-165">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="db4e1-165">These values are not real.</span></span> <span data-ttu-id="db4e1-166">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="db4e1-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="db4e1-167">請連絡[Jira 解析 GmbH 用戶端的 SAML SSO 支援小組](https://www.resolution.de/go/support)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="db4e1-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) tooget these values.</span></span> 

5. <span data-ttu-id="db4e1-168">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="db4e1-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="db4e1-170">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="db4e1-170">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="db4e1-172">在不同的網頁瀏覽器視窗中，登入 tooyour **Jira 解析 GmbH 管理員入口網站的 SAML SSO**身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="db4e1-172">In a different web browser window, log in tooyour **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="db4e1-173">將滑鼠停留在齒輪，然後按一下 hello**附加元件**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-173">Hover on cog and click hello **Add-ons**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="db4e1-175">您已重新導向的 tooAdministrator 存取頁面。</span><span class="sxs-lookup"><span data-stu-id="db4e1-175">You are redirected tooAdministrator Access page.</span></span> <span data-ttu-id="db4e1-176">輸入 hello**密碼**按一下**確認** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="db4e1-176">Enter hello **Password** and click **Confirm** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="db4e1-178">在附加元件索引標籤區段下，按一下 [尋找新的附加元件]。</span><span class="sxs-lookup"><span data-stu-id="db4e1-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="db4e1-179">搜尋**SAML 單一登入 (SSO) 針對 JIRA**按一下**安裝**按鈕 tooinstall hello 新 SAML 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="db4e1-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button tooinstall hello new SAML plugin.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="db4e1-181">hello 外掛程式安裝將會啟動。</span><span class="sxs-lookup"><span data-stu-id="db4e1-181">hello plugin installation will start.</span></span> <span data-ttu-id="db4e1-182">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="db4e1-182">Click **Close**.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="db4e1-185">按一下 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="db4e1-185">Click **Manage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="db4e1-187">按一下**設定**tooconfigure hello 新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="db4e1-187">Click **Configure** tooconfigure hello new plugin.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="db4e1-189">在**設定 SAML 單一登入外掛程式**頁面上，按一下**新增其他身分識別提供者**按鈕 tooconfigure hello 設定身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="db4e1-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button tooconfigure hello settings of Identity Provider.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="db4e1-191">在這個頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="db4e1-191">Perform following steps on this page:</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="db4e1-193">a.</span><span class="sxs-lookup"><span data-stu-id="db4e1-193">a.</span></span> <span data-ttu-id="db4e1-194">新增**名稱**的 hello 身分識別提供者 （例如 Azure AD）。</span><span class="sxs-lookup"><span data-stu-id="db4e1-194">Add **Name** of hello Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="db4e1-195">b.</span><span class="sxs-lookup"><span data-stu-id="db4e1-195">b.</span></span> <span data-ttu-id="db4e1-196">新增**描述**的 hello 身分識別提供者 （例如 Azure AD）。</span><span class="sxs-lookup"><span data-stu-id="db4e1-196">Add **Description** of hello Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="db4e1-197">c.</span><span class="sxs-lookup"><span data-stu-id="db4e1-197">c.</span></span> <span data-ttu-id="db4e1-198">按一下**XML**和選取 hello**中繼資料**您從 Azure 入口網站下載的檔案。</span><span class="sxs-lookup"><span data-stu-id="db4e1-198">Click **XML** and select hello **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="db4e1-199">d.</span><span class="sxs-lookup"><span data-stu-id="db4e1-199">d.</span></span> <span data-ttu-id="db4e1-200">按一下 [載入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="db4e1-200">Click **Load** button.</span></span>

    <span data-ttu-id="db4e1-201">e.</span><span class="sxs-lookup"><span data-stu-id="db4e1-201">e.</span></span> <span data-ttu-id="db4e1-202">它會讀取 hello IdP 中繼資料，並於其中填入 hello hello 螢幕擷取畫面中反白顯示的欄位。</span><span class="sxs-lookup"><span data-stu-id="db4e1-202">It reads hello IdP metadata and populates hello fields as highlighted in hello screenshot.</span></span>   

16. <span data-ttu-id="db4e1-203">按一下**儲存設定**按鈕 toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="db4e1-203">Click **Save settings** button toosave hello settings.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="db4e1-205">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="db4e1-205">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="db4e1-206">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="db4e1-206">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="db4e1-207">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="db4e1-207">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="db4e1-208">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="db4e1-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="db4e1-209">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="db4e1-209">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="db4e1-211">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="db4e1-211">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="db4e1-212">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="db4e1-212">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="db4e1-214">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-214">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="db4e1-216">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="db4e1-216">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="db4e1-218">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="db4e1-218">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="db4e1-220">a.</span><span class="sxs-lookup"><span data-stu-id="db4e1-220">a.</span></span> <span data-ttu-id="db4e1-221">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-221">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="db4e1-222">b.</span><span class="sxs-lookup"><span data-stu-id="db4e1-222">b.</span></span> <span data-ttu-id="db4e1-223">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="db4e1-223">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="db4e1-224">c.</span><span class="sxs-lookup"><span data-stu-id="db4e1-224">c.</span></span> <span data-ttu-id="db4e1-225">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-225">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="db4e1-226">d.</span><span class="sxs-lookup"><span data-stu-id="db4e1-226">d.</span></span> <span data-ttu-id="db4e1-227">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="db4e1-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="db4e1-228">建立 SAML SSO for Jira by resolution GmbH 測試使用者</span><span class="sxs-lookup"><span data-stu-id="db4e1-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="db4e1-229">tooenable Azure AD 使用者 toolog 中解析 GmbH tooSAML Jira 的 SSO，它們必須佈建到 Jira 的 SAML SSO 解析 GmbH。</span><span class="sxs-lookup"><span data-stu-id="db4e1-229">tooenable Azure AD users toolog in tooSAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="db4e1-230">在 SAML SSO for Jira by resolution GmbH 中，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="db4e1-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="db4e1-231">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="db4e1-231">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="db4e1-232">登入 tooyour SAML SSO Jira 解析 GmbH 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="db4e1-232">Log in tooyour SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="db4e1-233">將滑鼠停留在齒輪，然後按一下 hello**使用者管理**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-233">Hover on cog and click hello **User management**.</span></span>

    ![新增員工](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="db4e1-235">您會重新導向的 tooAdministrator 存取頁面 tooenter**密碼**按一下**確認** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="db4e1-235">You are redirected tooAdministrator Access page tooenter **Password** and click **Confirm** button.</span></span>

    ![新增員工](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="db4e1-237">在 [使用者管理] 索引標籤區段下，按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="db4e1-237">Under **User management** tab section, click **create user**.</span></span>

    ![新增員工](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="db4e1-239">在 hello **「 建立新的使用者 」**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="db4e1-239">On hello **“Create new user”** dialog page, perform hello following steps:</span></span>

    ![新增員工](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="db4e1-241">a.</span><span class="sxs-lookup"><span data-stu-id="db4e1-241">a.</span></span> <span data-ttu-id="db4e1-242">在 hello**電子郵件地址**文字方塊中，輸入 hello 電子郵件地址的使用者喜歡Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="db4e1-242">In hello **Email address** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="db4e1-243">b.</span><span class="sxs-lookup"><span data-stu-id="db4e1-243">b.</span></span> <span data-ttu-id="db4e1-244">在 hello**全名**文字方塊中，例如許 Simon 的 hello 使用者類型完整名稱。</span><span class="sxs-lookup"><span data-stu-id="db4e1-244">In hello **Full Name** textbox, type full name of hello user like Britta Simon.</span></span>

    <span data-ttu-id="db4e1-245">c.</span><span class="sxs-lookup"><span data-stu-id="db4e1-245">c.</span></span> <span data-ttu-id="db4e1-246">在 hello **Username**文字方塊中，型別 hello 電子郵件的使用者要Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="db4e1-246">In hello **Username** textbox, type hello email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="db4e1-247">d.</span><span class="sxs-lookup"><span data-stu-id="db4e1-247">d.</span></span> <span data-ttu-id="db4e1-248">在 hello**密碼**文字方塊中，輸入 hello 密碼的使用者。</span><span class="sxs-lookup"><span data-stu-id="db4e1-248">In hello **Password** textbox, type hello password of user.</span></span>

    <span data-ttu-id="db4e1-249">e.</span><span class="sxs-lookup"><span data-stu-id="db4e1-249">e.</span></span> <span data-ttu-id="db4e1-250">按一下 [建立使用者]。</span><span class="sxs-lookup"><span data-stu-id="db4e1-250">Click **Create user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="db4e1-251">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="db4e1-251">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="db4e1-252">在本節中，您可以授與解析 GmbH 存取 tooSAML SSO Jira 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="db4e1-252">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAML SSO for Jira by resolution GmbH.</span></span>

![指派使用者][200] 

<span data-ttu-id="db4e1-254">**tooassign 許 Simon tooSAML Jira 的 SSO 解析 GmbH，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="db4e1-254">**tooassign Britta Simon tooSAML SSO for Jira by resolution GmbH, perform hello following steps:**</span></span>

1. <span data-ttu-id="db4e1-255">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-255">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="db4e1-257">在 [hello] 應用程式清單中，選取**解析 GmbH Jira 的 SAML SSO**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-257">In hello applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="db4e1-259">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="db4e1-259">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="db4e1-261">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="db4e1-261">Click **Add** button.</span></span> <span data-ttu-id="db4e1-262">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="db4e1-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="db4e1-264">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="db4e1-264">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="db4e1-265">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="db4e1-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="db4e1-266">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="db4e1-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="db4e1-267">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="db4e1-267">Testing single sign-on</span></span>

<span data-ttu-id="db4e1-268">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="db4e1-268">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="db4e1-269">當您按一下 hello Jira 的 SAML SSO 所解析 GmbH 磚 hello 存取面板中時，您應該取得 Jira 自動登入 tooyour SAML SSO 解析 GmbH 應用程式。</span><span class="sxs-lookup"><span data-stu-id="db4e1-269">When you click hello SAML SSO for Jira by resolution GmbH tile in hello Access Panel, you should get automatically signed-on tooyour SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="db4e1-270">如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="db4e1-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="db4e1-271">其他資源</span><span class="sxs-lookup"><span data-stu-id="db4e1-271">Additional resources</span></span>

* [<span data-ttu-id="db4e1-272">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db4e1-272">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="db4e1-273">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="db4e1-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

