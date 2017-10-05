---
title: "教學課程：Azure Active Directory 與 TOPdesk - Secure 整合 | Microsoft Docs"
description: "了解如何使用 TOPdesk - Secure 搭配 Azure Active Directory 來啟用單一登入、自動佈建和更多功能！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 28f0542dbe87bb34c83a7852db7c3a9fef055ce9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="66b0f-103">教學課程：Azure Active Directory 與 TOPdesk - Secure 整合</span><span class="sxs-lookup"><span data-stu-id="66b0f-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="66b0f-104">本教學課程的目的是要示範 Azure 與 TOPdesk - Secure 的整合。</span><span class="sxs-lookup"><span data-stu-id="66b0f-104">The objective of this tutorial is to show the integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="66b0f-105">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="66b0f-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="66b0f-106">有效的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66b0f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="66b0f-107">已啟用 TOPdesk - Secure 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66b0f-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="66b0f-108">完成本教學課程之後，您指派給 TOPdesk - Secure 的 Azure AD 使用者就能夠從您的 TOPdesk - Secure 公司網站 (服務提供者起始登入)，或使用 [存取面板](active-directory-saas-access-panel-introduction.md)來單一登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="66b0f-108">After completing this tutorial, the Azure AD users you have assigned to TOPdesk - Secure will be able to single sign into the application at your TOPdesk - Secure company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="66b0f-109">本教學課程中說明的案例由下列建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="66b0f-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="66b0f-110">啟用 TOPdesk - Secure 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="66b0f-110">Enabling the application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="66b0f-111">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="66b0f-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="66b0f-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="66b0f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="66b0f-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="66b0f-113">Assigning users</span></span>

<span data-ttu-id="66b0f-114">![案例](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "案例")</span><span class="sxs-lookup"><span data-stu-id="66b0f-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-topdesk---secure"></a><span data-ttu-id="66b0f-115">啟用 TOPdesk - Secure 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="66b0f-115">Enabling the application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="66b0f-116">本節的目的是要說明如何啟用 TOPdesk - Secure 的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="66b0f-116">The objective of this section is to outline how to enable the application integration for TOPdesk - Secure.</span></span>

### <a name="to-enable-the-application-integration-for-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="66b0f-117">若要啟用 TOPdesk - Secure 的應用程式整合，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66b0f-117">To enable the application integration for TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="66b0f-118">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="66b0f-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="66b0f-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="66b0f-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="66b0f-120">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="66b0f-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="66b0f-121">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="66b0f-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="66b0f-122">![應用程式](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="66b0f-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="66b0f-123">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="66b0f-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="66b0f-124">![新增應用程式](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="66b0f-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="66b0f-125">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="66b0f-126">![從資源庫新增應用程式](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="66b0f-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="66b0f-127">在**搜尋方塊**中，輸入 **TOPdesk - Secure**。</span><span class="sxs-lookup"><span data-stu-id="66b0f-127">In the **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="66b0f-128">![應用程式資源庫](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="66b0f-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="66b0f-129">在結果窗格中，選取 [TOPdesk - Secure]，然後按一下 [完成] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="66b0f-129">In the results pane, select **TOPdesk - Secure**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="66b0f-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="66b0f-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="66b0f-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="66b0f-131">Configuring single sign-on</span></span>
<span data-ttu-id="66b0f-132">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己在 Azure AD 中的帳戶驗證至 TOPdesk - Secure。</span><span class="sxs-lookup"><span data-stu-id="66b0f-132">The objective of this section is to outline how to enable users to authenticate to TOPdesk - Secure with their account in Azure AD using federation based on the SAML protocol.</span></span>  
<span data-ttu-id="66b0f-133">設定 TOPdesk - Secure 的單一登入需要您上傳標誌的圖示檔。</span><span class="sxs-lookup"><span data-stu-id="66b0f-133">Configuring single sign-on for TOPdesk - Secure requires you to upload a logo icon file.</span></span> <span data-ttu-id="66b0f-134">若要取得圖示檔，請連絡 TOPdesk 支援小組。</span><span class="sxs-lookup"><span data-stu-id="66b0f-134">To get the icon file, contact the TOPdesk support team.</span></span>

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a><span data-ttu-id="66b0f-135">若要設定單一登入，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66b0f-135">To configure single sign-on, perform the following steps:</span></span>
1. <span data-ttu-id="66b0f-136">以系統管理員身分登入您的 **TOPdesk - Secure** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="66b0f-136">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="66b0f-137">在 [TOPdesk] 功能表中按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-137">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="66b0f-138">![設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "設定")</span><span class="sxs-lookup"><span data-stu-id="66b0f-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="66b0f-139">按一下 [登入設定] 。</span><span class="sxs-lookup"><span data-stu-id="66b0f-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="66b0f-140">![登入設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "登入設定")</span><span class="sxs-lookup"><span data-stu-id="66b0f-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="66b0f-141">展開 [登入設定] 功能表，然後按一下 [一般]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-141">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="66b0f-142">![一般](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "一般")</span><span class="sxs-lookup"><span data-stu-id="66b0f-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="66b0f-143">在 [SAML 登入] 組態區段的 **Secure** 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66b0f-143">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="66b0f-144">![技術設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "技術設定")</span><span class="sxs-lookup"><span data-stu-id="66b0f-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="66b0f-145">a.</span><span class="sxs-lookup"><span data-stu-id="66b0f-145">a.</span></span> <span data-ttu-id="66b0f-146">按 [下載]  來下載公用中繼資料檔案，然後再將它儲存在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="66b0f-146">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="66b0f-147">b.</span><span class="sxs-lookup"><span data-stu-id="66b0f-147">b.</span></span> <span data-ttu-id="66b0f-148">開啟此中繼資料檔案，然後找到 **AssertionConsumerService** 節點。</span><span class="sxs-lookup"><span data-stu-id="66b0f-148">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="66b0f-149">![判斷提示取用者服務](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "判斷提示取用者服務")</span><span class="sxs-lookup"><span data-stu-id="66b0f-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="66b0f-150">c.</span><span class="sxs-lookup"><span data-stu-id="66b0f-150">c.</span></span> <span data-ttu-id="66b0f-151">複製 **AssertionConsumerService** 值。</span><span class="sxs-lookup"><span data-stu-id="66b0f-151">Copy the **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="66b0f-152">在本教學課程稍後的＜ **設定應用程式 URL** ＞一節中，您將需要這個值。</span><span class="sxs-lookup"><span data-stu-id="66b0f-152">You will need the value in the **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="66b0f-153">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **Azure 傳統入口網站** 。</span><span class="sxs-lookup"><span data-stu-id="66b0f-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="66b0f-154">在**TOPdesk-Secure**應用程式整合頁面上，按一下 **設定單一登入**開啟 * * 設定單一登入 * * 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="66b0f-154">On the **TOPdesk - Secure** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="66b0f-155">![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="66b0f-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="66b0f-156">在 [要如何讓使用者登入 TOPdesk - Secure] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-156">On the **How would you like users to sign on to TOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="66b0f-157">![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="66b0f-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="66b0f-158">在 [設定應用程式 URL]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66b0f-158">On the **Configure App URL** page, perform the following steps:</span></span>
   
    <span data-ttu-id="66b0f-159">![設定應用程式 URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="66b0f-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="66b0f-160">a.</span><span class="sxs-lookup"><span data-stu-id="66b0f-160">a.</span></span> <span data-ttu-id="66b0f-161">在 [TOPdesk - Secure 登入 URL] 文字方塊中，輸入使用者用來登入 TOPdesk - Secure 應用程式的 URL (例如："*https://qssolutions.topdesk.net*")。</span><span class="sxs-lookup"><span data-stu-id="66b0f-161">In the **TOPdesk - Secure Sign On URL** textbox, type the URL used by your users to sign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="66b0f-162">b.</span><span class="sxs-lookup"><span data-stu-id="66b0f-162">b.</span></span> <span data-ttu-id="66b0f-163">在 [TOPdesk - Public 回覆 URL] 文字方塊中，貼上 **TOPdesk - Secure AssertionConsumerService URL** (例如："*https://qssolutions.topdesk.net/tas/public/login/saml*")。</span><span class="sxs-lookup"><span data-stu-id="66b0f-163">In the **TOPdesk – Public Reply URL** textbox, paste the **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="66b0f-164">c.</span><span class="sxs-lookup"><span data-stu-id="66b0f-164">c.</span></span> <span data-ttu-id="66b0f-165">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="66b0f-165">Click **Next**.</span></span>

10. <span data-ttu-id="66b0f-166">在 [設定在 TOPdesk - Secure 單一登入] 頁面上，若要下載您的中繼資料檔，請按一下 [下載中繼資料]，然後將檔案儲存在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="66b0f-166">On the **Configure single sign-on at TOPdesk - Secure** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
    
    <span data-ttu-id="66b0f-167">![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="66b0f-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="66b0f-168">若要建立憑證檔案，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66b0f-168">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="66b0f-169">![憑證](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "憑證")</span><span class="sxs-lookup"><span data-stu-id="66b0f-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="66b0f-170">a.</span><span class="sxs-lookup"><span data-stu-id="66b0f-170">a.</span></span> <span data-ttu-id="66b0f-171">開啟下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="66b0f-171">Open the downloaded metadata file.</span></span>
    <span data-ttu-id="66b0f-172">b.</span><span class="sxs-lookup"><span data-stu-id="66b0f-172">b.</span></span> <span data-ttu-id="66b0f-173">展開 **RoleDescriptor** 節點，其具有 **fed:ApplicationServiceType** 的 **xsi:type**。</span><span class="sxs-lookup"><span data-stu-id="66b0f-173">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="66b0f-174">c.</span><span class="sxs-lookup"><span data-stu-id="66b0f-174">c.</span></span> <span data-ttu-id="66b0f-175">複製 **X509Certificate** 節點的值。</span><span class="sxs-lookup"><span data-stu-id="66b0f-175">Copy the value of the **X509Certificate** node.</span></span>
    <span data-ttu-id="66b0f-176">d.</span><span class="sxs-lookup"><span data-stu-id="66b0f-176">d.</span></span> <span data-ttu-id="66b0f-177">儲存複製的 **X509Certificate** 值到本機電腦的檔案中。</span><span class="sxs-lookup"><span data-stu-id="66b0f-177">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="66b0f-178">在您 TOPdesk - Secure 公司網站的 [TOPdesk] 功能表上，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-178">On your TOPdesk - Secure company site, in the **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="66b0f-179">![設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "設定")</span><span class="sxs-lookup"><span data-stu-id="66b0f-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="66b0f-180">按一下 [登入設定] 。</span><span class="sxs-lookup"><span data-stu-id="66b0f-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="66b0f-181">![登入設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "登入設定")</span><span class="sxs-lookup"><span data-stu-id="66b0f-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="66b0f-182">展開 [登入設定] 功能表，然後按一下 [一般]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-182">Expand the **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="66b0f-183">![一般](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "一般")</span><span class="sxs-lookup"><span data-stu-id="66b0f-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="66b0f-184">在 **Public** 區段中，按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-184">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="66b0f-185">![新增](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "新增")</span><span class="sxs-lookup"><span data-stu-id="66b0f-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="66b0f-186">在 [SAML 組態輔助程式]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66b0f-186">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="66b0f-187">![SAML 組態輔助程式](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML 組態輔助程式")</span><span class="sxs-lookup"><span data-stu-id="66b0f-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="66b0f-188">a.</span><span class="sxs-lookup"><span data-stu-id="66b0f-188">a.</span></span> <span data-ttu-id="66b0f-189">若要上傳您下載的中繼資料檔，請在 [同盟中繼資料] 下按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-189">To upload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="66b0f-190">b.</span><span class="sxs-lookup"><span data-stu-id="66b0f-190">b.</span></span> <span data-ttu-id="66b0f-191">若要上傳您的憑證檔案，請在 [憑證 (RSA)] 下按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-191">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="66b0f-192">c.</span><span class="sxs-lookup"><span data-stu-id="66b0f-192">c.</span></span> <span data-ttu-id="66b0f-193">若要上傳您從 TOPdesk 支援小組取得的標誌檔案，請在 [標誌圖示] 下按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-193">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="66b0f-194">d.</span><span class="sxs-lookup"><span data-stu-id="66b0f-194">d.</span></span> <span data-ttu-id="66b0f-195">在 [使用者名稱] 屬性文字方塊中，輸入 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。</span><span class="sxs-lookup"><span data-stu-id="66b0f-195">In the **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="66b0f-196">e.</span><span class="sxs-lookup"><span data-stu-id="66b0f-196">e.</span></span> <span data-ttu-id="66b0f-197">在 [顯示名稱]  文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="66b0f-197">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="66b0f-198">f.</span><span class="sxs-lookup"><span data-stu-id="66b0f-198">f.</span></span> <span data-ttu-id="66b0f-199">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="66b0f-199">Click **Save**.</span></span>

17. <span data-ttu-id="66b0f-200">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="66b0f-200">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="66b0f-201">![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="66b0f-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="66b0f-202">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="66b0f-202">Configuring user provisioning</span></span>
<span data-ttu-id="66b0f-203">若要讓 Azure AD 使用者可以登入 TOPdesk - Secure，則必須將他們佈建到 TOPdesk - Secure。</span><span class="sxs-lookup"><span data-stu-id="66b0f-203">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="66b0f-204">TOPdesk - Secure 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="66b0f-204">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="66b0f-205">若要設定使用者佈建，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66b0f-205">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="66b0f-206">以系統管理員身分登入您的 **TOPdesk - Secure** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="66b0f-206">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="66b0f-207">在上方功能表中按一下 [TOPdesk] \> [新增] \> [支援檔案] \> [操作員]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-207">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="66b0f-208">![操作員](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "操作員")</span><span class="sxs-lookup"><span data-stu-id="66b0f-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="66b0f-209">在 [新增操作員]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66b0f-209">On the **New Operator** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="66b0f-210">![新增操作員](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "新增操作員")</span><span class="sxs-lookup"><span data-stu-id="66b0f-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="66b0f-211">a.</span><span class="sxs-lookup"><span data-stu-id="66b0f-211">a.</span></span> <span data-ttu-id="66b0f-212">按一下 [一般] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="66b0f-212">Click the General tab.</span></span>
   
    <span data-ttu-id="66b0f-213">b.</span><span class="sxs-lookup"><span data-stu-id="66b0f-213">b.</span></span> <span data-ttu-id="66b0f-214">在 [一般] 區段的 [姓氏] 文字方塊中，輸入您要佈建之有效 Azure Active Directory 帳戶的姓氏。</span><span class="sxs-lookup"><span data-stu-id="66b0f-214">In the **Surname** textbox of the **General** section, type the last name of a valid Azure Active Directory account you want to provision.</span></span>
   
    <span data-ttu-id="66b0f-215">c.</span><span class="sxs-lookup"><span data-stu-id="66b0f-215">c.</span></span> <span data-ttu-id="66b0f-216">在 [位置] 區段中選取該帳戶的 [網站]。</span><span class="sxs-lookup"><span data-stu-id="66b0f-216">Select a **Site** for the account in the **Location** section.</span></span>
   
    <span data-ttu-id="66b0f-217">d.</span><span class="sxs-lookup"><span data-stu-id="66b0f-217">d.</span></span> <span data-ttu-id="66b0f-218">在 [TOPdesk 登入] 區段的 [登入名稱] 文字方塊中，輸入使用者的登入名稱。</span><span class="sxs-lookup"><span data-stu-id="66b0f-218">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="66b0f-219">e.</span><span class="sxs-lookup"><span data-stu-id="66b0f-219">e.</span></span> <span data-ttu-id="66b0f-220">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="66b0f-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="66b0f-221">您可以使用任何其他的 TOPdesk - Secure 使用者帳戶建立工具或 TOPdesk - Secure 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="66b0f-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="66b0f-222">指派使用者</span><span class="sxs-lookup"><span data-stu-id="66b0f-222">Assigning users</span></span>
<span data-ttu-id="66b0f-223">若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。</span><span class="sxs-lookup"><span data-stu-id="66b0f-223">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-topdesk---secure-perform-the-following-steps"></a><span data-ttu-id="66b0f-224">若要指派使用者給 TOPdesk - Secure，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66b0f-224">To assign users to TOPdesk - Secure, perform the following steps:</span></span>
1. <span data-ttu-id="66b0f-225">在 Azure 傳統入口網站中建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="66b0f-225">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="66b0f-226">在 * * TOPdesk-Secure * * 應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="66b0f-226">On the **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="66b0f-227">![指派使用者](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="66b0f-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="66b0f-228">選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。</span><span class="sxs-lookup"><span data-stu-id="66b0f-228">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="66b0f-229">![是](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="66b0f-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="66b0f-230">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="66b0f-230">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="66b0f-231">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="66b0f-231">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

