---
title: "教學課程：Azure Active Directory 與 Replicon 整合 | Microsoft Docs"
description: "了解如何使用 Replicon 搭配 Azure Active Directory 來啟用單一登入、自動佈建和更多功能！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2aeeceb61191962b62892b8409218684f76c6fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="86b5d-103">教學課程：Azure Active Directory 與 Replicon 整合</span><span class="sxs-lookup"><span data-stu-id="86b5d-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="86b5d-104">本教學課程的目的是要示範 Azure 與 Replicon 的整合。</span><span class="sxs-lookup"><span data-stu-id="86b5d-104">The objective of this tutorial is to show the integration of Azure and Replicon.</span></span> <span data-ttu-id="86b5d-105">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="86b5d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="86b5d-106">有效的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="86b5d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="86b5d-107">Replicon 租用戶</span><span class="sxs-lookup"><span data-stu-id="86b5d-107">A Replicon tenant</span></span>

<span data-ttu-id="86b5d-108">完成本教學課程之後，您指派給 Replicon 的 Azure AD 使用者就能夠從您的 Replicon 公司網站 (服務提供者起始登入)，或使用 [存取面板](active-directory-saas-access-panel-introduction.md)來單一登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="86b5d-108">After completing this tutorial, the Azure AD users you have assigned to Replicon will be able to single sign into the application at your Replicon company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="86b5d-109">本教學課程中說明的案例由下列建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="86b5d-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="86b5d-110">啟用 Replicon 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="86b5d-110">Enabling the application integration for Replicon</span></span>
2. <span data-ttu-id="86b5d-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="86b5d-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="86b5d-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="86b5d-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="86b5d-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="86b5d-113">Assigning users</span></span>

<span data-ttu-id="86b5d-114">![案例](./media/active-directory-saas-replicon-tutorial/IC777798.png "案例")</span><span class="sxs-lookup"><span data-stu-id="86b5d-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-replicon"></a><span data-ttu-id="86b5d-115">啟用 Replicon 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="86b5d-115">Enable the application integration for Replicon</span></span>
<span data-ttu-id="86b5d-116">本節的目的是要說明如何啟用 Replicon 的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="86b5d-116">The objective of this section is to outline how to enable the application integration for Replicon.</span></span>

<span data-ttu-id="86b5d-117">**若要啟用 Replicon 的應用程式整合，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="86b5d-117">**To enable the application integration for Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="86b5d-118">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="86b5d-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="86b5d-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="86b5d-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="86b5d-120">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="86b5d-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="86b5d-121">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="86b5d-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="86b5d-122">![應用程式](./media/active-directory-saas-replicon-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="86b5d-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="86b5d-123">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="86b5d-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="86b5d-124">![新增應用程式](./media/active-directory-saas-replicon-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="86b5d-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="86b5d-125">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="86b5d-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="86b5d-126">![從資源庫新增應用程式](./media/active-directory-saas-replicon-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="86b5d-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="86b5d-127">在**搜尋方塊**中，輸入 **Replicon**。</span><span class="sxs-lookup"><span data-stu-id="86b5d-127">In the **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="86b5d-128">![應用程式資源庫](./media/active-directory-saas-replicon-tutorial/IC777799.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="86b5d-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="86b5d-129">在結果窗格中，選取 [Replicon]，然後按一下 [完成] 來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="86b5d-129">In the results pane, select **Replicon**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="86b5d-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="86b5d-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="86b5d-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="86b5d-131">Configure single sign-on</span></span>

<span data-ttu-id="86b5d-132">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶驗證到 Replicon。</span><span class="sxs-lookup"><span data-stu-id="86b5d-132">The objective of this section is to outline how to enable users to authenticate to Replicon with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="86b5d-133">**若要設定單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="86b5d-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="86b5d-134">在 Azure 傳統入口網站的 [Replicon] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="86b5d-134">In the Azure classic portal, on the **Replicon** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="86b5d-135">![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC777801.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="86b5d-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="86b5d-136">在 [要如何讓使用者登入 Replicon] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="86b5d-136">On the **How would you like users to sign on to Replicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="86b5d-137">![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC777802.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="86b5d-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="86b5d-138">在 [設定應用程式 URL]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="86b5d-138">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="86b5d-139">![設定應用程式 URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="86b5d-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="86b5d-140">在 [Replicon 登入 URL] 文字方塊中，輸入 Replicon 租用戶 URL (例如︰https://na2.replicon.com/company/saml2/sp-sso/post)。</span><span class="sxs-lookup"><span data-stu-id="86b5d-140">In the **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="86b5d-141">在 [Replicon 回覆 URL] 文字方塊中，輸入您的 Replicon **AssertionConsumerService** URL (例如：https://global.replicon.com/!/saml2/company/sso/post)。</span><span class="sxs-lookup"><span data-stu-id="86b5d-141">In the **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="86b5d-142">您可以從以下位置的 Replicon 中繼資料取得 URL：**https://global.replicon.com/!/saml2/\<YourCompanyKey\>**。</span><span class="sxs-lookup"><span data-stu-id="86b5d-142">You can get the URL from the Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="86b5d-143">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="86b5d-143">Click **Next**.</span></span>

4. <span data-ttu-id="86b5d-144">在 [設定在 Replicon 單一登入] 頁面上，按一下 [下載中繼資料] 來下載您的中繼資料，然後將中繼資料儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="86b5d-144">On the **Configure single sign-on at Replicon** page, to download your metadata, click **Download metadata**, and then save the metadata on your computer.</span></span>
   
    <span data-ttu-id="86b5d-145">![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC777804.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="86b5d-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="86b5d-146">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Replicon 公司網站。</span><span class="sxs-lookup"><span data-stu-id="86b5d-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="86b5d-147">若要設定 SAML 2.0，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="86b5d-147">To configure SAML 2.0, perform the following steps:</span></span>
   
    <span data-ttu-id="86b5d-148">![啟用 SAML 驗證](./media/active-directory-saas-replicon-tutorial/IC777805.png "啟用 SAML 驗證")</span><span class="sxs-lookup"><span data-stu-id="86b5d-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="86b5d-149">若要顯示 [EnableSAML Authentication2] 對話方塊，請將下列內容附加至 URL 中的公司金鑰之後︰**/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="86b5d-149">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="86b5d-150">下面會顯示完整 URL 的結構描述︰</span><span class="sxs-lookup"><span data-stu-id="86b5d-150">The following shows the schema of the complete URL:</span></span>  
   <span data-ttu-id="86b5d-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="86b5d-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="86b5d-152">按一下 [+] 來展開 [v20Configuration] 區段。</span><span class="sxs-lookup"><span data-stu-id="86b5d-152">Click the **+** to expand the **v20Configuration** section.</span></span>
   3. <span data-ttu-id="86b5d-153">按一下 [+] 來展開 [metaDataConfiguration] 區段。</span><span class="sxs-lookup"><span data-stu-id="86b5d-153">Click the **+** to expand the **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="86b5d-154">按一下 [選擇檔案]，選取您的識別提供者中繼資料 XML 檔案，然後按一下 [提交]。</span><span class="sxs-lookup"><span data-stu-id="86b5d-154">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="86b5d-155">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="86b5d-155">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="86b5d-156">![設定單一登入](./media/active-directory-saas-replicon-tutorial/IC778418.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="86b5d-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="86b5d-157">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="86b5d-157">Configure user provisioning</span></span>

<span data-ttu-id="86b5d-158">若要讓 Azure AD 使用者可以登入 Replicon，則必須將他們佈建至 Replicon。</span><span class="sxs-lookup"><span data-stu-id="86b5d-158">In order to enable Azure AD users to log into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="86b5d-159">在 Replicon 的情況下，需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="86b5d-159">In the case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="86b5d-160">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="86b5d-160">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="86b5d-161">在 Web 瀏覽器視窗中，以系統管理員身分登入您的 Replicon 公司網站。</span><span class="sxs-lookup"><span data-stu-id="86b5d-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="86b5d-162">移至 [管理] \> [使用者]。</span><span class="sxs-lookup"><span data-stu-id="86b5d-162">Go to **Administration \> Users**.</span></span>
   
    <span data-ttu-id="86b5d-163">![使用者](./media/active-directory-saas-replicon-tutorial/IC777806.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="86b5d-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="86b5d-164">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="86b5d-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="86b5d-165">![新增使用者](./media/active-directory-saas-replicon-tutorial/IC777807.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="86b5d-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="86b5d-166">在 [使用者設定檔]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="86b5d-166">In the **User Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="86b5d-167">![使用者設定檔](./media/active-directory-saas-replicon-tutorial/IC777808.png "使用者設定檔")</span><span class="sxs-lookup"><span data-stu-id="86b5d-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="86b5d-168">在 [登入名稱]  文字方塊中，輸入您要佈建之 Azure AD 使用者的 Azure AD 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="86b5d-168">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision.</span></span>
  2. <span data-ttu-id="86b5d-169">針對 [驗證類型] 選取 [SSO]。</span><span class="sxs-lookup"><span data-stu-id="86b5d-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="86b5d-170">在 [部門]  文字方塊中，輸入使用者的部門。</span><span class="sxs-lookup"><span data-stu-id="86b5d-170">In the **Department** textbox, type the user’s department.</span></span>
  4. <span data-ttu-id="86b5d-171">針對 [員工類型] 選取 [系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="86b5d-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="86b5d-172">按一下 [儲存使用者設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="86b5d-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="86b5d-173">您可以使用任何其他的 Replicon 使用者帳戶建立工具或 Replicon 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="86b5d-173">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="86b5d-174">指派使用者</span><span class="sxs-lookup"><span data-stu-id="86b5d-174">Assign users</span></span>
<span data-ttu-id="86b5d-175">若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。</span><span class="sxs-lookup"><span data-stu-id="86b5d-175">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="86b5d-176">**若要將使用者指派給 Replicon，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="86b5d-176">**To assign users to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="86b5d-177">在 Azure 傳統入口網站中建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="86b5d-177">In the Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="86b5d-178">在 [Replicon] 應用程式整合頁面上，按一下 [指派使用者]。</span><span class="sxs-lookup"><span data-stu-id="86b5d-178">On the **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="86b5d-179">![指派使用者](./media/active-directory-saas-replicon-tutorial/IC777809.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="86b5d-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="86b5d-180">選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。</span><span class="sxs-lookup"><span data-stu-id="86b5d-180">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="86b5d-181">![是](./media/active-directory-saas-replicon-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="86b5d-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="86b5d-182">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="86b5d-182">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="86b5d-183">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="86b5d-183">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

