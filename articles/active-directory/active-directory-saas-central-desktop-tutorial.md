---
title: "教學課程：Azure Active Directory 與 Central Desktop 整合 | Microsoft Docs"
description: "了解如何使用 Central Desktop 搭配 Azure Active Directory 來啟用單一登入、自動化佈建和更多功能！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fe32c1d68040ceb9d9de2ad6c4a6dc9ea93f5aef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="2ea70-103">教學課程：Azure Active Directory 與 Central Desktop 整合</span><span class="sxs-lookup"><span data-stu-id="2ea70-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="2ea70-104">本教學課程的目的是要示範 Azure 與 Central Desktop 的整合。</span><span class="sxs-lookup"><span data-stu-id="2ea70-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="2ea70-105">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="2ea70-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="2ea70-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="2ea70-106">A valid Azure subscription</span></span>
* <span data-ttu-id="2ea70-107">啟用 Central Desktop 單一登入的訂用帳戶/Central Desktop 租用戶</span><span class="sxs-lookup"><span data-stu-id="2ea70-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="2ea70-108">本教學課程中說明的案例由下列建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="2ea70-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="2ea70-109">啟用 Central Desktop 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="2ea70-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="2ea70-110">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="2ea70-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="2ea70-111">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="2ea70-111">Configuring user provisioning</span></span>
* <span data-ttu-id="2ea70-112">指派使用者</span><span class="sxs-lookup"><span data-stu-id="2ea70-112">Assigning users</span></span>

<span data-ttu-id="2ea70-113">![案例](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "案例")</span><span class="sxs-lookup"><span data-stu-id="2ea70-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="2ea70-114">啟用 Central Desktop 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="2ea70-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="2ea70-115">本節的目的是要說明如何啟用 Central Desktop 的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="2ea70-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="2ea70-116">**若要啟用 Central Desktop 的應用程式整合，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2ea70-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="2ea70-117">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="2ea70-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="2ea70-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="2ea70-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="2ea70-119">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="2ea70-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2ea70-120">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="2ea70-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="2ea70-121">![應用程式](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="2ea70-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="2ea70-122">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="2ea70-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="2ea70-123">![新增應用程式](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="2ea70-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="2ea70-124">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2ea70-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="2ea70-125">![從資源庫新增應用程式](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="2ea70-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="2ea70-126">在**搜尋方塊**中，輸入 **Central Desktop**。</span><span class="sxs-lookup"><span data-stu-id="2ea70-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="2ea70-127">![應用程式資源庫](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="2ea70-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="2ea70-128">在結果窗格中，選取 [Central Desktop]，然後按一下 [完成] 以加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="2ea70-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="2ea70-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="2ea70-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="2ea70-130">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="2ea70-130">Configure single sign-on</span></span>

<span data-ttu-id="2ea70-131">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶驗證至 Central Desktop。</span><span class="sxs-lookup"><span data-stu-id="2ea70-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="2ea70-132">在這個程序中，您需要上傳 base-64 編碼憑證到您的 Central Desktop 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2ea70-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="2ea70-133">如果您不熟悉此程序，請參閱 [如何將二進位憑證轉換成文字檔](http://youtu.be/PlgrzUZ-Y1o)。</span><span class="sxs-lookup"><span data-stu-id="2ea70-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="2ea70-134">**若要設定單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2ea70-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="2ea70-135">在 Azure 傳統入口網站上**Central Desktop**應用程式整合頁面上，按一下 **設定單一登入**開啟 * * 設定單一登入 * * 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2ea70-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="2ea70-136">![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="2ea70-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="2ea70-137">在 [要如何讓使用者登入 Central Desktop] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2ea70-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="2ea70-138">![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="2ea70-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="2ea70-139">在 [設定應用程式 URL] 頁面上，執行下列步驟，然後按 [下一步]：</span><span class="sxs-lookup"><span data-stu-id="2ea70-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="2ea70-140">在 [Central Desktop 登入 URL] 文字方塊中，輸入您的 Central Desktop 租用戶 URL (例如：*http://contoso.centraldesktop.com*)。</span><span class="sxs-lookup"><span data-stu-id="2ea70-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="2ea70-141">在 [Central Desktop 回覆 URL] 文字方塊中，輸入您的 Central Desktop AssertionConsumerService URL (例如：https://contoso.centraldesktop.com/saml2-assertion.php)。</span><span class="sxs-lookup"><span data-stu-id="2ea70-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="2ea70-142">您可以從 Central Desktop 中繼資料取得這個值 (例如：*http://contoso.centraldesktop.com*)。</span><span class="sxs-lookup"><span data-stu-id="2ea70-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="2ea70-143">![設定應用程式 URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="2ea70-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="2ea70-144">於 [在 Central Desktop 設定單一登入] 頁面上，按 [下載憑證] 以下載您的憑證，然後將憑證檔案儲存在您的電腦中。</span><span class="sxs-lookup"><span data-stu-id="2ea70-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="2ea70-145">![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="2ea70-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="2ea70-146">登入您的 **Central Desktop** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2ea70-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="2ea70-147">移至 [設定]，按一下 [進階]，然後按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="2ea70-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="2ea70-148">![設定 - 進階](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "設定 - 進階")</span><span class="sxs-lookup"><span data-stu-id="2ea70-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="2ea70-149">在 [單一登入設定]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2ea70-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="2ea70-150">![單一登入設定](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="2ea70-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="2ea70-151">選取 [啟用 SAML v2 單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="2ea70-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="2ea70-152">在 Azure 傳統入口網站的 [在 Central Desktop 設定單一登入] 頁面上，複製 [簽發者 URL] 的值，然後將它貼到 [SSO URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="2ea70-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="2ea70-153">在 Azure 傳統入口網站的 [在 Central Desktop 設定單一登入] 頁面上，複製 [遠端登入 URL] 值，然後將它貼到 [SSO 登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="2ea70-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="2ea70-154">在 Azure 傳統入口網站的 [在 Central Desktop 設定單一登入] 頁面上，複製 [單一登出服務 URL] 值，然後將它貼到 [SSO 登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="2ea70-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="2ea70-155">在 [訊息簽章驗證方法]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="2ea70-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="2ea70-156">![訊息簽章驗證方法](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "訊息簽章驗證方法")</span><span class="sxs-lookup"><span data-stu-id="2ea70-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="2ea70-157">選取 [憑證] 。</span><span class="sxs-lookup"><span data-stu-id="2ea70-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="2ea70-158">從 [SSO 憑證] 清單中選取 [RSH SHA256]。</span><span class="sxs-lookup"><span data-stu-id="2ea70-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="2ea70-159">從下載的憑證建立文字檔，複製文字檔的內容，然後將內容貼到 [SSO 憑證]  欄位中。</span><span class="sxs-lookup"><span data-stu-id="2ea70-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="2ea70-160">如需詳細資訊，請參閱 [如何將二進位憑證轉換成文字檔](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="2ea70-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="2ea70-161">選取 [顯示 SAMLv2 登入頁面的連結] 。</span><span class="sxs-lookup"><span data-stu-id="2ea70-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="2ea70-162">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="2ea70-162">Click **Update**.</span></span>
10. <span data-ttu-id="2ea70-163">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2ea70-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="2ea70-164">![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="2ea70-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="2ea70-165">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="2ea70-165">Configure user provisioning</span></span>

<span data-ttu-id="2ea70-166">AAD 使用者必須先佈建到 Central Desktop 應用程式，才可以登入。</span><span class="sxs-lookup"><span data-stu-id="2ea70-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="2ea70-167">本節說明如何在 Central Desktop 中建立 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ea70-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="2ea70-168">**將使用者帳戶佈建到 Central Desktop：**</span><span class="sxs-lookup"><span data-stu-id="2ea70-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="2ea70-169">登入您的 Central Desktop 租用戶。</span><span class="sxs-lookup"><span data-stu-id="2ea70-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="2ea70-170">移至 [人員] \> [內部成員]。</span><span class="sxs-lookup"><span data-stu-id="2ea70-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="2ea70-171">按一下 [加入內部成員] 。</span><span class="sxs-lookup"><span data-stu-id="2ea70-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="2ea70-172">![人員](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "人員")</span><span class="sxs-lookup"><span data-stu-id="2ea70-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="2ea70-173">在 [新成員的電子郵件地址] 文字方塊中，輸入您想要佈建的 AAD 帳戶，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2ea70-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="2ea70-174">![新成員的電子郵件地址](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "新成員的電子郵件地址")</span><span class="sxs-lookup"><span data-stu-id="2ea70-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="2ea70-175">按一下 [加入內部成員] 。</span><span class="sxs-lookup"><span data-stu-id="2ea70-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="2ea70-176">![加入內部成員](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "加入內部成員")</span><span class="sxs-lookup"><span data-stu-id="2ea70-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="2ea70-177">您加入的使用者會收到一封包含確認連結的電子郵件，使用者必須按一下才能啟用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ea70-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="2ea70-178">您可以使用任何其他的 Central Desktop 使用者帳戶建立工具或 Central Desktop 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ea70-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="2ea70-179">指派使用者</span><span class="sxs-lookup"><span data-stu-id="2ea70-179">Assign users</span></span>
<span data-ttu-id="2ea70-180">若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。</span><span class="sxs-lookup"><span data-stu-id="2ea70-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="2ea70-181">**若要指派使用者給 Central Desktop，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="2ea70-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="2ea70-182">在 Azure 傳統入口網站中建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ea70-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="2ea70-183">在 [Central Desktop] 應用程式整合頁面上，按一下 [指派使用者]。</span><span class="sxs-lookup"><span data-stu-id="2ea70-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="2ea70-184">![指派使用者](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="2ea70-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="2ea70-185">選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。</span><span class="sxs-lookup"><span data-stu-id="2ea70-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="2ea70-186">![是](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="2ea70-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="2ea70-187">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="2ea70-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="2ea70-188">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="2ea70-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

