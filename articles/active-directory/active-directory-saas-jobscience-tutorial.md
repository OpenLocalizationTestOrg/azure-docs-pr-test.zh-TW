---
title: "教學課程：Azure Active Directory 與 Jobscience 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Jobscience 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="20d8b-103">教學課程：Azure Active Directory 與 Jobscience 整合</span><span class="sxs-lookup"><span data-stu-id="20d8b-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="20d8b-104">在本教學課程中，您會了解如何整合 Jobscience 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="20d8b-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="20d8b-105">Jobscience 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="20d8b-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="20d8b-106">您可以在 Azure AD 中控制可存取 Jobscience 的人員</span><span class="sxs-lookup"><span data-stu-id="20d8b-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="20d8b-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Kantega SSO for FishEye/Crucible (單一登入)</span><span class="sxs-lookup"><span data-stu-id="20d8b-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="20d8b-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="20d8b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="20d8b-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="20d8b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20d8b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="20d8b-110">Prerequisites</span></span>

<span data-ttu-id="20d8b-111">若要設定 Azure AD 與 Jobscience 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="20d8b-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="20d8b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="20d8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="20d8b-113">啟用 Jobscience 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="20d8b-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="20d8b-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="20d8b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="20d8b-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="20d8b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="20d8b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="20d8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="20d8b-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="20d8b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="20d8b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="20d8b-118">Scenario description</span></span>
<span data-ttu-id="20d8b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20d8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="20d8b-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="20d8b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="20d8b-121">從資源庫新增 Jobscience</span><span class="sxs-lookup"><span data-stu-id="20d8b-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="20d8b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="20d8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="20d8b-123">從資源庫新增 Jobscience</span><span class="sxs-lookup"><span data-stu-id="20d8b-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="20d8b-124">若要設定將 Jobscience 整合到 Azure AD 中，您需要從資源庫將 Jobscience 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="20d8b-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="20d8b-125">**若要從資源庫新增 Jobscience，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="20d8b-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="20d8b-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="20d8b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="20d8b-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="20d8b-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="20d8b-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="20d8b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="20d8b-133">在搜尋方塊中，輸入 **Jobscience**。</span><span class="sxs-lookup"><span data-stu-id="20d8b-133">In the search box, type **Jobscience**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="20d8b-135">在結果面板中，選取 [Jobscience]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="20d8b-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="20d8b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="20d8b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="20d8b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Jobscience 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20d8b-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="20d8b-139">若要讓單一登入運作，Azure AD 必須知道 Jobscience 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="20d8b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="20d8b-140">換句話說，必須在 Azure AD 使用者和 Jobscience 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="20d8b-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="20d8b-141">在 Jobscience 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="20d8b-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="20d8b-142">若要設定及測試與 Jobscience 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="20d8b-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="20d8b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="20d8b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="20d8b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20d8b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="20d8b-145">**[建立 Jobscience 測試使用者](#creating-a-jobscience-test-user)** - 使 Jobscience 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="20d8b-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="20d8b-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20d8b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="20d8b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="20d8b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="20d8b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="20d8b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="20d8b-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Jobscience 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="20d8b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="20d8b-150">**若要設定與 Jobscience 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="20d8b-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="20d8b-151">在 Azure 入口網站的 [Jobscience] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="20d8b-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="20d8b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="20d8b-155">在 [Jobscience 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="20d8b-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="20d8b-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="20d8b-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="20d8b-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="20d8b-158">This value is not real.</span></span> <span data-ttu-id="20d8b-159">請使用實際的登入 URL 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="20d8b-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="20d8b-160">從 [Jobscience 客戶支援小組](https://www.jobscience.com/support)或從您將建立的 SSO 設定檔 (本教學課程稍後會說明) 取得此值。</span><span class="sxs-lookup"><span data-stu-id="20d8b-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="20d8b-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="20d8b-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="20d8b-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="20d8b-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="20d8b-165">在 [Jobscience 組態] 區段上，按一下 [設定 Jobscience] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="20d8b-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="20d8b-166">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="20d8b-168">以系統管理員身分登入您的 Jobscience 公司網站。</span><span class="sxs-lookup"><span data-stu-id="20d8b-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="20d8b-169">移到 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="20d8b-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="20d8b-170">![設定](./media/active-directory-saas-jobscience-tutorial/IC784358.png "設定")</span><span class="sxs-lookup"><span data-stu-id="20d8b-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="20d8b-171">在 [系統管理員] 區段的左方導覽窗格中，按一下 [網域管理] 展開相關的區段，然後按一下 [我的網域] 來開啟 [我的網域] 頁面。</span><span class="sxs-lookup"><span data-stu-id="20d8b-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="20d8b-172">![我的網域](./media/active-directory-saas-jobscience-tutorial/ic767825.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="20d8b-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="20d8b-173">若要確認已正確設定您的網域，請確定目前在 [步驟 4 已部署到使用者] 中，然後檢閱 [我的網域設定]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="20d8b-174">![已部署到使用者的網域](./media/active-directory-saas-jobscience-tutorial/ic784377.png "已部署到使用者的網域")</span><span class="sxs-lookup"><span data-stu-id="20d8b-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="20d8b-175">在 Jobscience 公司網站上，按一下 [安全性控制項]，然後按一下 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="20d8b-176">![安全性控制項](./media/active-directory-saas-jobscience-tutorial/ic784364.png "安全性控制項")</span><span class="sxs-lookup"><span data-stu-id="20d8b-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="20d8b-177">在 [單一登入設定]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="20d8b-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="20d8b-178">![單一登入設定](./media/active-directory-saas-jobscience-tutorial/ic781026.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="20d8b-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="20d8b-179">a.</span><span class="sxs-lookup"><span data-stu-id="20d8b-179">a.</span></span> <span data-ttu-id="20d8b-180">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="20d8b-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="20d8b-181">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="20d8b-181">b.</span></span> <span data-ttu-id="20d8b-182">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="20d8b-182">Click **New**.</span></span>

13. <span data-ttu-id="20d8b-183">在 [SAML 單一登入設定編輯]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="20d8b-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="20d8b-184">![SAML 單一登入設定](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML 單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="20d8b-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="20d8b-185">a.</span><span class="sxs-lookup"><span data-stu-id="20d8b-185">a.</span></span> <span data-ttu-id="20d8b-186">在 [名稱]  文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="20d8b-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="20d8b-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="20d8b-187">b.</span></span> <span data-ttu-id="20d8b-188">在 [簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="20d8b-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="20d8b-189">c.</span><span class="sxs-lookup"><span data-stu-id="20d8b-189">c.</span></span> <span data-ttu-id="20d8b-190">在 [實體識別碼] 文字方塊中，輸入 `https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="20d8b-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="20d8b-191">d.</span><span class="sxs-lookup"><span data-stu-id="20d8b-191">d.</span></span> <span data-ttu-id="20d8b-192">按一下 [瀏覽]  來上傳您的 Azure AD 憑證。</span><span class="sxs-lookup"><span data-stu-id="20d8b-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="20d8b-193">e.</span><span class="sxs-lookup"><span data-stu-id="20d8b-193">e.</span></span> <span data-ttu-id="20d8b-194">對於 [SAML 身分識別類型]，選取 [判斷提示包含來自使用者物件的同盟識別碼]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="20d8b-195">f.</span><span class="sxs-lookup"><span data-stu-id="20d8b-195">f.</span></span> <span data-ttu-id="20d8b-196">在 [SAML 識別位置]，請選取 [識別位於 Subject 陳述式的 NameIdentifier 元素中]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="20d8b-197">g.</span><span class="sxs-lookup"><span data-stu-id="20d8b-197">g.</span></span> <span data-ttu-id="20d8b-198">在 [識別提供者登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="20d8b-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="20d8b-199">h.</span><span class="sxs-lookup"><span data-stu-id="20d8b-199">h.</span></span> <span data-ttu-id="20d8b-200">在 [識別提供者登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="20d8b-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="20d8b-201">i.</span><span class="sxs-lookup"><span data-stu-id="20d8b-201">i.</span></span> <span data-ttu-id="20d8b-202">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="20d8b-202">Click **Save**.</span></span>

14. <span data-ttu-id="20d8b-203">在 [系統管理員] 區段的左方導覽窗格中，按一下 [網域管理] 展開相關的區段，然後按一下 [我的網域] 來開啟 [我的網域] 頁面。</span><span class="sxs-lookup"><span data-stu-id="20d8b-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="20d8b-204">![我的網域](./media/active-directory-saas-jobscience-tutorial/ic767825.png "我的網域")</span><span class="sxs-lookup"><span data-stu-id="20d8b-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="20d8b-205">在 [我的網域] 頁面的 [登入頁面商標] 區段中，按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="20d8b-206">![登入頁面商標](./media/active-directory-saas-jobscience-tutorial/ic767826.png "登入頁面商標")</span><span class="sxs-lookup"><span data-stu-id="20d8b-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="20d8b-207">[登入頁面商標] 頁面的 [驗證服務] 區段中，會顯示您的 [SAML SSO 設定] 的名稱。</span><span class="sxs-lookup"><span data-stu-id="20d8b-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="20d8b-208">請選取該名稱，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="20d8b-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="20d8b-209">![登入頁面商標](./media/active-directory-saas-jobscience-tutorial/ic784366.png "登入頁面商標")</span><span class="sxs-lookup"><span data-stu-id="20d8b-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="20d8b-210">若要取得 SP 初始化的單一登入 URL，請按一下 [安全性控制項] 功能表區段中的 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="20d8b-211">![安全性控制項](./media/active-directory-saas-jobscience-tutorial/ic784368.png "安全性控制項")</span><span class="sxs-lookup"><span data-stu-id="20d8b-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="20d8b-212">按一下您已經在上述步驟中建立的 SSO 設定檔。</span><span class="sxs-lookup"><span data-stu-id="20d8b-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="20d8b-213">此頁面會顯示您公司的單一登入 URL (例如 [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid))。</span><span class="sxs-lookup"><span data-stu-id="20d8b-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="20d8b-214">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="20d8b-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="20d8b-215">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="20d8b-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="20d8b-216">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="20d8b-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="20d8b-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="20d8b-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="20d8b-218">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="20d8b-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="20d8b-220">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="20d8b-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="20d8b-221">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="20d8b-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="20d8b-223">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="20d8b-225">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="20d8b-227">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="20d8b-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="20d8b-229">a.</span><span class="sxs-lookup"><span data-stu-id="20d8b-229">a.</span></span> <span data-ttu-id="20d8b-230">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="20d8b-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="20d8b-231">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="20d8b-231">b.</span></span> <span data-ttu-id="20d8b-232">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="20d8b-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="20d8b-233">c.</span><span class="sxs-lookup"><span data-stu-id="20d8b-233">c.</span></span> <span data-ttu-id="20d8b-234">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="20d8b-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="20d8b-235">d.</span><span class="sxs-lookup"><span data-stu-id="20d8b-235">d.</span></span> <span data-ttu-id="20d8b-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="20d8b-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="20d8b-237">建立 Jobscience 測試使用者</span><span class="sxs-lookup"><span data-stu-id="20d8b-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="20d8b-238">若要讓 Azure AD 使用者能夠登入 Jobscience，必須將他們佈建到 Jobscience。</span><span class="sxs-lookup"><span data-stu-id="20d8b-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="20d8b-239">Jobscience 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="20d8b-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="20d8b-240">您可以使用任何其他的 Jobscience 使用者帳戶建立工具，或 Jobscience 提供的 API，以佈建 Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="20d8b-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="20d8b-241">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="20d8b-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="20d8b-242">以系統管理員身分登入您的 **Jobscience** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="20d8b-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="20d8b-243">移到 [設定]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-243">Go to Setup.</span></span>
   
   <span data-ttu-id="20d8b-244">![設定](./media/active-directory-saas-jobscience-tutorial/ic784358.png "設定")</span><span class="sxs-lookup"><span data-stu-id="20d8b-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="20d8b-245">移至 [管理使用者 \> 使用者]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="20d8b-246">![使用者](./media/active-directory-saas-jobscience-tutorial/ic784369.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="20d8b-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="20d8b-247">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="20d8b-247">Click **New User**.</span></span>
   
   <span data-ttu-id="20d8b-248">![所有使用者](./media/active-directory-saas-jobscience-tutorial/ic784370.png "所有使用者")</span><span class="sxs-lookup"><span data-stu-id="20d8b-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="20d8b-249">在 [編輯使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="20d8b-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="20d8b-250">![使用者編輯](./media/active-directory-saas-jobscience-tutorial/ic784371.png "使用者編輯")</span><span class="sxs-lookup"><span data-stu-id="20d8b-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="20d8b-251">a.</span><span class="sxs-lookup"><span data-stu-id="20d8b-251">a.</span></span> <span data-ttu-id="20d8b-252">在 [名字] 文字方塊中，輸入使用者的名字，例如 Britta。</span><span class="sxs-lookup"><span data-stu-id="20d8b-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="20d8b-253">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="20d8b-253">b.</span></span> <span data-ttu-id="20d8b-254">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 Simon。</span><span class="sxs-lookup"><span data-stu-id="20d8b-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="20d8b-255">c.</span><span class="sxs-lookup"><span data-stu-id="20d8b-255">c.</span></span> <span data-ttu-id="20d8b-256">在 [別名] 文字方塊中，輸入使用者的別名，例如 brittas。</span><span class="sxs-lookup"><span data-stu-id="20d8b-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="20d8b-257">d.</span><span class="sxs-lookup"><span data-stu-id="20d8b-257">d.</span></span> <span data-ttu-id="20d8b-258">在 [電子郵件] 文字方塊中，輸入像是 Brittasimon@contoso.com 的使用者電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="20d8b-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="20d8b-259">e.</span><span class="sxs-lookup"><span data-stu-id="20d8b-259">e.</span></span> <span data-ttu-id="20d8b-260">在 [使用者名稱] 文字方塊中，輸入使用者的使用者名稱，例如 Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="20d8b-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="20d8b-261">f.</span><span class="sxs-lookup"><span data-stu-id="20d8b-261">f.</span></span> <span data-ttu-id="20d8b-262">在 [暱稱] 文字方塊中，輸入使用者的暱稱，例如 Simon。</span><span class="sxs-lookup"><span data-stu-id="20d8b-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="20d8b-263">g.</span><span class="sxs-lookup"><span data-stu-id="20d8b-263">g.</span></span> <span data-ttu-id="20d8b-264">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="20d8b-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="20d8b-265">Azure Active Directory 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="20d8b-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="20d8b-266">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="20d8b-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="20d8b-267">在本節中，您會將 Jobscience 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="20d8b-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![指派使用者][200] 

<span data-ttu-id="20d8b-269">**若要將 Britta Simon 指派給 Jobscience，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="20d8b-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="20d8b-270">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="20d8b-272">在應用程式清單中，選取 [Jobscience]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-272">In the applications list, select **Jobscience**.</span></span>

    ![設定單一登入](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="20d8b-274">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-274">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="20d8b-276">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="20d8b-276">Click **Add** button.</span></span> <span data-ttu-id="20d8b-277">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="20d8b-279">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="20d8b-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="20d8b-280">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="20d8b-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="20d8b-281">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="20d8b-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="20d8b-282">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="20d8b-282">Testing single sign-on</span></span>

<span data-ttu-id="20d8b-283">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="20d8b-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="20d8b-284">當您在存取面板中按一下 Jobscience 圖格時，應該會自動登入您的 Jobscience 應用程式。</span><span class="sxs-lookup"><span data-stu-id="20d8b-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="20d8b-285">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="20d8b-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="20d8b-286">其他資源</span><span class="sxs-lookup"><span data-stu-id="20d8b-286">Additional resources</span></span>

* [<span data-ttu-id="20d8b-287">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="20d8b-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="20d8b-288">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="20d8b-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

