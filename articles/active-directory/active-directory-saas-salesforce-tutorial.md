---
title: "教學課程：Azure Active Directory 與 Salesforce 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Salesforce 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="f93d3-103">教學課程：Azure Active Directory 與 Salesforce 整合</span><span class="sxs-lookup"><span data-stu-id="f93d3-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="f93d3-104">在本教學課程中，您會了解如何整合 Salesforce 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f93d3-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f93d3-105">Salesforce 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f93d3-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f93d3-106">您可以在 Azure AD 中控制可存取 Salesforce 的人員</span><span class="sxs-lookup"><span data-stu-id="f93d3-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="f93d3-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Salesforce (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f93d3-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f93d3-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f93d3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f93d3-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f93d3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f93d3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f93d3-110">Prerequisites</span></span>

<span data-ttu-id="f93d3-111">若要設定 Azure AD 與 Salesforce 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f93d3-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="f93d3-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f93d3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f93d3-113">啟用 Salesforce 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f93d3-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f93d3-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f93d3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f93d3-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f93d3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f93d3-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f93d3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f93d3-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f93d3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f93d3-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f93d3-118">Scenario description</span></span>
<span data-ttu-id="f93d3-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f93d3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f93d3-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f93d3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f93d3-121">從資源庫新增 Salesforce</span><span class="sxs-lookup"><span data-stu-id="f93d3-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="f93d3-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f93d3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="f93d3-123">從資源庫新增 Salesforce</span><span class="sxs-lookup"><span data-stu-id="f93d3-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="f93d3-124">若要設定 Salesforce 與 Azure AD 的整合作業，您必須從資源庫將 Salesforce 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="f93d3-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f93d3-125">**若要從資源庫新增 Salesforce，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f93d3-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f93d3-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f93d3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f93d3-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f93d3-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f93d3-131">按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f93d3-131">Click **New application** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f93d3-133">在 [搜尋方塊] 中，輸入 [Salesforce]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-133">In the search box, type **Salesforce**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="f93d3-135">在結果窗格中，選取 [Salesforce]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f93d3-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f93d3-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f93d3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f93d3-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Salesforce 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f93d3-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f93d3-139">若要讓單一登入運作，Azure AD 必須知道 Salesforce 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f93d3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="f93d3-140">換句話說，必須在 Azure AD 使用者和 Salesforce 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f93d3-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="f93d3-141">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 Salesforce 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="f93d3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="f93d3-142">若要設定及測試與 Salesforce 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="f93d3-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f93d3-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f93d3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f93d3-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f93d3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f93d3-145">**[建立 Salesforce 測試使用者](#creating-a-salesforce-test-user)** - 使 Salesforce 中 Britta Simon 的對應身分連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="f93d3-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f93d3-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f93d3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f93d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f93d3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f93d3-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f93d3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f93d3-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Salesforce 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f93d3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="f93d3-150">**若要使用 Salesforce 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f93d3-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="f93d3-151">在 Azure 入口網站的 [Salesforce] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f93d3-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f93d3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="f93d3-155">在 [Salesforce 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f93d3-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="f93d3-157">在 [登入 URL] 文字方塊中，以下列模式輸入值：</span><span class="sxs-lookup"><span data-stu-id="f93d3-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="f93d3-158">企業帳戶： `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f93d3-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="f93d3-159">開發人員帳戶： `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f93d3-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f93d3-160">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f93d3-160">These values are not the real.</span></span> <span data-ttu-id="f93d3-161">使用實際的「登入 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="f93d3-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="f93d3-162">請連絡 [Salesforce 用戶端支援小組](https://help.salesforce.com/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="f93d3-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="f93d3-163">在 [SAML 簽署憑證] 區段上，按一下 [憑證]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f93d3-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="f93d3-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f93d3-165">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f93d3-167">在 [Salesforce 組態] 區段上，按一下 [設定 Salesforce] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f93d3-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f93d3-168">從 [快速參考] 區段中複製 [SAML 實體 ID 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="f93d3-169">![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="f93d3-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="f93d3-170">在瀏覽器中開啟新索引標籤，登入您的 Salesforce 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="f93d3-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="f93d3-171">在 [系統管理員] 瀏覽窗格下，按一下 [安全性控制] 展開相關的區段。</span><span class="sxs-lookup"><span data-stu-id="f93d3-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="f93d3-172">然後按一下 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-172">Then click **Single Sign-On Settings**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="f93d3-174">在 [單一登入設定] 頁面上，按一下 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f93d3-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="f93d3-175">![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="f93d3-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="f93d3-176">如果您的 Salesforce 帳戶無法啟用單一登入設定，您可能需要連絡 [Salesforce 用戶端支援小組](https://help.salesforce.com/support)。</span><span class="sxs-lookup"><span data-stu-id="f93d3-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="f93d3-177">選取 [啟用 SAML]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="f93d3-179">若要設定 SAML 單一登入設定，請按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f93d3-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="f93d3-181">在 [SAML 單一登入設定編輯]  頁面上，進行下列設定：</span><span class="sxs-lookup"><span data-stu-id="f93d3-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="f93d3-183">a.</span><span class="sxs-lookup"><span data-stu-id="f93d3-183">a.</span></span> <span data-ttu-id="f93d3-184">在 [名稱]  欄位中，為此組態輸入易記的名稱。</span><span class="sxs-lookup"><span data-stu-id="f93d3-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="f93d3-185">提供 [名稱] 的值會自動填入 [API 名稱] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="f93d3-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="f93d3-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f93d3-186">b.</span></span> <span data-ttu-id="f93d3-187">將 [SMAL 實體識別碼] 的值貼到 Salesforce 中的 [簽發者] 欄位。</span><span class="sxs-lookup"><span data-stu-id="f93d3-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="f93d3-188">c.</span><span class="sxs-lookup"><span data-stu-id="f93d3-188">c.</span></span> <span data-ttu-id="f93d3-189">在 [實體識別碼] 文字方塊中，使用下列形式輸入您的 Salesforce 網域名稱：</span><span class="sxs-lookup"><span data-stu-id="f93d3-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="f93d3-190">企業帳戶： `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f93d3-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="f93d3-191">開發人員帳戶： `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="f93d3-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="f93d3-192">d.</span><span class="sxs-lookup"><span data-stu-id="f93d3-192">d.</span></span> <span data-ttu-id="f93d3-193">按一下 [瀏覽] 或 [選擇檔案] 開啟 [選擇要上傳的檔案] 對話方塊，選取您的 Salesforce 憑證，然後按一下 [開啟] 上傳憑證。</span><span class="sxs-lookup"><span data-stu-id="f93d3-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="f93d3-194">e.</span><span class="sxs-lookup"><span data-stu-id="f93d3-194">e.</span></span> <span data-ttu-id="f93d3-195">對於 [SAML 身分識別類型]，請選取 [判斷提示包含使用者的 salesforce.com 使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="f93d3-196">f.</span><span class="sxs-lookup"><span data-stu-id="f93d3-196">f.</span></span> <span data-ttu-id="f93d3-197">對於 [SAML 身分識別位置]，請選取 [身分識別位於 Subject 陳述式的 NameIdentifier 元素中]</span><span class="sxs-lookup"><span data-stu-id="f93d3-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="f93d3-198">g.</span><span class="sxs-lookup"><span data-stu-id="f93d3-198">g.</span></span> <span data-ttu-id="f93d3-199">將 [單一登入服務 URL] 貼到 Salesforce 中的 [識別提供者登入 URL] 欄位。</span><span class="sxs-lookup"><span data-stu-id="f93d3-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="f93d3-200">h.</span><span class="sxs-lookup"><span data-stu-id="f93d3-200">h.</span></span> <span data-ttu-id="f93d3-201">對於 [服務提供者起始的要求繫結]，請選取 [HTTP 重新導向]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="f93d3-202">i.</span><span class="sxs-lookup"><span data-stu-id="f93d3-202">i.</span></span> <span data-ttu-id="f93d3-203">最後，按一下 [儲存]  套用您的 SAML 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="f93d3-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="f93d3-204">在 Salesforce 的左方導覽窗格中，按一下 [網域管理] 展開相關的區段，然後按一下 [我的網域]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="f93d3-206">向下捲動至 [驗證組態] 區段，然後按一下 [編輯] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f93d3-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="f93d3-208">在 [驗證服務] 區段中，選取您 SAML SSO 組態的易記名稱，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="f93d3-210">如果選取了一個以上的驗證服務，當使用者嘗試啟動單一登入到您的 Salesforce 環境時，將會提示使用者選取登入時想要使用的驗證服務。</span><span class="sxs-lookup"><span data-stu-id="f93d3-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="f93d3-211">如果您不想發生這種情形，您應該**不要核取其他所有的驗證服務**。</span><span class="sxs-lookup"><span data-stu-id="f93d3-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="f93d3-212">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="f93d3-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f93d3-213">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="f93d3-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f93d3-214">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f93d3-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f93d3-215">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f93d3-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="f93d3-216">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f93d3-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f93d3-218">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f93d3-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f93d3-219">在 [Azure 入口網站] 的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f93d3-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f93d3-221">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f93d3-223">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f93d3-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f93d3-225">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f93d3-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f93d3-227">a.</span><span class="sxs-lookup"><span data-stu-id="f93d3-227">a.</span></span> <span data-ttu-id="f93d3-228">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f93d3-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f93d3-229">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f93d3-229">b.</span></span> <span data-ttu-id="f93d3-230">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f93d3-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f93d3-231">c.</span><span class="sxs-lookup"><span data-stu-id="f93d3-231">c.</span></span> <span data-ttu-id="f93d3-232">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f93d3-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f93d3-233">d.</span><span class="sxs-lookup"><span data-stu-id="f93d3-233">d.</span></span> <span data-ttu-id="f93d3-234">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f93d3-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="f93d3-235">建立 Salesforce 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f93d3-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="f93d3-236">本節會在 Salesforce 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f93d3-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="f93d3-237">Salesforce 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="f93d3-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="f93d3-238">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="f93d3-238">There is no action item for you in this section.</span></span> <span data-ttu-id="f93d3-239">如果 Salesforce 中還沒有該使用者，當您嘗試存取 Salesforce 時，就會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="f93d3-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f93d3-240">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f93d3-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f93d3-241">在本節中，您會將 Salesforce 的存取權授與 Britta Simon，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f93d3-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![指派使用者][200] 

<span data-ttu-id="f93d3-243">**若要將 Britta Simon 指派給 Salesforce，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f93d3-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="f93d3-244">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f93d3-246">在應用程式清單中，選取 [Salesforce]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-246">In the applications list, select **Salesforce**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="f93d3-248">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-248">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f93d3-250">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f93d3-250">Click **Add** button.</span></span> <span data-ttu-id="f93d3-251">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f93d3-253">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f93d3-254">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f93d3-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f93d3-255">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f93d3-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f93d3-256">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f93d3-256">Testing single sign-on</span></span>

<span data-ttu-id="f93d3-257">若要測試您的單一登入設定，請在 [https://myapps.microsoft.com](https://myapps.microsoft.com/) 開啟 [存取面板]、登入測試帳戶，然後按一下 [Salesforce]。</span><span class="sxs-lookup"><span data-stu-id="f93d3-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f93d3-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="f93d3-258">Additional resources</span></span>

* [<span data-ttu-id="f93d3-259">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f93d3-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f93d3-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f93d3-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f93d3-261">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="f93d3-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

