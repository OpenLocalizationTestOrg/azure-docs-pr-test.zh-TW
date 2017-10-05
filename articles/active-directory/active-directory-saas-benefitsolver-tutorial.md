---
title: "教學課程：Azure Active Directory 與 Benefitsolver 整合 | Microsoft Docs"
description: "了解如何使用 Benefitsolver 搭配 Azure Active Directory 來啟用單一登入、自動化佈建和更多功能！"
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
ms.openlocfilehash: 8a13dd5ebd872f86247158379b28bc291a9c9d83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="80732-103">教學課程：Azure Active Directory 與 Benefitsolver 整合</span><span class="sxs-lookup"><span data-stu-id="80732-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="80732-104">本教學課程的目的是要示範 Azure 與 Benefitsolver 的整合。</span><span class="sxs-lookup"><span data-stu-id="80732-104">The objective of this tutorial is to show the integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="80732-105">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="80732-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="80732-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="80732-106">A valid Azure subscription</span></span>
* <span data-ttu-id="80732-107">已啟用 Benefitsolver 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="80732-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="80732-108">完成本教學課程之後，您指派給 Benefitsolver 的 Azure AD 使用者就能夠單一登入應用程式或是使用 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="80732-108">After completing this tutorial, the Azure AD users you have assigned to Benefitsolver will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="80732-109">本教學課程中說明的案例由下列建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="80732-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="80732-110">啟用 Benefitsolver 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="80732-110">Enabling the application integration for Benefitsolver</span></span>
2. <span data-ttu-id="80732-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="80732-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="80732-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="80732-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="80732-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="80732-113">Assigning users</span></span>

<span data-ttu-id="80732-114">![案例](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "案例")</span><span class="sxs-lookup"><span data-stu-id="80732-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-benefitsolver"></a><span data-ttu-id="80732-115">啟用 Benefitsolver 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="80732-115">Enabling the application integration for Benefitsolver</span></span>
<span data-ttu-id="80732-116">本節的目的是要說明如何啟用 Benefitsolver 的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="80732-116">The objective of this section is to outline how to enable the application integration for Benefitsolver.</span></span>

### <a name="to-enable-the-application-integration-for-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="80732-117">若要啟用 Benefitsolver 的應用程式整合，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="80732-117">To enable the application integration for Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="80732-118">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="80732-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="80732-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="80732-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="80732-120">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="80732-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="80732-121">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="80732-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="80732-122">![應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="80732-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="80732-123">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="80732-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="80732-124">![新增應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="80732-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="80732-125">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="80732-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="80732-126">![從資源庫新增應用程式](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="80732-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="80732-127">在**搜尋方塊**中，輸入 **Benefitsolver**。</span><span class="sxs-lookup"><span data-stu-id="80732-127">In the **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="80732-128">![應用程式資源庫](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="80732-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="80732-129">在結果窗格中，選取 [Benefitsolver]，然後按一下 [完成] 以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="80732-129">In the results pane, select **Benefitsolver**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="80732-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="80732-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="80732-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="80732-131">Configure single sign-on</span></span>

<span data-ttu-id="80732-132">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶驗證至 Benefitsolver 。</span><span class="sxs-lookup"><span data-stu-id="80732-132">The objective of this section is to outline how to enable users to authenticate to Benefitsolver with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="80732-133">Benefitsolver 應用程式需要特定格式的 SAML 判斷提示，因此您必須將自訂屬性對應加入 **SAML Token 屬性** 組態。</span><span class="sxs-lookup"><span data-stu-id="80732-133">Your Benefitsolver application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **saml token attributes** configuration.</span></span> 

<span data-ttu-id="80732-134">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="80732-134">The following screenshot shows an example for this.</span></span>

<span data-ttu-id="80732-135">![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="80732-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="80732-136">**若要設定單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="80732-136">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="80732-137">在 Azure 傳統入口網站的 **Benefitsolver** 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80732-137">In the Azure classic portal, on the **Benefitsolver** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="80732-138">![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="80732-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="80732-139">在 [要如何讓使用者登入 Benefitsolver] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="80732-139">On the **How would you like users to sign on to Benefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="80732-140">![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="80732-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="80732-141">在 [設定應用程式設定]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="80732-141">On the **Configure App Settings** page, perform the following steps:</span></span>
   
   <span data-ttu-id="80732-142">![設定應用程式設定](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "進行應用程式設定")</span><span class="sxs-lookup"><span data-stu-id="80732-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="80732-143">在 [登入 URL] 文字方塊中，輸入：**http://azure.benefitsolver.com**。</span><span class="sxs-lookup"><span data-stu-id="80732-143">In the **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="80732-144">在 [回覆 URL] 文字方塊中，輸入 **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**。</span><span class="sxs-lookup"><span data-stu-id="80732-144">In the **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="80732-145">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="80732-145">Click **Next**.</span></span>
4. <span data-ttu-id="80732-146">在 [設定在 Benefitsolver 單一登入] 頁面上，按一下 [下載中繼資料] 以下載您的中繼資料，然後將中繼資料檔儲存在您的本機電腦中。</span><span class="sxs-lookup"><span data-stu-id="80732-146">On the **Configure single sign-on at Benefitsolver** page, to download your metadata, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="80732-147">![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="80732-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="80732-148">將下載的中繼資料檔傳送給 Benefitsolver 支援小組。</span><span class="sxs-lookup"><span data-stu-id="80732-148">Send the downloaded metadata file to your Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="80732-149">Benefitsolver 支援小組必須執行實際的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="80732-149">Your Benefitsolver support team has to do the actual SSO configuration.</span></span> <span data-ttu-id="80732-150">當您的訂用帳戶啟用 SSO 之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="80732-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="80732-151">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80732-151">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="80732-152">![設定單一登入](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="80732-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="80732-153">在頂端的功能表中，按一下 [屬性] **屬性** to open the **SAML Token 屬性** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="80732-153">In the menu on the top, click **Attributes** to open the **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="80732-154">![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="80732-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="80732-155">若要加入必要的屬性對應，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="80732-155">To add the required attribute mappings, perform the following steps:</span></span>
   
   <span data-ttu-id="80732-156">![屬性](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="80732-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="80732-157">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="80732-157">Attribute Name</span></span> | <span data-ttu-id="80732-158">屬性值</span><span class="sxs-lookup"><span data-stu-id="80732-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="80732-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="80732-159">ClientID</span></span> |<span data-ttu-id="80732-160">您需要向 Benefitsolver 支援小組取得這個值。</span><span class="sxs-lookup"><span data-stu-id="80732-160">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="80732-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="80732-161">ClientKey</span></span> |<span data-ttu-id="80732-162">您需要向 Benefitsolver 支援小組取得這個值。</span><span class="sxs-lookup"><span data-stu-id="80732-162">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="80732-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="80732-163">LogoutURL</span></span> |<span data-ttu-id="80732-164">您需要向 Benefitsolver 支援小組取得這個值。</span><span class="sxs-lookup"><span data-stu-id="80732-164">You need to get this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="80732-165">EmployeeID</span><span class="sxs-lookup"><span data-stu-id="80732-165">EmployeeID</span></span> |<span data-ttu-id="80732-166">您需要向 Benefitsolver 支援小組取得這個值。</span><span class="sxs-lookup"><span data-stu-id="80732-166">You need to get this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="80732-167">針對上表中的每個資料列，按一下 [加入使用者屬性] 。</span><span class="sxs-lookup"><span data-stu-id="80732-167">For each data row in the table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="80732-168">在 [屬性名稱]  文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="80732-168">In the **Attribute Name** textbox, type the attribute name shown for that row.</span></span>
   3. <span data-ttu-id="80732-169">在 [屬性值]  文字方塊中，選取該資料列所顯示的屬性值。</span><span class="sxs-lookup"><span data-stu-id="80732-169">In the **Attribute Value** textbox, select the attribute value shown for that row.</span></span>
   4. <span data-ttu-id="80732-170">按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="80732-170">Click **Complete**.</span></span>
9. <span data-ttu-id="80732-171">按一下 [套用變更] 。</span><span class="sxs-lookup"><span data-stu-id="80732-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="80732-172">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="80732-172">Configure user provisioning</span></span>
<span data-ttu-id="80732-173">若要讓 Azure AD 使用者可以登入 Benefitsolver，必須將他們佈建到 Benefitsolver。</span><span class="sxs-lookup"><span data-stu-id="80732-173">In order to enable Azure AD users to log into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="80732-174">在 Benefitsolver 案例中，員工資料是透過您的 HRIS 系統的普查檔案填入應用程式中 (通常是每晚)。</span><span class="sxs-lookup"><span data-stu-id="80732-174">In the case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="80732-175">您可以使用任何其他的 Benefitsolver 使用者帳戶建立工具或 Benefitsolver 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="80732-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver to provision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="80732-176">指派使用者</span><span class="sxs-lookup"><span data-stu-id="80732-176">Assigning users</span></span>
<span data-ttu-id="80732-177">若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。</span><span class="sxs-lookup"><span data-stu-id="80732-177">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

### <a name="to-assign-users-to-benefitsolver-perform-the-following-steps"></a><span data-ttu-id="80732-178">若要將使用者指派給 Benefitsolver，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="80732-178">To assign users to Benefitsolver, perform the following steps:</span></span>
1. <span data-ttu-id="80732-179">在 Azure 傳統入口網站中建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="80732-179">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="80732-180">在 * * Benefitsolver * * 應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="80732-180">On the **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="80732-181">![指派使用者](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="80732-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="80732-182">選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。</span><span class="sxs-lookup"><span data-stu-id="80732-182">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="80732-183">![是](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="80732-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="80732-184">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="80732-184">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="80732-185">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="80732-185">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

