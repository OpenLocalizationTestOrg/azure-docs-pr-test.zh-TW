---
title: "教學課程：Azure Active Directory 與 Syncplicity 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Syncplicity 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 1321fa71bcd625d6ea754432bfb402d3919e38f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="0c1c8-103">教學課程：Azure Active Directory 與 Syncplicity 整合</span><span class="sxs-lookup"><span data-stu-id="0c1c8-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="0c1c8-104">在本教學課程中，您將了解如何整合 Syncplicity 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c1c8-105">Syncplicity 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="0c1c8-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0c1c8-106">您可以在 Azure AD 中控制可存取 Syncplicity 的人員</span><span class="sxs-lookup"><span data-stu-id="0c1c8-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="0c1c8-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Syncplicity (單一登入)</span><span class="sxs-lookup"><span data-stu-id="0c1c8-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0c1c8-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="0c1c8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0c1c8-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c1c8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0c1c8-110">Prerequisites</span></span>

<span data-ttu-id="0c1c8-111">若要設定 Azure AD 與 Syncplicity 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0c1c8-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="0c1c8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0c1c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c1c8-113">已啟用 Syncplicity 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0c1c8-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0c1c8-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0c1c8-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0c1c8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c1c8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0c1c8-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0c1c8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0c1c8-118">Scenario description</span></span>
<span data-ttu-id="0c1c8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c1c8-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="0c1c8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c1c8-121">從資源庫新增 Syncplicity</span><span class="sxs-lookup"><span data-stu-id="0c1c8-121">Adding Syncplicity from the gallery</span></span>
2. <span data-ttu-id="0c1c8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0c1c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="0c1c8-123">從資源庫新增 Syncplicity</span><span class="sxs-lookup"><span data-stu-id="0c1c8-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="0c1c8-124">若要設定 Syncplicity 與 Azure AD 整合，您需要從資源庫將 Syncplicity 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0c1c8-125">**若要從資源庫新增 Syncplicity，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0c1c8-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0c1c8-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0c1c8-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0c1c8-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0c1c8-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0c1c8-133">在搜尋方塊中，輸入 **Syncplicity**。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-133">In the search box, type **Syncplicity**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="0c1c8-135">在結果窗格中，選取 [Syncplicity]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0c1c8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0c1c8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0c1c8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Syncplicity 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0c1c8-139">若要讓單一登入運作，Azure AD 必須知道 Syncplicity 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="0c1c8-140">換句話說，必須在 Azure AD 使用者和 Syncplicity 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="0c1c8-141">在 Syncplicity 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0c1c8-142">若要設定及測試與 Syncplicity 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0c1c8-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0c1c8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0c1c8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0c1c8-145">**[建立 Syncplicity 測試使用者](#creating-a-syncplicity-test-user)** - 使 Syncplicity 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0c1c8-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0c1c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0c1c8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0c1c8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0c1c8-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Syncplicity 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="0c1c8-150">**若要設定與 Syncplicity 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0c1c8-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="0c1c8-151">在 Azure 入口網站的 [Syncplicity] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0c1c8-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="0c1c8-155">在 [Syncplicity 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0c1c8-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="0c1c8-157">a.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-157">a.</span></span> <span data-ttu-id="0c1c8-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="0c1c8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="0c1c8-159">b.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-159">b.</span></span> <span data-ttu-id="0c1c8-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="0c1c8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0c1c8-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-161">These values are not real.</span></span> <span data-ttu-id="0c1c8-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0c1c8-163">請連絡 [Syncplicity 客戶支援小組](https://www.syncplicity.com/contact-us)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

4. <span data-ttu-id="0c1c8-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="0c1c8-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0c1c8-168">在 [Syncplicity 組態] 區段上，按一下 [設定 Syncplicity] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0c1c8-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="0c1c8-171">登入您的 **Syncplicity** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-171">Sign in to your **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="0c1c8-172">在上方功能表中按一下 [管理]，選取 [設定]，然後按一下 [自訂網域和單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="0c1c8-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="0c1c8-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="0c1c8-174">在 [單一登入 (SSO)]  對話方塊頁面執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0c1c8-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="0c1c8-175">![單一登入 \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="0c1c8-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="0c1c8-176">a.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-176">a.</span></span> <span data-ttu-id="0c1c8-177">在 [自訂網域]  文字方塊中輸入您的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="0c1c8-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-178">b.</span></span> <span data-ttu-id="0c1c8-179">在 [單一登入狀態] 中選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="0c1c8-180">c.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-180">c.</span></span> <span data-ttu-id="0c1c8-181">在 [實體識別碼] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0c1c8-182">d.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-182">d.</span></span> <span data-ttu-id="0c1c8-183">在 [登入頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0c1c8-184">e.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-184">e.</span></span> <span data-ttu-id="0c1c8-185">在 [登出頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0c1c8-186">f.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-186">f.</span></span> <span data-ttu-id="0c1c8-187">在 [識別提供者憑證] 中，按一下 [選擇檔案]，然後上傳您從 Azure 入口網站下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="0c1c8-188">g.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-188">g.</span></span> <span data-ttu-id="0c1c8-189">按一下 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="0c1c8-190">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="0c1c8-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0c1c8-191">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0c1c8-192">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0c1c8-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0c1c8-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0c1c8-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="0c1c8-194">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0c1c8-196">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0c1c8-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0c1c8-197">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0c1c8-199">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0c1c8-201">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0c1c8-203">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0c1c8-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0c1c8-205">a.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-205">a.</span></span> <span data-ttu-id="0c1c8-206">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0c1c8-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-207">b.</span></span> <span data-ttu-id="0c1c8-208">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0c1c8-209">c.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-209">c.</span></span> <span data-ttu-id="0c1c8-210">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0c1c8-211">d.</span><span class="sxs-lookup"><span data-stu-id="0c1c8-211">d.</span></span> <span data-ttu-id="0c1c8-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="0c1c8-213">建立 Syncplicity 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0c1c8-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="0c1c8-214">AAD 使用者必須先佈建到 Syncplicity 應用程式，才可以登入。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="0c1c8-215">本節描述如何建立 Syncplicity 內的 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="0c1c8-216">**若要將使用者帳戶佈建到 Syncplicity，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0c1c8-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="0c1c8-217">登入您的 **Syncplicity** 租用戶 (例如 `https://company.Syncplicity.com`)。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="0c1c8-218">按一下 [管理員]，然後選取 [使用者帳戶]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="0c1c8-219">按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="0c1c8-220">![管理使用者](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="0c1c8-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="0c1c8-221">輸入您想要佈建之 AAD 帳戶的 [電子郵件地址]，選取 [使用者] 作為 [角色]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="0c1c8-222">![帳戶資訊](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "帳戶資訊")</span><span class="sxs-lookup"><span data-stu-id="0c1c8-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="0c1c8-223">AAD 帳戶的持有者會收到電子郵件，其中包含可確認並啟動帳戶的連結。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="0c1c8-224">選取要讓新使用者成為成員的公司群組，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="0c1c8-225">![群組成員資格](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "群組成員資格")</span><span class="sxs-lookup"><span data-stu-id="0c1c8-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="0c1c8-226">如果未列出群組，請按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="0c1c8-227">選取您想要在使用者電腦上受 Syncplicity 控制的資料夾，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="0c1c8-228">![Syncplicity 資料夾](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity 資料夾")</span><span class="sxs-lookup"><span data-stu-id="0c1c8-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="0c1c8-229">您可以使用任何其他的 Syncplicity 使用者帳戶建立工具或 Syncplicity 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0c1c8-230">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0c1c8-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0c1c8-231">在本節中，您會將 Syncplicity 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![指派使用者][200] 

<span data-ttu-id="0c1c8-233">**若要將 Britta Simon 指派給 Syncplicity，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0c1c8-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="0c1c8-234">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0c1c8-236">在應用程式清單中，選取 [Syncplicity]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-236">In the applications list, select **Syncplicity**.</span></span>

    ![設定單一登入](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="0c1c8-238">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-238">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0c1c8-240">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-240">Click **Add** button.</span></span> <span data-ttu-id="0c1c8-241">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0c1c8-243">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0c1c8-244">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0c1c8-245">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0c1c8-246">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0c1c8-246">Testing single sign-on</span></span>

<span data-ttu-id="0c1c8-247">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0c1c8-248">當您在存取面板中按一下 [Syncplicity] 圖格時，應該會自動登入您的 Syncplicity 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c1c8-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="0c1c8-249">其他資源</span><span class="sxs-lookup"><span data-stu-id="0c1c8-249">Additional resources</span></span>

* [<span data-ttu-id="0c1c8-250">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="0c1c8-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0c1c8-251">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0c1c8-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

