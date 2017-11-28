---
title: "教學課程：Azure Active Directory 與 SAML SSO for Confluence by resolution GmbH 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SAML SSO for Confluence by resolution GmbH 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a36d686ba39b5168860a20e8c4db357888df6a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a><span data-ttu-id="fb410-103">教學課程：Azure Active Directory 與 SAML SSO for Confluence by resolution GmbH 整合</span><span class="sxs-lookup"><span data-stu-id="fb410-103">Tutorial: Azure Active Directory integration with SAML SSO for Confluence by resolution GmbH</span></span>

<span data-ttu-id="fb410-104">在本教學課程中，您將了解如何整合 SAML SSO for Confluence by resolution GmbH 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="fb410-104">In this tutorial, you learn how to integrate SAML SSO for Confluence by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb410-105">SAML SSO for Confluence by resolution GmbH 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="fb410-105">Integrating SAML SSO for Confluence by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fb410-106">您可以在 Azure AD 中控制誰可以存取 SAML SSO for Confluence by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="fb410-106">You can control in Azure AD who has access to SAML SSO for Confluence by resolution GmbH</span></span>
- <span data-ttu-id="fb410-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SAML SSO for Confluence by resolution GmbH (單一登入)</span><span class="sxs-lookup"><span data-stu-id="fb410-107">You can enable your users to automatically get signed-on to SAML SSO for Confluence by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fb410-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="fb410-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fb410-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="fb410-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb410-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="fb410-110">Prerequisites</span></span>

<span data-ttu-id="fb410-111">若要設定 Azure AD 與 SAML SSO for Confluence by resolution GmbH 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="fb410-111">To configure Azure AD integration with SAML SSO for Confluence by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="fb410-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fb410-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb410-113">SAML SSO for Confluence by resolution GmbH 單一登入已啟用的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fb410-113">A SAML SSO for Confluence by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb410-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fb410-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb410-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="fb410-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb410-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fb410-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb410-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="fb410-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb410-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="fb410-118">Scenario description</span></span>
<span data-ttu-id="fb410-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb410-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb410-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="fb410-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb410-121">從資源庫新增 SAML SSO for Confluence by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="fb410-121">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="fb410-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fb410-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="fb410-123">從資源庫新增 SAML SSO for Confluence by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="fb410-123">Adding SAML SSO for Confluence by resolution GmbH from the gallery</span></span>

<span data-ttu-id="fb410-124">若要設定 SAML SSO for Confluence by resolution GmbH 到 Azure AD 的整合，您必須從資源庫將 SAML SSO for Confluence by resolution GmbH 新增至受管理 SaaS 應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="fb410-124">To configure the integration of SAML SSO for Confluence by resolution GmbH into Azure AD, you need to add SAML SSO for Confluence by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fb410-125">**若要從資源庫新增 SAML SSO for Confluence by resolution GmbH，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fb410-125">**To add SAML SSO for Confluence by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fb410-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="fb410-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fb410-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fb410-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fb410-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fb410-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="fb410-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb410-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="fb410-133">在搜尋方塊中，輸入 **SAML SSO for Confluence by resolution GmbH**。</span><span class="sxs-lookup"><span data-stu-id="fb410-133">In the search box, type **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. <span data-ttu-id="fb410-135">在結果窗格中，選取 [SAML SSO for Confluence by resolution GmbH]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb410-135">In the results panel, select **SAML SSO for Confluence by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fb410-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fb410-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="fb410-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAML SSO for Confluence by resolution GmbH 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb410-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fb410-139">若要讓單一登入運作，Azure AD 必須知道 SAML SSO for Confluence by resolution GmbH 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="fb410-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Confluence by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="fb410-140">換句話說，必須在 Azure AD 使用者和 SAML SSO for Confluence by resolution GmbH 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fb410-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Confluence by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="fb410-141">在 SAML SSO for Confluence by resolution GmbH 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fb410-141">In SAML SSO for Confluence by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fb410-142">若要使用 SAML SSO for Confluence by resolution GmbH 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="fb410-142">To configure and test Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fb410-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="fb410-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fb410-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb410-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fb410-145">**[建立 SAML SSO for Confluence by resolution GmbH 測試使用者](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - 讓連結至 Azure AD 之 SAML SSO for Confluence by resolution GmbH 中 Britta Simon 的對應使用者表示使用者。</span><span class="sxs-lookup"><span data-stu-id="fb410-145">**[Creating a SAML SSO for Confluence by resolution GmbH test user](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Confluence by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fb410-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb410-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fb410-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="fb410-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fb410-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fb410-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fb410-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 SAML SSO for Confluence by resolution GmbHl 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb410-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Confluence by resolution GmbH application.</span></span>

<span data-ttu-id="fb410-150">**若要使用 SAML SSO for Confluence by resolution GmbH 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fb410-150">**To configure Azure AD single sign-on with SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="fb410-151">在 Azure 入口網站的 [SAML SSO for Confluence by resolution GmbH] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fb410-151">In the Azure portal, on the **SAML SSO for Confluence by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="fb410-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb410-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. <span data-ttu-id="fb410-155">如果您想要以「IDP 起始模式」設定應用程式，請在 [SAML SSO for Confluence by resolution GmbH 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fb410-155">On the **SAML SSO for Confluence by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    <span data-ttu-id="fb410-157">a.</span><span class="sxs-lookup"><span data-stu-id="fb410-157">a.</span></span> <span data-ttu-id="fb410-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="fb410-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="fb410-159">b.</span><span class="sxs-lookup"><span data-stu-id="fb410-159">b.</span></span> <span data-ttu-id="fb410-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="fb410-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="fb410-161">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="fb410-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="fb410-162">如果您想要以 **SP** 起始模式設定應用程式：</span><span class="sxs-lookup"><span data-stu-id="fb410-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    <span data-ttu-id="fb410-164">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="fb410-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="fb410-165">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="fb410-165">These values are not real.</span></span> <span data-ttu-id="fb410-166">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="fb410-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="fb410-167">請連絡 [SAML SSO for Confluence by resolution GmbH 用戶端支援小組](https://www.resolution.de/go/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="fb410-167">Contact [SAML SSO for Confluence by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="fb410-168">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="fb410-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. <span data-ttu-id="fb410-170">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb410-170">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. <span data-ttu-id="fb410-172">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **SAML SSO for Confluence by resolution GmbH 系統管理入口網站**。</span><span class="sxs-lookup"><span data-stu-id="fb410-172">In a different web browser window, log in to your **SAML SSO for Confluence by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="fb410-173">將滑鼠停留在 cog 上，然後按一下 [附加元件]。</span><span class="sxs-lookup"><span data-stu-id="fb410-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. <span data-ttu-id="fb410-175">系統會將您重新導向至 [系統管理員存取] 頁面。</span><span class="sxs-lookup"><span data-stu-id="fb410-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="fb410-176">輸入密碼，然後按一下 [確認] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb410-176">Enter the password and click **Confirm** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. <span data-ttu-id="fb410-178">在 [ATLASSIAN MARKETPLACE] 索引標籤上，按一下 [尋找新的附加元件]。</span><span class="sxs-lookup"><span data-stu-id="fb410-178">Under **ATLASSIAN MARKETPLACE** tab, click **Find new add-ons**.</span></span> 

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. <span data-ttu-id="fb410-180">搜尋 **SAML Single Sign On (SSO) for Confluence**，然後按一下 [安裝] 按鈕以安裝新的 SAML 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="fb410-180">Search **SAML Single Sign On (SSO) for Confluence** and click **Install** button to install the new SAML plugin.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. <span data-ttu-id="fb410-182">外掛程式將會開始安裝。</span><span class="sxs-lookup"><span data-stu-id="fb410-182">The plugin installation will start.</span></span> <span data-ttu-id="fb410-183">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="fb410-183">Click **Close**.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. <span data-ttu-id="fb410-186">按一下 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="fb410-186">Click **Manage**.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. <span data-ttu-id="fb410-188">按一下 [設定] 來設定新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="fb410-188">Click **Configure** to configure the new plugin.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. <span data-ttu-id="fb410-190">您也可以在 [使用者與安全性] 索引標籤底下找到這個新的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="fb410-190">This new plugin can also be found under **USERS & SECURITY** tab.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. <span data-ttu-id="fb410-192">在 [SAML SingleSignOn 外掛程式組態] 頁面上，按一下 [新增額外的識別提供者] 按鈕以進行識別提供者的設定。</span><span class="sxs-lookup"><span data-stu-id="fb410-192">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. <span data-ttu-id="fb410-194">在這個頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fb410-194">Perform following steps on this page:</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    <span data-ttu-id="fb410-196">a.</span><span class="sxs-lookup"><span data-stu-id="fb410-196">a.</span></span> <span data-ttu-id="fb410-197">新增識別提供者的**名稱** (例如 Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="fb410-197">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="fb410-198">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb410-198">b.</span></span> <span data-ttu-id="fb410-199">新增識別提供者的**描述** (例如 Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="fb410-199">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="fb410-200">c.</span><span class="sxs-lookup"><span data-stu-id="fb410-200">c.</span></span> <span data-ttu-id="fb410-201">按一下 [XML]，然後選取您從 Azure 入口網站下載的**中繼資料**檔案。</span><span class="sxs-lookup"><span data-stu-id="fb410-201">Click **XML** and select the **Metadata** file that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="fb410-202">d.</span><span class="sxs-lookup"><span data-stu-id="fb410-202">d.</span></span> <span data-ttu-id="fb410-203">按一下 [載入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb410-203">Click **Load** button.</span></span>

    <span data-ttu-id="fb410-204">e.</span><span class="sxs-lookup"><span data-stu-id="fb410-204">e.</span></span> <span data-ttu-id="fb410-205">它會讀取 IdP 中繼資料，並且填入螢幕擷取畫面中反白顯示的欄位。</span><span class="sxs-lookup"><span data-stu-id="fb410-205">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 
18. <span data-ttu-id="fb410-206">按一下 [儲存設定] 按鈕以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="fb410-206">Click **Save settings** button to save the settings.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="fb410-208">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="fb410-208">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fb410-209">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="fb410-209">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fb410-210">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fb410-210">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fb410-211">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fb410-211">Creating an Azure AD test user</span></span>
<span data-ttu-id="fb410-212">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="fb410-212">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="fb410-214">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fb410-214">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fb410-215">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="fb410-215">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fb410-217">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="fb410-217">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fb410-219">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fb410-219">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fb410-221">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fb410-221">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fb410-223">a.</span><span class="sxs-lookup"><span data-stu-id="fb410-223">a.</span></span> <span data-ttu-id="fb410-224">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="fb410-224">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb410-225">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb410-225">b.</span></span> <span data-ttu-id="fb410-226">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="fb410-226">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fb410-227">c.</span><span class="sxs-lookup"><span data-stu-id="fb410-227">c.</span></span> <span data-ttu-id="fb410-228">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="fb410-228">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fb410-229">d.</span><span class="sxs-lookup"><span data-stu-id="fb410-229">d.</span></span> <span data-ttu-id="fb410-230">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fb410-230">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a><span data-ttu-id="fb410-231">建立 SAML SSO for Confluence by resolution GmbH 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fb410-231">Creating a SAML SSO for Confluence by resolution GmbH test user</span></span>

<span data-ttu-id="fb410-232">若要讓 Azure AD 使用者登入 SAML SSO for Confluence by resolution GmbH，必須將他們佈建到 SAML SSO for Confluence by resolution GmbH。</span><span class="sxs-lookup"><span data-stu-id="fb410-232">To enable Azure AD users to log in to SAML SSO for Confluence by resolution GmbH, they must be provisioned into SAML SSO for Confluence by resolution GmbH.</span></span>  
<span data-ttu-id="fb410-233">在 SAML SSO for Confluence by resolution GmbH 中，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="fb410-233">In SAML SSO for Confluence by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="fb410-234">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fb410-234">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="fb410-235">以系統管理員身分登入 SAML SSO for Confluence by resolution GmbH 公司網站。</span><span class="sxs-lookup"><span data-stu-id="fb410-235">Log in to your SAML SSO for Confluence by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="fb410-236">將滑鼠停留在 cog 上，然後按一下 [使用者管理]。</span><span class="sxs-lookup"><span data-stu-id="fb410-236">Hover on cog and click the **User management**.</span></span>

    ![新增員工](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. <span data-ttu-id="fb410-238">在 [使用者] 區段底下，按一下 [新增使用者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fb410-238">Under Users section, click **Add users** tab.</span></span> <span data-ttu-id="fb410-239">在 [新增使用者] 對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fb410-239">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![新增員工](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    <span data-ttu-id="fb410-241">a.</span><span class="sxs-lookup"><span data-stu-id="fb410-241">a.</span></span> <span data-ttu-id="fb410-242">在 [使用者名稱] 文字方塊中，輸入使用者 (例如 Britta Simon) 的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="fb410-242">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="fb410-243">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb410-243">b.</span></span> <span data-ttu-id="fb410-244">在 [全名] 文字方塊中，輸入使用者 (例如 Britta Simon) 的全名。</span><span class="sxs-lookup"><span data-stu-id="fb410-244">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="fb410-245">c.</span><span class="sxs-lookup"><span data-stu-id="fb410-245">c.</span></span> <span data-ttu-id="fb410-246">在 [電子郵件] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="fb410-246">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="fb410-247">d.</span><span class="sxs-lookup"><span data-stu-id="fb410-247">d.</span></span> <span data-ttu-id="fb410-248">在 [密碼] 文字方塊中，輸入 Britta Simon 的密碼。</span><span class="sxs-lookup"><span data-stu-id="fb410-248">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="fb410-249">e.</span><span class="sxs-lookup"><span data-stu-id="fb410-249">e.</span></span> <span data-ttu-id="fb410-250">按一下 [確認密碼] 以再次輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="fb410-250">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="fb410-251">f.</span><span class="sxs-lookup"><span data-stu-id="fb410-251">f.</span></span> <span data-ttu-id="fb410-252">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb410-252">Click **Add** button.</span></span>    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fb410-253">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fb410-253">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fb410-254">在本節中，您會將 SAML SSO for Confluence by resolution GmbH 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fb410-254">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Confluence by resolution GmbH.</span></span>

![指派使用者][200] 

<span data-ttu-id="fb410-256">**若要將 Britta Simon 指派至 SAML SSO for Confluence by resolution GmbH，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fb410-256">**To assign Britta Simon to SAML SSO for Confluence by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="fb410-257">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fb410-257">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="fb410-259">在應用程式清單中，選取 [SAML SSO for Confluence by resolution GmbH]。</span><span class="sxs-lookup"><span data-stu-id="fb410-259">In the applications list, select **SAML SSO for Confluence by resolution GmbH**.</span></span>

    ![設定單一登入](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. <span data-ttu-id="fb410-261">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fb410-261">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="fb410-263">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb410-263">Click **Add** button.</span></span> <span data-ttu-id="fb410-264">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fb410-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="fb410-266">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="fb410-266">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fb410-267">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb410-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fb410-268">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb410-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fb410-269">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="fb410-269">Testing single sign-on</span></span>

<span data-ttu-id="fb410-270">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="fb410-270">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fb410-271">當您按一下 [存取面板] 中的 [SAML SSO for Confluence by resolution GmbH] 圖格時，您應該會自動登入 SAML SSO for Confluence by resolution GmbH 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb410-271">When you click the SAML SSO for Confluence by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Confluence by resolution GmbH application.</span></span>
<span data-ttu-id="fb410-272">如需存取面板的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="fb410-272">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fb410-273">其他資源</span><span class="sxs-lookup"><span data-stu-id="fb410-273">Additional resources</span></span>

* [<span data-ttu-id="fb410-274">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="fb410-274">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fb410-275">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="fb410-275">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

