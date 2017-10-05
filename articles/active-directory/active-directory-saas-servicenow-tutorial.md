---
title: "教學課程：Azure Active Directory 與 ServiceNow 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ServiceNow 和 ServiceNow Express 之間的單一登入。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: a91fab90a94b655b93c8ae9064ea4836b80d7678
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="5722b-103">教學課程：Azure Active Directory 與 ServiceNow 整合</span><span class="sxs-lookup"><span data-stu-id="5722b-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="5722b-104">在本教學課程中，您會了解如何整合 ServiceNow and ServiceNow Express 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5722b-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5722b-105">ServiceNow 和 ServiceNow Express 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="5722b-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="5722b-106">您可以在 Azure AD 中控制可存取 ServiceNow 和 ServiceNow Express 的人員</span><span class="sxs-lookup"><span data-stu-id="5722b-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="5722b-107">您可以讓您的使用者使用他們的 Azure AD 帳戶自動登入 ServiceNow 和 ServiceNow Express (單一登入)</span><span class="sxs-lookup"><span data-stu-id="5722b-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="5722b-108">您可以在 Azure 傳統入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5722b-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="5722b-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5722b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5722b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5722b-110">Prerequisites</span></span>
<span data-ttu-id="5722b-111">若要設定 Azure AD 與 ServiceNow 和 ServiceNow Express 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5722b-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="5722b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5722b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="5722b-113">若為 ServiceNow，ServiceNow 的執行個體或租用戶 (Calgary 版本或更新版本)</span><span class="sxs-lookup"><span data-stu-id="5722b-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="5722b-114">若為 ServiceNow Express，ServiceNow Express 的執行個體 (Helsinki 版本或更新版本)</span><span class="sxs-lookup"><span data-stu-id="5722b-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="5722b-115">ServiceNow 租用戶必須啟用[多個提供者單一登入外掛程式](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0)。</span><span class="sxs-lookup"><span data-stu-id="5722b-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="5722b-116">[提交服務要求](https://hi.service-now.com)即可達到此目的。</span><span class="sxs-lookup"><span data-stu-id="5722b-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="5722b-117">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5722b-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="5722b-118">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5722b-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="5722b-119">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="5722b-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="5722b-120">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5722b-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5722b-121">案例描述</span><span class="sxs-lookup"><span data-stu-id="5722b-121">Scenario description</span></span>
<span data-ttu-id="5722b-122">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5722b-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5722b-123">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5722b-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5722b-124">從資源庫新增 ServiceNow</span><span class="sxs-lookup"><span data-stu-id="5722b-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="5722b-125">為 ServiceNow 或 ServiceNow Express 設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5722b-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="5722b-126">從資源庫新增 ServiceNow</span><span class="sxs-lookup"><span data-stu-id="5722b-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="5722b-127">若要設定 ServiceNow 或 ServiceNow Express 與 Azure AD 整合，您需要從資源庫將 ServiceNow 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="5722b-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="5722b-128">**若要從資源庫新增 ServiceNow，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5722b-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5722b-129">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="5722b-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="5722b-131">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="5722b-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5722b-132">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="5722b-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![應用程式][2]
4. <span data-ttu-id="5722b-134">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="5722b-134">Click **Add** at the bottom of the page.</span></span>
   
    ![應用程式][3]
5. <span data-ttu-id="5722b-136">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5722b-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![應用程式][4]
6. <span data-ttu-id="5722b-138">在搜尋方塊中，輸入 **ServiceNow**。</span><span class="sxs-lookup"><span data-stu-id="5722b-138">In the search box, type **ServiceNow**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="5722b-140">在結果窗格中，選取 [ServiceNow]，然後按一下 [完成] 來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="5722b-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5722b-142">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5722b-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5722b-143">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試透過 ServiceNow 或 ServiceNow Express 使用 Azure AD 單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="5722b-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5722b-144">若要讓單一登入運作，Azure AD 必須知道 ServiceNow 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="5722b-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="5722b-145">換句話說，必須在 Azure AD 使用者和 ServiceNow 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5722b-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="5722b-146">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指派為 ServiceNow 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="5722b-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="5722b-147">若要設定及測試透過 ServiceNow 使用 Azure AD 單一登入功能，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5722b-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5722b-148">**[針對 ServiceNow 設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on-for-servicenow)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5722b-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5722b-149">**[針對 ServiceNow Express 設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5722b-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="5722b-150">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5722b-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="5722b-151">**[建立 ServiceNow 測試使用者](#creating-a-servicenow-test-user)** - 使 ServiceNow 中 Britta Simon 的對應使用者連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="5722b-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="5722b-152">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5722b-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="5722b-153">**[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5722b-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="5722b-154">如果您想要設定 ServiceNow，請略過步驟 2。</span><span class="sxs-lookup"><span data-stu-id="5722b-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="5722b-155">同樣地，如果您想要設定 ServiceNow Express，請略過步驟 1。</span><span class="sxs-lookup"><span data-stu-id="5722b-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="5722b-156">為 ServiceNow 設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5722b-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="5722b-157">在 Azure AD 傳統入口網站的 [ServiceNow] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5722b-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="5722b-158">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749323.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="5722b-159">在 [您希望使用者如何登入 ServiceNow] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5722b-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="5722b-160">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749324.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="5722b-161">在 [設定應用程式設定]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="5722b-162">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="5722b-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="5722b-163">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-163">a.</span></span> <span data-ttu-id="5722b-164">在 [ServiceNow 登入 URL] 文字方塊中，使用下列模式輸入使用者用來登入 ServiceNow 應用程式的 URL：`https://<instance-name>.service-now.com`。</span><span class="sxs-lookup"><span data-stu-id="5722b-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="5722b-165">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-165">b.</span></span> <span data-ttu-id="5722b-166">在 [識別碼] 文字方塊中，使用下列模式輸入使用者用來登入 ServiceNow 應用程式的 URL：`https://<instance-name>.service-now.com`。</span><span class="sxs-lookup"><span data-stu-id="5722b-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="5722b-167">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-167">c.</span></span> <span data-ttu-id="5722b-168">按一下 [下一步] </span><span class="sxs-lookup"><span data-stu-id="5722b-168">Click **Next**</span></span>

4. <span data-ttu-id="5722b-169">若要讓 Azure AD 自動設定 ServiceNow 以便進行 SAML 型驗證，請在 [自動設定單一登入] 表單上輸入您的 ServiceNow 執行個體名稱、系統管理員使用者名稱和系統管理員密碼，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="5722b-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="5722b-170">請注意，提供的系統管理員使用者名稱必須在 ServiceNow 中指派 **security_admin** 角色，才能運作。</span><span class="sxs-lookup"><span data-stu-id="5722b-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="5722b-171">否則，若要手動設定 ServiceNow 以使用 Azure AD 做為 SAML 識別提供者，請按一下 [手動設定應用程式以進行單一登入]，然後按 [下一步] 並完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="5722b-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="5722b-172">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="5722b-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="5722b-173">在 [在 ServiceNow 設定單一登入] 頁面上，按一下 [下載憑證]，然後在本機電腦上儲存憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="5722b-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="5722b-174">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749325.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="5722b-175">以系統管理員身分登入您的 ServiceNow 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5722b-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="5722b-176">遵循下一個步驟，啟動 [整合 - 多個提供者單一登入安裝程式] 外掛程式︰</span><span class="sxs-lookup"><span data-stu-id="5722b-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="5722b-177">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-177">a.</span></span> <span data-ttu-id="5722b-178">在左側導覽窗格中，移至 [系統定義] 區段，然後按一下 [外掛程式]。</span><span class="sxs-lookup"><span data-stu-id="5722b-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="5722b-179">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "啟動外掛程式")</span><span class="sxs-lookup"><span data-stu-id="5722b-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="5722b-180">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-180">b.</span></span> <span data-ttu-id="5722b-181">搜尋*整合 - 多個提供者單一登入安裝程式*。</span><span class="sxs-lookup"><span data-stu-id="5722b-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="5722b-182">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "啟動外掛程式")</span><span class="sxs-lookup"><span data-stu-id="5722b-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="5722b-183">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-183">c.</span></span> <span data-ttu-id="5722b-184">選取外掛程式。</span><span class="sxs-lookup"><span data-stu-id="5722b-184">Select the plugin.</span></span> <span data-ttu-id="5722b-185">按一下滑鼠右鍵並選取 [啟動/升級]。</span><span class="sxs-lookup"><span data-stu-id="5722b-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="5722b-186">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-186">d.</span></span> <span data-ttu-id="5722b-187">按一下 [啟用] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5722b-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="5722b-188">在左側的導覽窗格中，按一下 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="5722b-189">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="5722b-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="5722b-190">在 [多個提供者 SSO 內容]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="5722b-191">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="5722b-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="5722b-192">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-192">a.</span></span> <span data-ttu-id="5722b-193">針對 [啟用多個提供者 SSO]，選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="5722b-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="5722b-194">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-194">b.</span></span> <span data-ttu-id="5722b-195">針對 [啟用偵錯記錄有多個提供者 SSO 整合]，選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="5722b-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="5722b-196">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-196">c.</span></span> <span data-ttu-id="5722b-197">在 [使用者資料表上的欄位...] 文字方塊中，輸入 **user_name**。</span><span class="sxs-lookup"><span data-stu-id="5722b-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="5722b-198">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-198">d.</span></span> <span data-ttu-id="5722b-199">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-199">Click **Save**.</span></span>

10. <span data-ttu-id="5722b-200">在左側的導覽窗格中，按一下 [x509 憑證] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="5722b-201">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="5722b-202">在 [X.509 憑證] 對話方塊中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5722b-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="5722b-203">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="5722b-204">在 [X.509 憑證]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="5722b-205">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="5722b-206">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-206">a.</span></span> <span data-ttu-id="5722b-207">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-207">Click **New**.</span></span>
    
     <span data-ttu-id="5722b-208">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-208">b.</span></span> <span data-ttu-id="5722b-209">在 [名稱] 文字方塊中，輸入您的設定名稱 (例如：**TestSAML2.0**)。</span><span class="sxs-lookup"><span data-stu-id="5722b-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="5722b-210">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-210">c.</span></span> <span data-ttu-id="5722b-211">選取 [使用中] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-211">Select **Active**.</span></span>
    
     <span data-ttu-id="5722b-212">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-212">d.</span></span> <span data-ttu-id="5722b-213">針對 [格式]，選取 [PEM]。</span><span class="sxs-lookup"><span data-stu-id="5722b-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="5722b-214">e.</span><span class="sxs-lookup"><span data-stu-id="5722b-214">e.</span></span> <span data-ttu-id="5722b-215">針對 [類型]，選取 [信任存放區憑證]。</span><span class="sxs-lookup"><span data-stu-id="5722b-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="5722b-216">f.</span><span class="sxs-lookup"><span data-stu-id="5722b-216">f.</span></span> <span data-ttu-id="5722b-217">在記事本中開啟您的 Base64 編碼的憑證，將其內容複製到剪貼簿，然後貼到 [PEM 憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5722b-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="5722b-218">g.</span><span class="sxs-lookup"><span data-stu-id="5722b-218">g.</span></span> <span data-ttu-id="5722b-219">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-219">Click **Update**.</span></span>

13. <span data-ttu-id="5722b-220">在左側的導覽窗格中，按一下 [識別提供者] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="5722b-221">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="5722b-222">在 [身分識別提供者] 對話方塊中，按一下 [新增]：</span><span class="sxs-lookup"><span data-stu-id="5722b-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="5722b-223">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="5722b-224">在 [身分識別提供者] 對話方塊中，按一下 [SAML2 更新 1]：</span><span class="sxs-lookup"><span data-stu-id="5722b-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="5722b-225">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="5722b-226">在 [SAML2 Update1 內容] 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="5722b-227">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="5722b-228">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-228">a.</span></span> <span data-ttu-id="5722b-229">在 [名稱] 文字方塊中，輸入您的設定名稱 (例如：**SAML 2.0**)。</span><span class="sxs-lookup"><span data-stu-id="5722b-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="5722b-230">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-230">b.</span></span> <span data-ttu-id="5722b-231">在 [使用者欄位] 文字方塊中，輸入 **email** 或 **user_name**，這取決於會用哪一個欄位來唯一識別 ServiceNow 部署中的使用者。</span><span class="sxs-lookup"><span data-stu-id="5722b-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="5722b-232">移至 Azure 傳統入口網站的 [ServiceNow] > [屬性] > [單一登入] 區段，並將所要的欄位對應至 [nameidentifier] 屬性，即可設定 Azure AD 以發出 Azure AD 使用者識別碼 (使用者主體名稱) 或電子郵件地址做為 SAML 權杖中的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="5722b-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="5722b-233">所選屬性儲存在 Azure AD 中的值 (例如使用者主體名稱) 必須符合所輸入欄位 (例如 user_name) 儲存在 ServiceNow 中的值</span><span class="sxs-lookup"><span data-stu-id="5722b-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="5722b-234">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-234">c.</span></span> <span data-ttu-id="5722b-235">在 Azure AD 傳統入口網站中，複製 [識別提供者 ID] 值，然後將它貼至 [識別提供者 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5722b-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="5722b-236">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-236">d.</span></span> <span data-ttu-id="5722b-237">在 Azure AD 傳統入口網站中，複製 [驗證要求 URL] 值，然後將它貼至 [識別提供者的 AuthnRequest] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5722b-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="5722b-238">e.</span><span class="sxs-lookup"><span data-stu-id="5722b-238">e.</span></span> <span data-ttu-id="5722b-239">在 Azure AD 傳統入口網站中，複製 [單一登出服務 URL] 值，然後將它貼至 [識別提供者的 SingleLogoutRequest] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5722b-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="5722b-240">f.</span><span class="sxs-lookup"><span data-stu-id="5722b-240">f.</span></span> <span data-ttu-id="5722b-241">在 [ServiceNow 首頁] 文字方塊中，輸入您的 ServiceNow 執行個體首頁的 URL。</span><span class="sxs-lookup"><span data-stu-id="5722b-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5722b-242">串連您的 [ServieNow 租用戶 URL] 和 **/navpage.do** (例如：`https://fabrikam.service-now.com/navpage.do`)，就是 ServiceNow 執行個體首頁。</span><span class="sxs-lookup"><span data-stu-id="5722b-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="5722b-243">g.</span><span class="sxs-lookup"><span data-stu-id="5722b-243">g.</span></span> <span data-ttu-id="5722b-244">在 [對象識別碼/核發者] 文字方塊中，輸入您的 ServiceNow 租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="5722b-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="5722b-245">h.</span><span class="sxs-lookup"><span data-stu-id="5722b-245">h.</span></span> <span data-ttu-id="5722b-246">在 [對象 URL] 文字方塊中，輸入您的 ServiceNow 租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="5722b-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="5722b-247">i.</span><span class="sxs-lookup"><span data-stu-id="5722b-247">i.</span></span> <span data-ttu-id="5722b-248">在 [IDP 的 SingleLogoutRequest 通訊協定繫結] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**。</span><span class="sxs-lookup"><span data-stu-id="5722b-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="5722b-249">j.</span><span class="sxs-lookup"><span data-stu-id="5722b-249">j.</span></span> <span data-ttu-id="5722b-250">在 [名稱識別碼原則] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**。</span><span class="sxs-lookup"><span data-stu-id="5722b-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="5722b-251">k.</span><span class="sxs-lookup"><span data-stu-id="5722b-251">k.</span></span> <span data-ttu-id="5722b-252">取消選取 [建立 AuthnContextClass]。</span><span class="sxs-lookup"><span data-stu-id="5722b-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="5722b-253">l.</span><span class="sxs-lookup"><span data-stu-id="5722b-253">l.</span></span> <span data-ttu-id="5722b-254">在 **AuthnContextClassRef 方法**中，輸入 `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`。</span><span class="sxs-lookup"><span data-stu-id="5722b-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="5722b-255">只有您是僅限雲端組織時才需要此值。</span><span class="sxs-lookup"><span data-stu-id="5722b-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="5722b-256">如果您使用內部部署 ADFS 或 MFA 進行驗證，則不應該設定這個值。</span><span class="sxs-lookup"><span data-stu-id="5722b-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="5722b-257">m.</span><span class="sxs-lookup"><span data-stu-id="5722b-257">m.</span></span> <span data-ttu-id="5722b-258">在 [時鐘誤差] 文字方塊中，輸入 **60**。</span><span class="sxs-lookup"><span data-stu-id="5722b-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="5722b-259">n.</span><span class="sxs-lookup"><span data-stu-id="5722b-259">n.</span></span> <span data-ttu-id="5722b-260">針對**單一登入指令碼**，選取 **MultiSSO_SAML2_Update1**。</span><span class="sxs-lookup"><span data-stu-id="5722b-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="5722b-261">o.</span><span class="sxs-lookup"><span data-stu-id="5722b-261">o.</span></span> <span data-ttu-id="5722b-262">針對 **x509 憑證**，選取您在上一個步驟中建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="5722b-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="5722b-263">p.</span><span class="sxs-lookup"><span data-stu-id="5722b-263">p.</span></span> <span data-ttu-id="5722b-264">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="5722b-265">在 Azure AD 傳統入口網站上，選取單一登入設定確認，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="5722b-266">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="5722b-267">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5722b-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="5722b-268">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="5722b-269">為 ServiceNow Express 設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5722b-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="5722b-270">在 Azure AD 傳統入口網站的 [ServiceNow] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5722b-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="5722b-271">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749323.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="5722b-272">在 [您希望使用者如何登入 ServiceNow] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5722b-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="5722b-273">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749324.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="5722b-274">在 [設定應用程式設定]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="5722b-275">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="5722b-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="5722b-276">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-276">a.</span></span> <span data-ttu-id="5722b-277">在 [ServiceNow 登入 URL] 文字方塊中，使用下列模式輸入使用者用來登入 ServiceNow 應用程式的 URL：`https://<instance-name>.service-now.com`。</span><span class="sxs-lookup"><span data-stu-id="5722b-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="5722b-278">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-278">b.</span></span> <span data-ttu-id="5722b-279">在 [簽發者 URL] 文字方塊中，使用下列模式輸入使用者用來登入 ServiceNow 應用程式的 URL：`https://<instance-name>.service-now.com`。</span><span class="sxs-lookup"><span data-stu-id="5722b-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="5722b-280">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-280">c.</span></span> <span data-ttu-id="5722b-281">按一下 [下一步] </span><span class="sxs-lookup"><span data-stu-id="5722b-281">Click **Next**</span></span>

4. <span data-ttu-id="5722b-282">按一下 [手動設定應用程式以進行單一登入]，然後按 [下一步] 並完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="5722b-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="5722b-283">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="5722b-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="5722b-284">在 [在 ServiceNow 設定單一登入] 頁面上，按一下 [下載憑證]，然後在本機電腦上儲存憑證檔案，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5722b-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="5722b-285">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749325.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="5722b-286">以系統管理員身分登入您的 ServiceNow Express 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5722b-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="5722b-287">在左側導覽窗格中按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5722b-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="5722b-288">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="5722b-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="5722b-289">在 [單一登入] 對話方塊中，按一下右上方的 [設定] 圖示，然後設定下列屬性︰</span><span class="sxs-lookup"><span data-stu-id="5722b-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="5722b-290">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="5722b-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="5722b-291">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-291">a.</span></span> <span data-ttu-id="5722b-292">將 [啟用多個提供者 SSO] 切換到右邊。</span><span class="sxs-lookup"><span data-stu-id="5722b-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="5722b-293">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-293">b.</span></span> <span data-ttu-id="5722b-294">將 [啟用偵錯記錄以供多個提供者 SSO 整合] 切換到右邊。</span><span class="sxs-lookup"><span data-stu-id="5722b-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="5722b-295">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-295">c.</span></span> <span data-ttu-id="5722b-296">在 [使用者資料表上的欄位...] 文字方塊中，輸入 **user_name**。</span><span class="sxs-lookup"><span data-stu-id="5722b-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="5722b-297">在 [單一登入] 對話方塊上，按一下 [新增憑證]。</span><span class="sxs-lookup"><span data-stu-id="5722b-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="5722b-298">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="5722b-299">在 [X.509 憑證]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="5722b-300">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="5722b-301">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-301">a.</span></span> <span data-ttu-id="5722b-302">在 [名稱] 文字方塊中，輸入您的設定名稱 (例如：**TestSAML2.0**)。</span><span class="sxs-lookup"><span data-stu-id="5722b-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="5722b-303">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-303">b.</span></span> <span data-ttu-id="5722b-304">選取 [使用中] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-304">Select **Active**.</span></span>
    
    <span data-ttu-id="5722b-305">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-305">c.</span></span> <span data-ttu-id="5722b-306">針對 [格式]，選取 [PEM]。</span><span class="sxs-lookup"><span data-stu-id="5722b-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="5722b-307">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-307">d.</span></span> <span data-ttu-id="5722b-308">針對 [類型]，選取 [信任存放區憑證]。</span><span class="sxs-lookup"><span data-stu-id="5722b-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="5722b-309">e.</span><span class="sxs-lookup"><span data-stu-id="5722b-309">e.</span></span> <span data-ttu-id="5722b-310">從您下載的憑證建立 Base64 編碼的檔案。</span><span class="sxs-lookup"><span data-stu-id="5722b-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5722b-311">如需詳細資訊，請參閱 [如何將二進位憑證轉換成文字檔](http://youtu.be/PlgrzUZ-Y1o)。</span><span class="sxs-lookup"><span data-stu-id="5722b-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="5722b-312">f.</span><span class="sxs-lookup"><span data-stu-id="5722b-312">f.</span></span> <span data-ttu-id="5722b-313">在記事本中開啟您的 Base64 編碼的憑證，將其內容複製到剪貼簿，然後貼到 [PEM 憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5722b-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="5722b-314">g.</span><span class="sxs-lookup"><span data-stu-id="5722b-314">g.</span></span> <span data-ttu-id="5722b-315">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-315">Click **Update**.</span></span>
11. <span data-ttu-id="5722b-316">在 [單一登入] 對話方塊上，按一下 [新增 IdP]。</span><span class="sxs-lookup"><span data-stu-id="5722b-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="5722b-317">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="5722b-318">在 [新增識別提供者] 對話方塊的 [設定識別提供者] 之下，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="5722b-319">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="5722b-320">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-320">a.</span></span> <span data-ttu-id="5722b-321">在 [名稱] 文字方塊中，輸入您的組態名稱 (例如：**SAML 2.0**)。</span><span class="sxs-lookup"><span data-stu-id="5722b-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="5722b-322">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-322">b.</span></span> <span data-ttu-id="5722b-323">在 Azure AD 傳統入口網站中，複製 [識別提供者 ID] 值，然後將它貼至 [識別提供者 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5722b-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="5722b-324">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-324">c.</span></span> <span data-ttu-id="5722b-325">在 Azure AD 傳統入口網站中，複製 [驗證要求 URL] 值，然後將它貼至 [識別提供者的 AuthnRequest] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5722b-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="5722b-326">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-326">d.</span></span> <span data-ttu-id="5722b-327">在 Azure AD 傳統入口網站中，複製 [單一登出服務 URL] 值，然後將它貼至 [識別提供者的 SingleLogoutRequest] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5722b-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="5722b-328">e.</span><span class="sxs-lookup"><span data-stu-id="5722b-328">e.</span></span> <span data-ttu-id="5722b-329">針對 [識別提供者憑證]，選取您在上一個步驟中建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="5722b-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="5722b-330">按一下 [進階設定]，然後在 [其他識別提供者屬性] 之下，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="5722b-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="5722b-331">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="5722b-332">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-332">a.</span></span> <span data-ttu-id="5722b-333">在 [IDP 的 SingleLogoutRequest 通訊協定繫結] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**。</span><span class="sxs-lookup"><span data-stu-id="5722b-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="5722b-334">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-334">b.</span></span> <span data-ttu-id="5722b-335">在 [名稱識別碼原則] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**。</span><span class="sxs-lookup"><span data-stu-id="5722b-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="5722b-336">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-336">c.</span></span> <span data-ttu-id="5722b-337">在 **AuthnContextClassRef 方法**中，輸入 **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**。</span><span class="sxs-lookup"><span data-stu-id="5722b-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="5722b-338">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-338">d.</span></span> <span data-ttu-id="5722b-339">取消選取 [建立 AuthnContextClass]。</span><span class="sxs-lookup"><span data-stu-id="5722b-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="5722b-340">在 [其他服務提供者屬性] 之下，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="5722b-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="5722b-341">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="5722b-342">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-342">a.</span></span> <span data-ttu-id="5722b-343">在 [ServiceNow 首頁] 文字方塊中，輸入您的 ServiceNow 執行個體首頁的 URL。</span><span class="sxs-lookup"><span data-stu-id="5722b-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="5722b-344">串連您的 [ServieNow 租用戶 URL] 和 **/navpage.do** (例如：`https://fabrikam.service-now.com/navpage.do`)，就是 ServiceNow 執行個體首頁。</span><span class="sxs-lookup"><span data-stu-id="5722b-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="5722b-345">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-345">b.</span></span> <span data-ttu-id="5722b-346">在 [對象識別碼/核發者] 文字方塊中，輸入您的 ServiceNow 租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="5722b-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="5722b-347">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-347">c.</span></span> <span data-ttu-id="5722b-348">在 [對象 URI] 文字方塊中，輸入您的 ServiceNow 租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="5722b-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="5722b-349">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-349">d.</span></span> <span data-ttu-id="5722b-350">在 [時鐘誤差] 文字方塊中，輸入 **60**。</span><span class="sxs-lookup"><span data-stu-id="5722b-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="5722b-351">e.</span><span class="sxs-lookup"><span data-stu-id="5722b-351">e.</span></span> <span data-ttu-id="5722b-352">在 [使用者欄位] 文字方塊中，輸入 **email** 或 **user_name**，這取決於會用哪一個欄位來唯一識別 ServiceNow 部署中的使用者。</span><span class="sxs-lookup"><span data-stu-id="5722b-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="5722b-353">移至 Azure 傳統入口網站的 [ServiceNow] > [屬性] > [單一登入] 區段，並將所要的欄位對應至 [nameidentifier] 屬性，即可設定 Azure AD 以發出 Azure AD 使用者識別碼 (使用者主體名稱) 或電子郵件地址做為 SAML 權杖中的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="5722b-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="5722b-354">所選屬性儲存在 Azure AD 中的值 (例如使用者主體名稱) 必須符合所輸入欄位 (例如 user_name) 儲存在 ServiceNow 中的值</span><span class="sxs-lookup"><span data-stu-id="5722b-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="5722b-355">f.</span><span class="sxs-lookup"><span data-stu-id="5722b-355">f.</span></span> <span data-ttu-id="5722b-356">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-356">Click **Save**.</span></span> 

3. <span data-ttu-id="5722b-357">在 Azure AD 傳統入口網站上，選取單一登入設定確認，然後按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="5722b-358">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="5722b-359">在 [單一登入確認] 頁面上，按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5722b-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="5722b-360">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="5722b-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="5722b-361">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="5722b-361">Configuring user provisioning</span></span>
<span data-ttu-id="5722b-362">本節的目的是要說明如何對 ServiceNow 啟用 Active Directory 使用者帳戶的使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="5722b-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="5722b-363">若要設定使用者佈建，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="5722b-364">在 Azure 傳統管理入口網站中的 [ServiceNow] 應用程式整合頁面上，按一下 [設定使用者佈建]。</span><span class="sxs-lookup"><span data-stu-id="5722b-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="5722b-365">![使用者佈建](./media/active-directory-saas-servicenow-tutorial/IC769498.png "使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="5722b-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="5722b-366">在 [輸入您的 ServiceNow 認證來啟用自動使用者佈建] 頁面上，提供以下組態設定：</span><span class="sxs-lookup"><span data-stu-id="5722b-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="5722b-367">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-367">a.</span></span> <span data-ttu-id="5722b-368">在 [ServiceNow 執行個體名稱] 字方塊中，輸入 ServiceNow 執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="5722b-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="5722b-369">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-369">b.</span></span> <span data-ttu-id="5722b-370">在 [ServiceNow 管理使用者名稱] 文字方塊中，輸入 ServiceNow 管理員帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="5722b-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="5722b-371">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-371">c.</span></span> <span data-ttu-id="5722b-372">在 [ServiceNow 管理員密碼] 文字方塊中，輸入這個帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="5722b-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="5722b-373">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-373">d.</span></span> <span data-ttu-id="5722b-374">按一下 [驗證]  來驗證您的組態。</span><span class="sxs-lookup"><span data-stu-id="5722b-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="5722b-375">e.</span><span class="sxs-lookup"><span data-stu-id="5722b-375">e.</span></span> <span data-ttu-id="5722b-376">按 [下一步] 按鈕以開啟 [後續步驟] 頁面。</span><span class="sxs-lookup"><span data-stu-id="5722b-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="5722b-377">f.</span><span class="sxs-lookup"><span data-stu-id="5722b-377">f.</span></span> <span data-ttu-id="5722b-378">如果您想要將所有使用者佈建到此應用程式，請選取 [自動將此目錄中的所有使用者帳戶佈建到這個應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5722b-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="5722b-379">![後續步驟](./media/active-directory-saas-servicenow-tutorial/IC698804.png "後續步驟")</span><span class="sxs-lookup"><span data-stu-id="5722b-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="5722b-380">g.</span><span class="sxs-lookup"><span data-stu-id="5722b-380">g.</span></span> <span data-ttu-id="5722b-381">在 [後續步驟] 頁面上，按一下 [完成] 來儲存您的組態。</span><span class="sxs-lookup"><span data-stu-id="5722b-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5722b-382">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5722b-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="5722b-383">在本節中，您會在傳統入口網站中建立名稱為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5722b-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="5722b-385">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5722b-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5722b-386">在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="5722b-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="5722b-388">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="5722b-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="5722b-389">若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5722b-391">若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="5722b-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="5722b-393">在 [告訴我們這位使用者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="5722b-395">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-395">a.</span></span> <span data-ttu-id="5722b-396">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="5722b-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="5722b-397">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-397">b.</span></span> <span data-ttu-id="5722b-398">在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5722b-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="5722b-399">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-399">c.</span></span> <span data-ttu-id="5722b-400">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-400">Click **Next**.</span></span>

6. <span data-ttu-id="5722b-401">在 [使用者設定檔]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="5722b-403">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-403">a.</span></span> <span data-ttu-id="5722b-404">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="5722b-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="5722b-405">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-405">b.</span></span> <span data-ttu-id="5722b-406">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="5722b-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="5722b-407">c.</span><span class="sxs-lookup"><span data-stu-id="5722b-407">c.</span></span> <span data-ttu-id="5722b-408">在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="5722b-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="5722b-409">d.</span><span class="sxs-lookup"><span data-stu-id="5722b-409">d.</span></span> <span data-ttu-id="5722b-410">在 [角色] 清單中選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="5722b-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="5722b-411">e.</span><span class="sxs-lookup"><span data-stu-id="5722b-411">e.</span></span> <span data-ttu-id="5722b-412">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-412">Click **Next**.</span></span>

7. <span data-ttu-id="5722b-413">在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5722b-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="5722b-415">在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5722b-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="5722b-417">a.</span><span class="sxs-lookup"><span data-stu-id="5722b-417">a.</span></span> <span data-ttu-id="5722b-418">記下 [新密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="5722b-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="5722b-419">b.</span><span class="sxs-lookup"><span data-stu-id="5722b-419">b.</span></span> <span data-ttu-id="5722b-420">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5722b-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="5722b-421">建立 ServiceNow 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5722b-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="5722b-422">在本節中，您要在 ServiceNow 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5722b-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="5722b-423">在本節中，您要在 ServiceNow 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5722b-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="5722b-424">如果您不知道如何在 ServiceNow 或 ServiceNow Express 帳戶中新增使用者，請連絡 ServiceNow 支援小組。</span><span class="sxs-lookup"><span data-stu-id="5722b-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5722b-425">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5722b-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="5722b-426">在本節中，您會把 ServiceNow 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5722b-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![指派使用者][200] 

<span data-ttu-id="5722b-428">**若要將 Britta Simon 指派給 ServiceNow，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5722b-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="5722b-429">在傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="5722b-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![指派使用者][201] 

2. <span data-ttu-id="5722b-431">在應用程式清單中，選取 [ServiceNow]。</span><span class="sxs-lookup"><span data-stu-id="5722b-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="5722b-433">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-433">In the menu on the top, click **Users**.</span></span>
   
    ![指派使用者][203] 

4. <span data-ttu-id="5722b-435">在 [所有使用者] 清單中，選取 [Britta Simon] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="5722b-436">在底部的工具列中，按一下 [指派] 。</span><span class="sxs-lookup"><span data-stu-id="5722b-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="5722b-438">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5722b-438">Testing single sign-on</span></span>
<span data-ttu-id="5722b-439">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="5722b-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5722b-440">當您在 [存取面板] 中按一下 [ServiceNow] 圖格時，應該會自動登入您的 ServiceNow 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5722b-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5722b-441">其他資源</span><span class="sxs-lookup"><span data-stu-id="5722b-441">Additional resources</span></span>
* [<span data-ttu-id="5722b-442">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5722b-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5722b-443">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5722b-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
