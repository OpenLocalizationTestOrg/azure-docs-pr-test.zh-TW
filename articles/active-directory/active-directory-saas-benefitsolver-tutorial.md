---
title: "教學課程：Azure Active Directory 與 Benefitsolver 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Benefitsolver 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="df242-103">教學課程：Azure Active Directory 與 Benefitsolver 整合</span><span class="sxs-lookup"><span data-stu-id="df242-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="df242-104">本教學課程的 hello 目標是 Azure 與 Benefitsolver tooshow hello 整合。</span><span class="sxs-lookup"><span data-stu-id="df242-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="df242-105">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="df242-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="df242-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="df242-106">A valid Azure subscription</span></span>
* <span data-ttu-id="df242-107">已啟用 Benefitsolver 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="df242-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="df242-108">完成本教學課程之後, 您已指派 tooBenefitsolver hello Azure AD 使用者將無法 toosingle 登入 hello 應用程式使用 hello[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="df242-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="df242-109">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="df242-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="df242-110">啟用 Benefitsolver hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="df242-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="df242-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="df242-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="df242-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="df242-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="df242-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="df242-113">Assigning users</span></span>

<span data-ttu-id="df242-114">![案例](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "案例")</span><span class="sxs-lookup"><span data-stu-id="df242-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="df242-115">啟用 Benefitsolver hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="df242-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="df242-116">本節 hello 目標是 toooutline 如何 Benefitsolver tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="df242-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="df242-117">tooenable hello 應用程式整合 Benefitsolver，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="df242-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="df242-118">在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="df242-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="df242-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="df242-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="df242-120">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="df242-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="df242-121">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="df242-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="df242-122">![應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="df242-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="df242-123">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="df242-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="df242-124">![新增應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="df242-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="df242-125">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="df242-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="df242-126">![從資源庫新增應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="df242-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="df242-127">在 hello**搜尋方塊**，型別**Benefitsolver**。</span><span class="sxs-lookup"><span data-stu-id="df242-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="df242-128">![應用程式資源庫](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="df242-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="df242-129">在 hello 結果窗格中，選取  **Benefitsolver**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="df242-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="df242-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="df242-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="df242-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="df242-131">Configure single sign-on</span></span>

<span data-ttu-id="df242-132">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooBenefitsolver 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="df242-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="df242-133">Benefitsolver 應用程式需要特定格式，這需要您 tooadd 自訂屬性對應 tooyour hello SAML 判斷提示**saml 權杖屬性**組態。</span><span class="sxs-lookup"><span data-stu-id="df242-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="df242-134">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="df242-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="df242-135">![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="df242-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="df242-136">**tooconfigure 單一登入，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="df242-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="df242-137">在 Azure 傳統入口網站，在 hello hello **Benefitsolver**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="df242-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="df242-138">![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="df242-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="df242-139">在 hello**如何想您使用者 toosign tooBenefitsolver 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="df242-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="df242-140">![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="df242-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="df242-141">在 hello**設定應用程式設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="df242-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="df242-142">![設定應用程式設定](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "進行應用程式設定")</span><span class="sxs-lookup"><span data-stu-id="df242-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="df242-143">在 hello**登入 URL**文字方塊中，輸入**http://azure.benefitsolver.com**。</span><span class="sxs-lookup"><span data-stu-id="df242-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="df242-144">在 hello**回覆 URL**文字方塊中，輸入**https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**。</span><span class="sxs-lookup"><span data-stu-id="df242-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="df242-145">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="df242-145">Click **Next**.</span></span>
4. <span data-ttu-id="df242-146">在 hello **Benefitsolver 在設定單一登入**頁面、 toodownload 中繼資料，按一下**下載中繼資料**，然後儲存在本機電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="df242-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="df242-147">![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="df242-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="df242-148">傳送嗨下載中繼資料檔案 tooyour Benefitsolver 支援小組。</span><span class="sxs-lookup"><span data-stu-id="df242-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="df242-149">您 Benefitsolver 的支援團隊已 toodo hello 實際 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="df242-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="df242-150">當您的訂用帳戶啟用 SSO 之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="df242-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="df242-151">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="df242-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="df242-152">![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="df242-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="df242-153">在 hello 最上層顯示 hello 功能表上，按一下**屬性**tooopen hello **SAML 權杖屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="df242-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="df242-154">![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="df242-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="df242-155">tooadd hello 必要屬性對應，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="df242-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="df242-156">![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="df242-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="df242-157">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="df242-157">Attribute Name</span></span> | <span data-ttu-id="df242-158">屬性值</span><span class="sxs-lookup"><span data-stu-id="df242-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="df242-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="df242-159">ClientID</span></span> |<span data-ttu-id="df242-160">您需要 tooget 這個值向 Benefitsolver 支援小組。</span><span class="sxs-lookup"><span data-stu-id="df242-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="df242-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="df242-161">ClientKey</span></span> |<span data-ttu-id="df242-162">您需要 tooget 這個值向 Benefitsolver 支援小組。</span><span class="sxs-lookup"><span data-stu-id="df242-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="df242-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="df242-163">LogoutURL</span></span> |<span data-ttu-id="df242-164">您需要 tooget 這個值向 Benefitsolver 支援小組。</span><span class="sxs-lookup"><span data-stu-id="df242-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="df242-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="df242-165">EmployeeID</span></span> |<span data-ttu-id="df242-166">您需要 tooget 這個值向 Benefitsolver 支援小組。</span><span class="sxs-lookup"><span data-stu-id="df242-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="df242-167">上述的 hello 資料表中每個資料列，按一下 **新增使用者屬性**。</span><span class="sxs-lookup"><span data-stu-id="df242-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="df242-168">在 hello**屬性名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="df242-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="df242-169">在 hello**屬性值**文字方塊中，顯示該資料列選取 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="df242-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="df242-170">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="df242-170">Click **Complete**.</span></span>
9. <span data-ttu-id="df242-171">按一下 [套用變更] 。</span><span class="sxs-lookup"><span data-stu-id="df242-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="df242-172">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="df242-172">Configure user provisioning</span></span>
<span data-ttu-id="df242-173">在訂單 tooenable Azure AD 使用者 toolog Benefitsolver 成，它們必須佈建到 Benefitsolver。</span><span class="sxs-lookup"><span data-stu-id="df242-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="df242-174">在的 Benefitsolver hello 案例中，員工資料是透過從 HRIS 系統 （通常每晚都會更新） 人口普查檔填入應用程式中。</span><span class="sxs-lookup"><span data-stu-id="df242-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="df242-175">您可以使用任何其他 Benefitsolver 使用者帳戶建立工具或 Api 提供 Benefitsolver tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="df242-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="df242-176">指派使用者</span><span class="sxs-lookup"><span data-stu-id="df242-176">Assigning users</span></span>
<span data-ttu-id="df242-177">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="df242-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="df242-178">tooassign 使用者 tooBenefitsolver，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="df242-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="df242-179">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="df242-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="df242-180">在 hello * * Benefitsolver * * 應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="df242-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="df242-181">![指派使用者](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="df242-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="df242-182">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="df242-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="df242-183">![是](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="df242-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="df242-184">如果您想 tootest 您的單一登入設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="df242-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="df242-185">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="df242-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

