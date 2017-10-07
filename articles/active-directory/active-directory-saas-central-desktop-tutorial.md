---
title: "教學課程：Azure Active Directory 與 Central Desktop 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Central Desktop 單一登入、 自動化佈建，以及更多 ！"
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
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="4cbfe-103">教學課程：Azure Active Directory 與 Central Desktop 整合</span><span class="sxs-lookup"><span data-stu-id="4cbfe-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="4cbfe-104">本教學課程的 hello 目標是 Azure 與 Central Desktop tooshow hello 整合。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="4cbfe-105">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="4cbfe-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="4cbfe-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="4cbfe-106">A valid Azure subscription</span></span>
* <span data-ttu-id="4cbfe-107">啟用 Central Desktop 單一登入的訂用帳戶/Central Desktop 租用戶</span><span class="sxs-lookup"><span data-stu-id="4cbfe-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="4cbfe-108">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="4cbfe-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="4cbfe-109">啟用 Central Desktop 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="4cbfe-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="4cbfe-110">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="4cbfe-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="4cbfe-111">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="4cbfe-111">Configuring user provisioning</span></span>
* <span data-ttu-id="4cbfe-112">指派使用者</span><span class="sxs-lookup"><span data-stu-id="4cbfe-112">Assigning users</span></span>

<span data-ttu-id="4cbfe-113">![案例](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "案例")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="4cbfe-114">啟用 Central Desktop 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="4cbfe-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="4cbfe-115">本節 hello 目標是 toooutline 如何 Central Desktop tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="4cbfe-116">**tooenable hello 應用程式整合 Central desktop，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4cbfe-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cbfe-117">在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="4cbfe-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="4cbfe-119">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="4cbfe-120">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="4cbfe-121">![應用程式](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="4cbfe-122">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="4cbfe-123">![新增應用程式](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="4cbfe-124">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="4cbfe-125">![從資源庫新增應用程式](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="4cbfe-126">在 hello**搜尋方塊**，型別**Central Desktop**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="4cbfe-127">![應用程式資源庫](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="4cbfe-128">在 hello 結果窗格中，選取  **Central Desktop**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="4cbfe-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="4cbfe-130">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="4cbfe-130">Configure single sign-on</span></span>

<span data-ttu-id="4cbfe-131">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooCentral 桌面的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="4cbfe-132">此程序的一部分，您就需要的 tooupload base 64 編碼的憑證 tooyour Central Desktop 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="4cbfe-133">如果您不熟悉這個程序，請參閱[如何 tooconvert 二進位憑證到文字檔](http://youtu.be/PlgrzUZ-Y1o)。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="4cbfe-134">**tooconfigure 單一登入，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4cbfe-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cbfe-135">在 Azure 傳統入口網站，在 hello hello **Central Desktop**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello * * 設定單一登入 * * 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="4cbfe-136">![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="4cbfe-137">在 hello**如何想您使用者 toosign tooCentral 桌面上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="4cbfe-138">![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="4cbfe-139">在 hello**設定應用程式 URL**頁面上，執行下列步驟，hello，然後按一下**下一步**:</span><span class="sxs-lookup"><span data-stu-id="4cbfe-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="4cbfe-140">在 hello **Central Desktop 登入 URL**文字方塊中，您的 Central Desktop 租用戶的型別 hello URL (例如： *http://contoso.centraldesktop.com*)。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="4cbfe-141">在 [hello Central Desktop 回覆 URL] 文字方塊中，輸入您的 Central Desktop AssertionConsumerService URL (例如： https://contoso.centraldesktop.com/saml2-assertion.php)。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="4cbfe-142">您可以從 hello central desktop 中繼資料取得 hello 值 (例如： *http://contoso.centraldesktop.com*)。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="4cbfe-143">![設定應用程式 URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="4cbfe-144">在 hello**於 Central Desktop 設定單一登入**頁面、 toodownload 憑證，請按一下**下載憑證**，然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="4cbfe-145">![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="4cbfe-146">登入 tooyour **Central Desktop**租用戶。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="4cbfe-147">跳過**設定**，按一下 **進階**，然後按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="4cbfe-148">![設定 - 進階](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "設定 - 進階")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="4cbfe-149">在 hello**單一登入設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4cbfe-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="4cbfe-150">![單一登入設定](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "單一登入設定")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="4cbfe-151">選取 [啟用 SAML v2 單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="4cbfe-152">在 Azure 傳統入口網站，在 hello hello**於 Central Desktop 設定單一登入**頁面上，複製 hello**簽發者 URL**值並貼到 hello **SSO URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="4cbfe-153">在 Azure 傳統入口網站，在 hello hello**於 Central Desktop 設定單一登入**頁面上，複製 hello**遠端登入 URL**值並貼到 hello **SSO 登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="4cbfe-154">在 Azure 傳統入口網站，在 hello hello**於 Central Desktop 設定單一登入**頁面上，複製 hello**單一登出服務 URL**值並貼到 hello **SSO 登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="4cbfe-155">在 hello**訊息簽章驗證方法**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4cbfe-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="4cbfe-156">![訊息簽章驗證方法](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "訊息簽章驗證方法")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="4cbfe-157">選取 [憑證] 。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="4cbfe-158">從 hello **SSO 憑證**清單中，選取**RSH SHA256**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="4cbfe-159">從 hello 下載的憑證，複製 hello 內容的 hello 文字檔案，請建立文字檔，然後將它貼到 hello **SSO 憑證**欄位。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="4cbfe-160">如需詳細資訊，請參閱[如何 tooconvert 二進位憑證到文字檔案](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="4cbfe-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="4cbfe-161">選取**顯示連結 tooyour SAMLv2 登入頁面**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="4cbfe-162">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-162">Click **Update**.</span></span>
10. <span data-ttu-id="4cbfe-163">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="4cbfe-164">![設定單一登入](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="4cbfe-165">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="4cbfe-165">Configure user provisioning</span></span>

<span data-ttu-id="4cbfe-166">AAD 使用者 toobe 無法 toosign 中，它們必須已佈建的 toohello Central Desktop 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="4cbfe-167">本章節描述如何 toocreate AAD 使用者帳戶在 Central Desktop。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="4cbfe-168">**使用者帳戶 tooCentral 桌面 tooprovision:**</span><span class="sxs-lookup"><span data-stu-id="4cbfe-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="4cbfe-169">登入 tooyour Central Desktop 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="4cbfe-170">跳過**人員\>內部成員**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="4cbfe-171">按一下 [加入內部成員] 。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="4cbfe-172">![人員](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "人員")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="4cbfe-173">在 hello**新成員的電子郵件地址**文字方塊中，輸入您想 tooprovision，，然後按一下的 AAD 帳戶**下一步**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="4cbfe-174">![新成員的電子郵件地址](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "新成員的電子郵件地址")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="4cbfe-175">按一下 [加入內部成員] 。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="4cbfe-176">![加入內部成員](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "加入內部成員")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="4cbfe-177">您加入的 hello 使用者會收到電子郵件，其中包含確認連結需要他們點 tooclick tooactivate hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="4cbfe-178">您可以使用任何其他 Central Desktop 使用者帳戶建立工具或 Api 提供 Central Desktop tooprovision AAD 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="4cbfe-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="4cbfe-179">指派使用者</span><span class="sxs-lookup"><span data-stu-id="4cbfe-179">Assign users</span></span>
<span data-ttu-id="4cbfe-180">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="4cbfe-181">**tooassign 使用者 tooCentral Desktop 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4cbfe-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cbfe-182">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="4cbfe-183">在 hello **Central Desktop**應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="4cbfe-184">![指派使用者](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="4cbfe-185">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="4cbfe-186">![是](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="4cbfe-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="4cbfe-187">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="4cbfe-188">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="4cbfe-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

