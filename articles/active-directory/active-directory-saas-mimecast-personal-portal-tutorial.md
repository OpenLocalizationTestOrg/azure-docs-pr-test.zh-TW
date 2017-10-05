---
title: "教學課程：Azure Active Directory 與 Mimecast Personal Portal 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Mimecast Personal Portal 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bf46da35a55608d7e4656c9dd3ad9d5f2253e225
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="e1dc5-103">教學課程：Azure Active Directory 與 Mimecast Personal Portal 整合</span><span class="sxs-lookup"><span data-stu-id="e1dc5-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="e1dc5-104">在本教學課程中，您會了解如何整合 Mimecast Personal Portal 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1dc5-105">Mimecast Personal Portal 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e1dc5-106">您可以在 Azure AD 中控制可存取 Mimecast Personal Portal 的人員</span><span class="sxs-lookup"><span data-stu-id="e1dc5-106">You can control in Azure AD who has access to Mimecast Personal Portal</span></span>
- <span data-ttu-id="e1dc5-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Mimecast Personal Portal (單一登入)</span><span class="sxs-lookup"><span data-stu-id="e1dc5-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e1dc5-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e1dc5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e1dc5-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1dc5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e1dc5-110">Prerequisites</span></span>

<span data-ttu-id="e1dc5-111">若要設定 Azure AD 與 Mimecast Personal Portal 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="e1dc5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e1dc5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1dc5-113">啟用 Mimecast Personal Portal 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e1dc5-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1dc5-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1dc5-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1dc5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1dc5-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1dc5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e1dc5-118">Scenario description</span></span>
<span data-ttu-id="e1dc5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1dc5-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1dc5-121">從資源庫新增 Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="e1dc5-121">Adding Mimecast Personal Portal from the gallery</span></span>
2. <span data-ttu-id="e1dc5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e1dc5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="e1dc5-123">從資源庫新增 Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="e1dc5-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="e1dc5-124">若要設定將 Mimecast Personal Portal 整合到 Azure AD 中，您需要從資源庫將 Mimecast Personal Portal 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e1dc5-125">**若要從資源庫新增 Mimecast Personal Portal，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e1dc5-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e1dc5-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e1dc5-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e1dc5-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e1dc5-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e1dc5-133">在搜尋方塊中，輸入 **Mimecast Personal Portal**。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-133">In the search box, type **Mimecast Personal Portal**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="e1dc5-135">在結果面板中，選取 [Mimecast Personal Portal]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-135">In the results panel, select **Mimecast Personal Portal**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e1dc5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e1dc5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e1dc5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Mimecast Personal Portal 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1dc5-139">若要讓單一登入運作，Azure AD 必須知道 Mimecast Personal Portal 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="e1dc5-140">換句話說，必須在 Azure AD 使用者和 Mimecast Personal Portal 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-140">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="e1dc5-141">在 Mimecast Personal Portal 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-141">In Mimecast Personal Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e1dc5-142">若要設定及測試與 Mimecast Personal Portal 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-142">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e1dc5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e1dc5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1dc5-145">**[建立 Mimecast Personal Portal 測試使用者](#creating-a-mimecast-personal-portal-test-user)** - 使 Mimecast Personal Portal 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1dc5-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1dc5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e1dc5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e1dc5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e1dc5-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Mimecast Personal Portal 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="e1dc5-150">**若要設定與 Mimecast Personal Portal 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e1dc5-150">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="e1dc5-151">在 Azure 入口網站的 [Mimecast Personal Portal] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-151">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e1dc5-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="e1dc5-155">在 [Mimecast Personal Portal 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-155">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="e1dc5-157">a.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-157">a.</span></span> <span data-ttu-id="e1dc5-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="e1dc5-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="e1dc5-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-159">b.</span></span> <span data-ttu-id="e1dc5-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="e1dc5-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-161">These values are not real.</span></span> <span data-ttu-id="e1dc5-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e1dc5-163">請連絡 [Mimecast Personal Portal 客戶支援小組](https://www.mimecast.com/customer-success/technical-support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) to get these values.</span></span> 
 


4. <span data-ttu-id="e1dc5-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="e1dc5-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e1dc5-168">在 [Mimecast Personal Portal 組態] 區段上，按一下 [設定 Mimecast Personal Portal 入口網站] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-168">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e1dc5-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="e1dc5-171">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Mimecast Personal Portal 公司網站。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="e1dc5-172">移至 [服務] \> [應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-172">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="e1dc5-173">![應用程式](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="e1dc5-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="e1dc5-174">按一下 [驗證設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="e1dc5-175">![驗證設定檔](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="e1dc5-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="e1dc5-176">按一下 [新驗證設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="e1dc5-177">![新驗證設定檔](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "新驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="e1dc5-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="e1dc5-178">在 [驗證設定檔]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-178">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e1dc5-179">![驗證設定檔](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="e1dc5-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="e1dc5-180">a.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-180">a.</span></span> <span data-ttu-id="e1dc5-181">在 [描述]  文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-181">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="e1dc5-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-182">b.</span></span> <span data-ttu-id="e1dc5-183">選取 [強制執行 Mimecast Personal Portal 的 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="e1dc5-184">c.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-184">c.</span></span> <span data-ttu-id="e1dc5-185">在 [提供者] 中選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="e1dc5-186">d.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-186">d.</span></span> <span data-ttu-id="e1dc5-187">在 [簽發者 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-187">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e1dc5-188">e.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-188">e.</span></span> <span data-ttu-id="e1dc5-189">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-189">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e1dc5-190">f.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-190">f.</span></span> <span data-ttu-id="e1dc5-191">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-191">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e1dc5-192">g.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-192">g.</span></span> <span data-ttu-id="e1dc5-193">在記事本中，開啟您從 Azure 入口網站下載的 **base-64** 編碼憑證，將其內容複製到剪貼簿，然後貼到 [識別提供者憑證]\(中繼資料\) 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="e1dc5-194">h.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-194">h.</span></span> <span data-ttu-id="e1dc5-195">選取 [允許單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="e1dc5-196">i.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-196">i.</span></span> <span data-ttu-id="e1dc5-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e1dc5-198">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="e1dc5-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e1dc5-199">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e1dc5-200">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1dc5-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e1dc5-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e1dc5-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="e1dc5-202">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e1dc5-204">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e1dc5-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e1dc5-205">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e1dc5-207">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e1dc5-209">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e1dc5-211">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e1dc5-213">a.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-213">a.</span></span> <span data-ttu-id="e1dc5-214">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1dc5-215">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-215">b.</span></span> <span data-ttu-id="e1dc5-216">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e1dc5-217">c.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-217">c.</span></span> <span data-ttu-id="e1dc5-218">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e1dc5-219">d.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-219">d.</span></span> <span data-ttu-id="e1dc5-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="e1dc5-221">建立 Mimecast Personal Portal 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e1dc5-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="e1dc5-222">若要讓 Azure AD 使用者能夠登入 Mimecast Personal Portal，必須將它們佈建到 Mimecast Personal Portal。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-222">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="e1dc5-223">Mimecast Personal Portal 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-223">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="e1dc5-224">您需要先註冊網域才能建立使用者。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-224">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="e1dc5-225">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e1dc5-225">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="e1dc5-226">以系統管理員身份登入您的 **Mimecast Personal Portal** 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-226">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="e1dc5-227">移至 [目錄 \> 內部]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-227">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="e1dc5-228">![目錄](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "目錄")</span><span class="sxs-lookup"><span data-stu-id="e1dc5-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="e1dc5-229">按一下 [註冊新網域] 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="e1dc5-230">![註冊新網域](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "註冊新網域")</span><span class="sxs-lookup"><span data-stu-id="e1dc5-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="e1dc5-231">在您建立好新網域之後，，按一下 [新位址] 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="e1dc5-232">![新位址](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "新位址")</span><span class="sxs-lookup"><span data-stu-id="e1dc5-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="e1dc5-233">在 [新位址] 對話方塊中，針對您想要佈建的有效 Azure AD 帳戶，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e1dc5-233">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="e1dc5-234">![儲存](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "儲存")</span><span class="sxs-lookup"><span data-stu-id="e1dc5-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="e1dc5-235">a.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-235">a.</span></span> <span data-ttu-id="e1dc5-236">在 [電子郵件地址] 文字方塊中，輸入使用者的**電子郵件地址**：**BrittaSimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-236">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="e1dc5-237">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-237">b.</span></span> <span data-ttu-id="e1dc5-238">在 [全域名稱] 文字方塊中，輸入**使用者名稱**：**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-238">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="e1dc5-239">c.</span><span class="sxs-lookup"><span data-stu-id="e1dc5-239">c.</span></span> <span data-ttu-id="e1dc5-240">在 [密碼] 和 [確認密碼] 文字方塊中，輸入使用者的**密碼**。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-240">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="e1dc5-241">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-241">b.</span></span> <span data-ttu-id="e1dc5-242">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="e1dc5-243">您可以使用任何其他的 Mimecast Personal Portal 使用者帳戶建立工具，或 Mimecast Personal Portal 提供的 API，以佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e1dc5-244">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e1dc5-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e1dc5-245">在本節中，您會將 Mimecast Personal Portal 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![指派使用者][200] 

<span data-ttu-id="e1dc5-247">**若要將 Britta Simon 指派給 Mimecast Personal Portal，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e1dc5-247">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="e1dc5-248">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e1dc5-250">在應用程式清單中，選取 [Mimecast Personal Portal]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-250">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![設定單一登入](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="e1dc5-252">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-252">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e1dc5-254">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-254">Click **Add** button.</span></span> <span data-ttu-id="e1dc5-255">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e1dc5-257">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e1dc5-258">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1dc5-259">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e1dc5-260">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e1dc5-260">Testing single sign-on</span></span>
<span data-ttu-id="e1dc5-261">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e1dc5-262">當您在存取面板中按一下 Mimecast Personal Portal 圖格時，應該會自動登入您的 Mimecast Personal Portal 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-262">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span> <span data-ttu-id="e1dc5-263">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e1dc5-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1dc5-264">其他資源</span><span class="sxs-lookup"><span data-stu-id="e1dc5-264">Additional resources</span></span>

* [<span data-ttu-id="e1dc5-265">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e1dc5-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1dc5-266">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e1dc5-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

