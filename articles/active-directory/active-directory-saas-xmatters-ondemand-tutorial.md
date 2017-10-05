---
title: "教學課程：Azure Active Directory 與 xMatters OnDemand 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 xMatters OnDemand 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9bfcb44ed19f167872b3cd9119e2dbdd35c82604
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="950ce-103">教學課程：Azure Active Directory 與 xMatters OnDemand 整合</span><span class="sxs-lookup"><span data-stu-id="950ce-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="950ce-104">在本教學課程中，您將了解如何整合 xMatters OnDemand 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="950ce-104">In this tutorial, you learn how to integrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="950ce-105">xMatters OnDemand 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="950ce-105">Integrating xMatters OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="950ce-106">您可以在 Azure AD 中控制可存取 xMatters OnDemand 的人員</span><span class="sxs-lookup"><span data-stu-id="950ce-106">You can control in Azure AD who has access to xMatters OnDemand</span></span>
- <span data-ttu-id="950ce-107">您可以讓使用者利用自己的 Azure AD 帳戶，來自動登入 xMatters OnDemand (單一登入)</span><span class="sxs-lookup"><span data-stu-id="950ce-107">You can enable your users to automatically get signed-on to xMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="950ce-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="950ce-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="950ce-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="950ce-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="950ce-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="950ce-110">Prerequisites</span></span>

<span data-ttu-id="950ce-111">若要設定 Azure AD 與 xMatters OnDemand 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="950ce-111">To configure Azure AD integration with xMatters OnDemand, you need the following items:</span></span>

- <span data-ttu-id="950ce-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="950ce-112">An Azure AD subscription</span></span>
- <span data-ttu-id="950ce-113">已啟用 xMatters OnDemand 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="950ce-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="950ce-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="950ce-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="950ce-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="950ce-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="950ce-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="950ce-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="950ce-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="950ce-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="950ce-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="950ce-118">Scenario description</span></span>
<span data-ttu-id="950ce-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="950ce-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="950ce-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="950ce-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="950ce-121">從資源庫新增 xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="950ce-121">Adding xMatters OnDemand from the gallery</span></span>
2. <span data-ttu-id="950ce-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="950ce-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-the-gallery"></a><span data-ttu-id="950ce-123">從資源庫新增 xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="950ce-123">Adding xMatters OnDemand from the gallery</span></span>
<span data-ttu-id="950ce-124">若要設定將 xMatters OnDemand 整合到 Azure AD 中，您需要從資源庫將 xMatters OnDemand 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="950ce-124">To configure the integration of xMatters OnDemand into Azure AD, you need to add xMatters OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="950ce-125">**若要從資源庫新增 xMatters OnDemand，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="950ce-125">**To add xMatters OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="950ce-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="950ce-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="950ce-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="950ce-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="950ce-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="950ce-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="950ce-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="950ce-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="950ce-133">在搜尋方塊中，輸入 **xMatters OnDemand**。</span><span class="sxs-lookup"><span data-stu-id="950ce-133">In the search box, type **xMatters OnDemand**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="950ce-135">在結果窗格中，選取 [xMatters OnDemand]，然後按一下 [新增] 按鈕來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="950ce-135">In the results panel, select **xMatters OnDemand**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="950ce-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="950ce-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="950ce-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 xMatters OnDemand 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="950ce-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="950ce-139">若要讓單一登入運作，Azure AD 必須知道 xMatters OnDemand 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="950ce-139">For single sign-on to work, Azure AD needs to know what the counterpart user in xMatters OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="950ce-140">換句話說，必須建立 Azure AD 使用者和 xMatters OnDemand 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="950ce-140">In other words, a link relationship between an Azure AD user and the related user in xMatters OnDemand needs to be established.</span></span>

<span data-ttu-id="950ce-141">在 xMatters OnDemand 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="950ce-141">In xMatters OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="950ce-142">若要設定及測試與 xMatters OnDemand 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="950ce-142">To configure and test Azure AD single sign-on with xMatters OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="950ce-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="950ce-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="950ce-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="950ce-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="950ce-145">**[建立 xMatters OnDemand 測試使用者](#creating-a-xmatters-ondemand-test-user)** - 在 xMatters OnDemand 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="950ce-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - to have a counterpart of Britta Simon in xMatters OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="950ce-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="950ce-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="950ce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="950ce-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="950ce-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="950ce-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="950ce-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 xMatters OnDemand 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="950ce-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="950ce-150">**若要使用 xMatters OnDemand 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="950ce-150">**To configure Azure AD single sign-on with xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="950ce-151">在 Azure 入口網站的 [xMatters OnDemand] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="950ce-151">In the Azure portal, on the **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="950ce-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="950ce-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="950ce-155">在 [xMatters OnDemand 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="950ce-155">On the **xMatters OnDemand Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="950ce-157">a.</span><span class="sxs-lookup"><span data-stu-id="950ce-157">a.</span></span> <span data-ttu-id="950ce-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="950ce-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="950ce-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="950ce-159">b.</span></span> <span data-ttu-id="950ce-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="950ce-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="950ce-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="950ce-161">These values are not real.</span></span> <span data-ttu-id="950ce-162">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="950ce-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="950ce-163">請連絡 [xMatters OnDemand 支援小組](https://www.xmatters.com/company/contact-us/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="950ce-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="950ce-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證]\(Base64\)，然後將憑證檔案儲存在本機 **c:\\XMatters OnDemand.cer**。</span><span class="sxs-lookup"><span data-stu-id="950ce-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="950ce-166">您需要將憑證轉送給 [xMatters OnDemand 支援小組](https://www.xmatters.com/company/contact-us/)。</span><span class="sxs-lookup"><span data-stu-id="950ce-166">You need to forward the certificate to the [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="950ce-167">xMatters 支援小組需要先上傳憑證，您才能完成單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="950ce-167">The certificate needs to be uploaded by the xMatters support team before you can finalize the single sign-on configuration.</span></span> 

5. <span data-ttu-id="950ce-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="950ce-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="950ce-170">在 [xMatters OnDemand 設定] 區段中，按一下 [設定 xMatters OnDemand] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="950ce-170">On the **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="950ce-171">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="950ce-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="950ce-173">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 xMatters OnDemand 公司網站。</span><span class="sxs-lookup"><span data-stu-id="950ce-173">In a different web browser window, log in to your XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="950ce-174">在頂端工具列中按一下 [管理]，然後按一下左側導覽列中的 [公司詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="950ce-174">In the toolbar on the top, click **Admin**, and then click **Company Details** in the navigation bar on the left side.</span></span>
   
    <span data-ttu-id="950ce-175">![管理](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "管理")</span><span class="sxs-lookup"><span data-stu-id="950ce-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="950ce-176">在 [SAML 組態]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="950ce-176">On the **SAML Configuration** page, perform the following steps:</span></span>
   
    <span data-ttu-id="950ce-177">![SAML 組態](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML 組態")</span><span class="sxs-lookup"><span data-stu-id="950ce-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="950ce-178">a.</span><span class="sxs-lookup"><span data-stu-id="950ce-178">a.</span></span> <span data-ttu-id="950ce-179">選取 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="950ce-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="950ce-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="950ce-180">b.</span></span> <span data-ttu-id="950ce-181">將您從 Azure 入口網站複製的「SAML 實體識別碼」貼到 [識別提供者識別碼] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="950ce-181">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="950ce-182">c.</span><span class="sxs-lookup"><span data-stu-id="950ce-182">c.</span></span> <span data-ttu-id="950ce-183">將您從 Azure 入口網站複製的「SAML 單一登入服務 URL」貼到 [單一登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="950ce-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="950ce-184">d.</span><span class="sxs-lookup"><span data-stu-id="950ce-184">d.</span></span> <span data-ttu-id="950ce-185">將您從 Azure 入口網站複製的「登出 URL」貼到 [單一登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="950ce-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="950ce-186">e.</span><span class="sxs-lookup"><span data-stu-id="950ce-186">e.</span></span> <span data-ttu-id="950ce-187">在 [公司詳細資料] 頁面頂端，按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="950ce-187">On the Company Details page, at the top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="950ce-188">![公司詳細資料](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "公司詳細資料")</span><span class="sxs-lookup"><span data-stu-id="950ce-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="950ce-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="950ce-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="950ce-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="950ce-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="950ce-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="950ce-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="950ce-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="950ce-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="950ce-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="950ce-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="950ce-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="950ce-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="950ce-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="950ce-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="950ce-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="950ce-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="950ce-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="950ce-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="950ce-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="950ce-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="950ce-204">a.</span><span class="sxs-lookup"><span data-stu-id="950ce-204">a.</span></span> <span data-ttu-id="950ce-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="950ce-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="950ce-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="950ce-206">b.</span></span> <span data-ttu-id="950ce-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="950ce-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="950ce-208">c.</span><span class="sxs-lookup"><span data-stu-id="950ce-208">c.</span></span> <span data-ttu-id="950ce-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="950ce-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="950ce-210">d.</span><span class="sxs-lookup"><span data-stu-id="950ce-210">d.</span></span> <span data-ttu-id="950ce-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="950ce-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="950ce-212">建立 xMatters OnDemand 測試使用者</span><span class="sxs-lookup"><span data-stu-id="950ce-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="950ce-213">若要讓 Azure AD 使用者可以登入 xMatters OnDemand，則必須將他們佈建到 xMatters OnDemand。</span><span class="sxs-lookup"><span data-stu-id="950ce-213">In order to enable Azure AD users to log in to XMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="950ce-214">xMatters OnDemand 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="950ce-214">In the case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="950ce-215">若要佈建使用者帳戶，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="950ce-215">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="950ce-216">登入 **xMatters OnDemand** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="950ce-216">Log in to your **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="950ce-217">按一下 [使用者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="950ce-217">Click **Users** tab.</span></span> <span data-ttu-id="950ce-218">然後按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="950ce-218">and then click **Add User**.</span></span>
  
    <span data-ttu-id="950ce-219">![使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="950ce-219">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="950ce-220">在 [加入使用者]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="950ce-220">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="950ce-221">![加入使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "加入使用者")</span><span class="sxs-lookup"><span data-stu-id="950ce-221">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="950ce-222">a.</span><span class="sxs-lookup"><span data-stu-id="950ce-222">a.</span></span> <span data-ttu-id="950ce-223">選取 [使用中] 。</span><span class="sxs-lookup"><span data-stu-id="950ce-223">Select **Active**.</span></span>

    <span data-ttu-id="950ce-224">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="950ce-224">b.</span></span> <span data-ttu-id="950ce-225">在 [使用者識別碼] 文字方塊中，輸入使用者的使用者識別碼，例如 Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="950ce-225">In the **User ID** textbox, type the user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="950ce-226">c.</span><span class="sxs-lookup"><span data-stu-id="950ce-226">c.</span></span> <span data-ttu-id="950ce-227">在 [名字] 文字方塊中，輸入使用者的名字，例如 Britta。</span><span class="sxs-lookup"><span data-stu-id="950ce-227">In the **First Name** textbox, type first name of the user like Britta.</span></span>

    <span data-ttu-id="950ce-228">d.</span><span class="sxs-lookup"><span data-stu-id="950ce-228">d.</span></span> <span data-ttu-id="950ce-229">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 Simon。</span><span class="sxs-lookup"><span data-stu-id="950ce-229">In the **Last Name** textbox, type last name of the user like Simon.</span></span>
    
    <span data-ttu-id="950ce-230">e.</span><span class="sxs-lookup"><span data-stu-id="950ce-230">e.</span></span> <span data-ttu-id="950ce-231">在 [網站] 文字方塊中，輸入您想要佈建之有效 Azure AD 帳戶的有效網站。</span><span class="sxs-lookup"><span data-stu-id="950ce-231">In the **Site** textbox, Enter the valid site of a valid Azure AD account you want to provision.</span></span>
    
    <span data-ttu-id="950ce-232">f.</span><span class="sxs-lookup"><span data-stu-id="950ce-232">f.</span></span> <span data-ttu-id="950ce-233">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="950ce-233">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="950ce-234">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="950ce-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="950ce-235">在本節中，您會將 xMatters OnDemand 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="950ce-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to xMatters OnDemand.</span></span>

![指派使用者][200] 

<span data-ttu-id="950ce-237">**若要將 Britta Simon 指派給 xMatters OnDemand，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="950ce-237">**To assign Britta Simon to xMatters OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="950ce-238">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="950ce-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="950ce-240">在應用程式清單中，選取 **xMatters OnDemand**。</span><span class="sxs-lookup"><span data-stu-id="950ce-240">In the applications list, select **xMatters OnDemand**.</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="950ce-242">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="950ce-242">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="950ce-244">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="950ce-244">Click **Add** button.</span></span> <span data-ttu-id="950ce-245">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="950ce-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="950ce-247">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="950ce-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="950ce-248">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="950ce-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="950ce-249">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="950ce-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="950ce-250">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="950ce-250">Testing single sign-on</span></span>

<span data-ttu-id="950ce-251">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="950ce-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="950ce-252">當您在存取面板中按一下 [xMatters OnDemand] 圖格時，應該會自動登入您的 xMatters OnDemand 應用程式。</span><span class="sxs-lookup"><span data-stu-id="950ce-252">When you click the xMatters OnDemand tile in the Access Panel, you should get automatically signed-on to your xMatters OnDemand application.</span></span>
<span data-ttu-id="950ce-253">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="950ce-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="950ce-254">其他資源</span><span class="sxs-lookup"><span data-stu-id="950ce-254">Additional resources</span></span>

* [<span data-ttu-id="950ce-255">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="950ce-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="950ce-256">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="950ce-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

