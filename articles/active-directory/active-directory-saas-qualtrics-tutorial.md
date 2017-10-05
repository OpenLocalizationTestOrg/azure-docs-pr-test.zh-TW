---
title: "教學課程：Azure Active Directory 與 Qualtrics 整合 | Microsoft Docs"
description: "了解如何使用 Qualtrics 搭配 Azure Active Directory 來啟用單一登入、自動佈建和更多功能！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 2fcde595a40dafda7549f5bccb582b57585b314e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="17e56-103">教學課程：Azure Active Directory 與 Qualtrics 整合</span><span class="sxs-lookup"><span data-stu-id="17e56-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="17e56-104">本教學課程的目的是要示範 Azure 與 Qualtrics 的整合。</span><span class="sxs-lookup"><span data-stu-id="17e56-104">The objective of this tutorial is to show the integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="17e56-105">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="17e56-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="17e56-106">有效的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="17e56-106">A valid Azure subscription</span></span>
* <span data-ttu-id="17e56-107">已啟用 Qualtrics 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="17e56-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="17e56-108">完成本教學課程之後，您指派給 Qualtrics 的 Azure AD 使用者就能夠從您的 Qualtrics 公司網站 (服務提供者起始登入)，或使用 [存取面板](active-directory-saas-access-panel-introduction.md)來單一登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e56-108">After completing this tutorial, the Azure AD users you have assigned to Qualtrics will be able to single sign into the application at your Qualtrics company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="17e56-109">本教學課程中說明的案例由下列建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="17e56-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="17e56-110">啟用 Qualtrics 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="17e56-110">Enabling the application integration for Qualtrics</span></span>
2. <span data-ttu-id="17e56-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="17e56-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="17e56-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="17e56-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="17e56-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="17e56-113">Assigning users</span></span>

<span data-ttu-id="17e56-114">![案例](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "案例")</span><span class="sxs-lookup"><span data-stu-id="17e56-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-qualtrics"></a><span data-ttu-id="17e56-115">啟用 Qualtrics 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="17e56-115">Enabling the application integration for Qualtrics</span></span>
<span data-ttu-id="17e56-116">本節的目的是要說明如何啟用 Qualtrics 的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="17e56-116">The objective of this section is to outline how to enable the application integration for Qualtrics.</span></span>

<span data-ttu-id="17e56-117">**若要啟用 Qualtrics 的應用程式整合，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="17e56-117">**To enable the application integration for Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="17e56-118">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="17e56-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="17e56-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="17e56-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="17e56-120">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="17e56-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="17e56-121">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="17e56-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="17e56-122">![應用程式](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="17e56-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="17e56-123">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="17e56-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="17e56-124">![新增應用程式](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="17e56-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="17e56-125">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="17e56-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="17e56-126">![從資源庫新增應用程式](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="17e56-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="17e56-127">在**搜尋方塊**中，輸入 **Qualtrics**。</span><span class="sxs-lookup"><span data-stu-id="17e56-127">In the **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="17e56-128">![應用程式資源庫](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="17e56-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="17e56-129">在結果窗格中，選取 [Qualtrics]，然後按一下 [完成] 來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="17e56-129">In the results pane, select **Qualtrics**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="17e56-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="17e56-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="17e56-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="17e56-131">Configure single sign-on</span></span>

<span data-ttu-id="17e56-132">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶驗證到 Qualtrics。</span><span class="sxs-lookup"><span data-stu-id="17e56-132">The objective of this section is to outline how to enable users to authenticate to Qualtrics with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="17e56-133">**若要設定單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="17e56-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="17e56-134">在 Azure 傳統入口網站的 [Qualtrics] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="17e56-134">In the Azure classic portal, on the **Qualtrics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="17e56-135">![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="17e56-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="17e56-136">在 [要如何讓使用者登入 Qualtrics] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="17e56-136">On the **How would you like users to sign on to Qualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="17e56-137">![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="17e56-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="17e56-138">在 [設定應用程式 URL] 頁面的 [Qualtrics 登入 URL] 文字方塊中，輸入您的 URL (例如：“ https://ssotest2ut1.qualtrics.com ")，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="17e56-138">On the **Configure App URL** page, in the **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="17e56-139">![設定應用程式 URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="17e56-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="17e56-140">在 [設定在 Qualtrics 單一登入] 頁面上，按一下 [下載中繼資料]，然後將中繼資料檔儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="17e56-140">On the **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save the metadata file on your computer.</span></span>
   
   <span data-ttu-id="17e56-141">![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="17e56-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="17e56-142">將中繼資料檔傳送至 Qualtrics 支援小組。</span><span class="sxs-lookup"><span data-stu-id="17e56-142">Send the metadata file to the Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="17e56-143">SSO 設定必須由 Qualtrics 支援小組執行。</span><span class="sxs-lookup"><span data-stu-id="17e56-143">The SSO configuration has to be performed by the Qualtrics support team.</span></span> <span data-ttu-id="17e56-144">設定完成後，您將會收到通知。</span><span class="sxs-lookup"><span data-stu-id="17e56-144">You will get a notification as soon as the configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="17e56-145">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="17e56-145">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="17e56-146">![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="17e56-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="17e56-147">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="17e56-147">Configure user provisioning</span></span>

<span data-ttu-id="17e56-148">沒有動作項目可讓您設定 Qualtrics 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="17e56-148">There is no action item for you to configure user provisioning to Qualtrics.</span></span> <span data-ttu-id="17e56-149">當指派的使用者透過存取面板嘗試登入 Qualtrics 時，Qualtrics 會檢查使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="17e56-149">When an assigned user tries to log into Qualtrics using the access panel, Qualtrics checks whether the user exists.</span></span>  

<span data-ttu-id="17e56-150">如果尚無可用的使用者帳戶，Qualtrics 就會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="17e56-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="17e56-151">指派使用者</span><span class="sxs-lookup"><span data-stu-id="17e56-151">Assign users</span></span>
<span data-ttu-id="17e56-152">若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。</span><span class="sxs-lookup"><span data-stu-id="17e56-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="17e56-153">**若要將使用者指派給 Qualtrics，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="17e56-153">**To assign users to Qualtrics, perform the following steps:**</span></span>

1. <span data-ttu-id="17e56-154">在 Azure 傳統入口網站中建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="17e56-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="17e56-155">在 [Qualtrics] 應用程式整合頁面上，按一下 [指派使用者]。</span><span class="sxs-lookup"><span data-stu-id="17e56-155">On the **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="17e56-156">![指派使用者](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="17e56-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="17e56-157">選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。</span><span class="sxs-lookup"><span data-stu-id="17e56-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="17e56-158">![是](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="17e56-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="17e56-159">如果要測試您的 SSO 設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="17e56-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="17e56-160">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="17e56-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

