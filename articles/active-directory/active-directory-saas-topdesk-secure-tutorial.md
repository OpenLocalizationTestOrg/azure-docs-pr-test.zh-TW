---
title: "教學課程：Azure Active Directory 與 TOPdesk - Secure 整合 | Microsoft Docs"
description: "深入了解如何 toouse TOPdesk-保護 Azure Active Directory tooenable 單一登入、 與自動化佈建更多 ！。"
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
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="299cd-103">教學課程：Azure Active Directory 與 TOPdesk - Secure 整合</span><span class="sxs-lookup"><span data-stu-id="299cd-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="299cd-104">本教學課程的 hello 目標是 tooshow hello 整合 Azure 與 TOPdesk-Secure。</span><span class="sxs-lookup"><span data-stu-id="299cd-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="299cd-105">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="299cd-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="299cd-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="299cd-106">A valid Azure subscription</span></span>
* <span data-ttu-id="299cd-107">已啟用 TOPdesk - Secure 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="299cd-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="299cd-108">完成本教學課程、 hello Azure AD 使用者之後您已指派 tooTOPdesk-安全的會是能 toosingle 登入位於您 TOPdesk-Secure 公司網站 （服務提供者起始登入） 的 hello 應用程式或使用 hello[簡介存取面板 toohello](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="299cd-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="299cd-109">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="299cd-110">啟用 TOPdesk-Secure 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="299cd-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="299cd-111">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="299cd-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="299cd-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="299cd-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="299cd-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="299cd-113">Assigning users</span></span>

<span data-ttu-id="299cd-114">![案例](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "案例")</span><span class="sxs-lookup"><span data-stu-id="299cd-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="299cd-115">啟用 TOPdesk-Secure 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="299cd-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="299cd-116">本節 hello 目標是 toooutline 如何 TOPdesk-Secure tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="299cd-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="299cd-117">tooenable hello 應用程式整合 TOPdesk-Secure，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="299cd-118">在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="299cd-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="299cd-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="299cd-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="299cd-120">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="299cd-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="299cd-121">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="299cd-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="299cd-122">![應用程式](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="299cd-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="299cd-123">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="299cd-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="299cd-124">![新增應用程式](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="299cd-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="299cd-125">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="299cd-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="299cd-126">![從資源庫新增應用程式](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="299cd-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="299cd-127">在 hello**搜尋方塊**，型別**TOPdesk-Secure**。</span><span class="sxs-lookup"><span data-stu-id="299cd-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="299cd-128">![應用程式資源庫](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="299cd-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="299cd-129">在 hello 結果窗格中，選取  **TOPdesk-Secure**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="299cd-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="299cd-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span><span class="sxs-lookup"><span data-stu-id="299cd-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="299cd-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="299cd-131">Configuring single sign-on</span></span>
<span data-ttu-id="299cd-132">本節 hello 目標是 toooutline 如何 tooenable 使用者 tooauthenticate tooTOPdesk-hello SAML 通訊協定為基礎的同盟，使用 Azure AD 中與他們的帳戶安全。</span><span class="sxs-lookup"><span data-stu-id="299cd-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="299cd-133">設定單一登入 topdesk-Secure 需要您 tooupload 標誌圖示檔。</span><span class="sxs-lookup"><span data-stu-id="299cd-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="299cd-134">tooget hello 圖示檔案，請連絡 hello TOPdesk 支援小組。</span><span class="sxs-lookup"><span data-stu-id="299cd-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="299cd-135">tooconfigure 單一登入，請執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="299cd-136">登入 tooyour **TOPdesk-Secure**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="299cd-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="299cd-137">在 hello **TOPdesk**功能表上，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="299cd-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="299cd-138">![設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "設定")</span><span class="sxs-lookup"><span data-stu-id="299cd-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="299cd-139">按一下 [登入設定] 。</span><span class="sxs-lookup"><span data-stu-id="299cd-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="299cd-140">![登入設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "登入設定")</span><span class="sxs-lookup"><span data-stu-id="299cd-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="299cd-141">展開 hello**登入設定**功能表，然後再按一下**一般**。</span><span class="sxs-lookup"><span data-stu-id="299cd-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="299cd-142">![一般](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "一般")</span><span class="sxs-lookup"><span data-stu-id="299cd-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="299cd-143">在 hello**安全**hello 區段**SAML 登入**組態區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="299cd-144">![技術設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "技術設定")</span><span class="sxs-lookup"><span data-stu-id="299cd-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="299cd-145">a.</span><span class="sxs-lookup"><span data-stu-id="299cd-145">a.</span></span> <span data-ttu-id="299cd-146">按一下**下載**toodownload hello 公用中繼資料檔案，然後將它儲存在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="299cd-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="299cd-147">b.</span><span class="sxs-lookup"><span data-stu-id="299cd-147">b.</span></span> <span data-ttu-id="299cd-148">開啟 hello 中繼資料檔案，然後再找出 hello **AssertionConsumerService**節點。</span><span class="sxs-lookup"><span data-stu-id="299cd-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="299cd-149">![判斷提示取用者服務](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "判斷提示取用者服務")</span><span class="sxs-lookup"><span data-stu-id="299cd-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="299cd-150">c.</span><span class="sxs-lookup"><span data-stu-id="299cd-150">c.</span></span> <span data-ttu-id="299cd-151">複製 hello **AssertionConsumerService**值。</span><span class="sxs-lookup"><span data-stu-id="299cd-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="299cd-152">您將需要 hello 中 hello 值**設定應用程式 URL**稍後在本教學課程 > 一節。</span><span class="sxs-lookup"><span data-stu-id="299cd-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="299cd-153">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **Azure 傳統入口網站** 。</span><span class="sxs-lookup"><span data-stu-id="299cd-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="299cd-154">在 hello **TOPdesk-Secure**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello * * 設定單一登入 * * 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="299cd-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="299cd-155">![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="299cd-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="299cd-156">在 hello**如何將您像使用者 toosign 上 tooTOPdesk-安全**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="299cd-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="299cd-157">![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="299cd-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="299cd-158">在 hello**設定應用程式 URL**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="299cd-159">![設定應用程式 URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="299cd-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="299cd-160">a.</span><span class="sxs-lookup"><span data-stu-id="299cd-160">a.</span></span> <span data-ttu-id="299cd-161">在 hello **TOPdesk-Secure 登入 URL**文字方塊中，供使用者 toosign 入 TOPdesk-安全的應用程式的型別 hello URL (例如:"*https://qssolutions.topdesk.net*")。</span><span class="sxs-lookup"><span data-stu-id="299cd-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="299cd-162">b.</span><span class="sxs-lookup"><span data-stu-id="299cd-162">b.</span></span> <span data-ttu-id="299cd-163">在 hello **TOPdesk-Public 回覆 URL**文字方塊中，貼上 hello **TOPdesk-Secure AssertionConsumerService URL** (例如:"*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="299cd-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="299cd-164">c.</span><span class="sxs-lookup"><span data-stu-id="299cd-164">c.</span></span> <span data-ttu-id="299cd-165">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="299cd-165">Click **Next**.</span></span>

10. <span data-ttu-id="299cd-166">在 hello**於 TOPdesk-Secure 設定單一登入**頁面、 toodownload 中繼資料檔案，按一下 **下載中繼資料**，然後儲存在本機電腦上的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="299cd-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="299cd-167">![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="299cd-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="299cd-168">toocreate 憑證檔案，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="299cd-169">![憑證](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "憑證")</span><span class="sxs-lookup"><span data-stu-id="299cd-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="299cd-170">a.</span><span class="sxs-lookup"><span data-stu-id="299cd-170">a.</span></span> <span data-ttu-id="299cd-171">開啟 hello 下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="299cd-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="299cd-172">b.</span><span class="sxs-lookup"><span data-stu-id="299cd-172">b.</span></span> <span data-ttu-id="299cd-173">展開 hello **RoleDescriptor**節點具有**xsi: type**的**fed: ApplicationServiceType**。</span><span class="sxs-lookup"><span data-stu-id="299cd-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="299cd-174">c.</span><span class="sxs-lookup"><span data-stu-id="299cd-174">c.</span></span> <span data-ttu-id="299cd-175">複製 hello hello 值**X509Certificate**節點。</span><span class="sxs-lookup"><span data-stu-id="299cd-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="299cd-176">d.</span><span class="sxs-lookup"><span data-stu-id="299cd-176">d.</span></span> <span data-ttu-id="299cd-177">複製儲存 hello **X509Certificate**在檔案中的電腦上本機值。</span><span class="sxs-lookup"><span data-stu-id="299cd-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="299cd-178">在您 TOPdesk-Secure 公司網站，請在 hello **TOPdesk**功能表上，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="299cd-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="299cd-179">![設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "設定")</span><span class="sxs-lookup"><span data-stu-id="299cd-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="299cd-180">按一下 [登入設定] 。</span><span class="sxs-lookup"><span data-stu-id="299cd-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="299cd-181">![登入設定](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "登入設定")</span><span class="sxs-lookup"><span data-stu-id="299cd-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="299cd-182">展開 hello**登入設定**功能表，然後再按一下**一般**。</span><span class="sxs-lookup"><span data-stu-id="299cd-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="299cd-183">![一般](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "一般")</span><span class="sxs-lookup"><span data-stu-id="299cd-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="299cd-184">在 hello**公用**區段中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="299cd-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="299cd-185">![新增](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "新增")</span><span class="sxs-lookup"><span data-stu-id="299cd-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="299cd-186">在 hello **SAML 設定助理**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="299cd-187">![SAML 組態輔助程式](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML 組態輔助程式")</span><span class="sxs-lookup"><span data-stu-id="299cd-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="299cd-188">a.</span><span class="sxs-lookup"><span data-stu-id="299cd-188">a.</span></span> <span data-ttu-id="299cd-189">在您下載的中繼資料檔案的 tooupload**同盟中繼資料**，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="299cd-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="299cd-190">b.</span><span class="sxs-lookup"><span data-stu-id="299cd-190">b.</span></span> <span data-ttu-id="299cd-191">在您的憑證檔案的 tooupload**憑證 (RSA)**，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="299cd-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="299cd-192">c.</span><span class="sxs-lookup"><span data-stu-id="299cd-192">c.</span></span> <span data-ttu-id="299cd-193">所得 hello TOPdesk 支援小組，底下 tooupload hello 標誌檔**標誌圖示**，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="299cd-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="299cd-194">d.</span><span class="sxs-lookup"><span data-stu-id="299cd-194">d.</span></span> <span data-ttu-id="299cd-195">在 hello**使用者名稱屬性**文字方塊中，輸入**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。</span><span class="sxs-lookup"><span data-stu-id="299cd-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="299cd-196">e.</span><span class="sxs-lookup"><span data-stu-id="299cd-196">e.</span></span> <span data-ttu-id="299cd-197">在 hello**顯示名稱**文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="299cd-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="299cd-198">f.</span><span class="sxs-lookup"><span data-stu-id="299cd-198">f.</span></span> <span data-ttu-id="299cd-199">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="299cd-199">Click **Save**.</span></span>

17. <span data-ttu-id="299cd-200">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="299cd-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="299cd-201">![設定單一登入](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="299cd-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="299cd-202">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="299cd-202">Configuring user provisioning</span></span>
<span data-ttu-id="299cd-203">順序 tooenable Azure AD 使用者 toolog 到 TOPdesk-在安全的它們必須佈建到 TOPdesk-Secure。</span><span class="sxs-lookup"><span data-stu-id="299cd-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="299cd-204">在 TOPdesk-的案例中 hello 安全，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="299cd-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="299cd-205">tooconfigure 使用者佈建，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="299cd-206">登入 tooyour **TOPdesk-Secure**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="299cd-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="299cd-207">在 hello 最上層顯示 hello 功能表上，按一下**TOPdesk\>新增\>支援檔案\>運算子**。</span><span class="sxs-lookup"><span data-stu-id="299cd-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="299cd-208">![操作員](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "操作員")</span><span class="sxs-lookup"><span data-stu-id="299cd-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="299cd-209">在 [hello **New 運算子**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="299cd-210">![新增操作員](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "新增操作員")</span><span class="sxs-lookup"><span data-stu-id="299cd-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="299cd-211">a.</span><span class="sxs-lookup"><span data-stu-id="299cd-211">a.</span></span> <span data-ttu-id="299cd-212">按一下 hello 一般索引標籤。</span><span class="sxs-lookup"><span data-stu-id="299cd-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="299cd-213">b.</span><span class="sxs-lookup"><span data-stu-id="299cd-213">b.</span></span> <span data-ttu-id="299cd-214">在 hello**姓氏**文字方塊中的 hello**一般**> 一節中，輸入您想要 tooprovision 之有效 Azure Active Directory 帳戶 hello 最後一個名稱。</span><span class="sxs-lookup"><span data-stu-id="299cd-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="299cd-215">c.</span><span class="sxs-lookup"><span data-stu-id="299cd-215">c.</span></span> <span data-ttu-id="299cd-216">選取**網站**hello hello 帳戶**位置**> 一節。</span><span class="sxs-lookup"><span data-stu-id="299cd-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="299cd-217">d.</span><span class="sxs-lookup"><span data-stu-id="299cd-217">d.</span></span> <span data-ttu-id="299cd-218">在 hello**登入名稱**文字方塊中的 hello **TOPdesk 登入**區段中，輸入您使用者的登入名稱。</span><span class="sxs-lookup"><span data-stu-id="299cd-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="299cd-219">e.</span><span class="sxs-lookup"><span data-stu-id="299cd-219">e.</span></span> <span data-ttu-id="299cd-220">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="299cd-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="299cd-221">您可以使用任何其他 TOPdesk-Secure 使用者帳戶建立工具或 Api 提供 TOPdesk-Secure tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="299cd-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="299cd-222">指派使用者</span><span class="sxs-lookup"><span data-stu-id="299cd-222">Assigning users</span></span>
<span data-ttu-id="299cd-223">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="299cd-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="299cd-224">tooassign 使用者 tooTOPdesk-Secure，請執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="299cd-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="299cd-225">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="299cd-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="299cd-226">在 hello * * TOPdesk-Secure * * 應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="299cd-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="299cd-227">![指派使用者](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="299cd-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="299cd-228">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="299cd-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="299cd-229">![是](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="299cd-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="299cd-230">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="299cd-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="299cd-231">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="299cd-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

