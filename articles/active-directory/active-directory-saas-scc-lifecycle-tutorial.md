---
title: "教學課程：Azure Active Directory 與 SCC LifeCycle 整合 | Microsoft Docs"
description: "了解如何使用 SCC LifeCycle 搭配 Azure Active Directory 來啟用單一登入、自動佈建和更多功能！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a30bcca720ff135d0180d73f46e78403e9bca43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="dd0ad-103">教學課程：Azure Active Directory 與 SCC LifeCycle 整合</span><span class="sxs-lookup"><span data-stu-id="dd0ad-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="dd0ad-104">本教學課程的目的是要示範 Azure 與 SCC LifeCycle 的整合。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="dd0ad-105">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="dd0ad-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="dd0ad-106">有效的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dd0ad-106">A valid Azure subscription</span></span>
* <span data-ttu-id="dd0ad-107">已啟用 SCC LifeCycle 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dd0ad-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="dd0ad-108">完成本教學課程之後，您指派給 SCC LifeCycle 的 Azure AD 使用者就能夠單一登入您 SCC LifeCycle 公司網站 (服務提供者起始登入) 的應用程式，或是使用 [存取面板簡介](active-directory-saas-access-panel-introduction.md)進行單一登入。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="dd0ad-109">本教學課程中說明的案例由下列建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="dd0ad-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="dd0ad-110">啟用 SCC LifeCycle 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="dd0ad-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="dd0ad-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="dd0ad-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="dd0ad-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="dd0ad-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="dd0ad-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="dd0ad-113">Assigning users</span></span>

<span data-ttu-id="dd0ad-114">![案例](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "案例")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="dd0ad-115">啟用 SCC LifeCycle 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="dd0ad-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="dd0ad-116">本節的目的是要說明如何啟用 SCC LifeCycle 的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="dd0ad-117">**若要啟用 SCC LifeCycle 的應用程式整合，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dd0ad-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="dd0ad-118">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="dd0ad-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="dd0ad-120">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="dd0ad-121">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="dd0ad-122">![應用程式](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="dd0ad-123">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="dd0ad-124">![新增應用程式](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="dd0ad-125">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="dd0ad-126">![從資源庫新增應用程式](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="dd0ad-127">在 [搜尋] 對話方塊中，輸入 **SCC LifeCycle**。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="dd0ad-128">![應用程式資源庫](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="dd0ad-129">在結果窗格中，選取 [SCC LifeCycle]，然後按一下 [完成] 來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="dd0ad-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="dd0ad-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="dd0ad-131">Configure single sign-on</span></span>

<span data-ttu-id="dd0ad-132">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己在 Azure AD 中的帳戶在 SCC LifeCycle 中進行驗證。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="dd0ad-133">**若要設定單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dd0ad-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="dd0ad-134">在 Azure 傳統入口網站的 [SCC LifeCycle] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="dd0ad-135">![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="dd0ad-136">在 [要如何讓使用者登入 SCC LifeCycle] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="dd0ad-137">![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="dd0ad-138">在 [設定應用程式 URL] 頁面的 [登入 URL] 文字方塊中，使用下列模式輸入使用者用來登入 SCC LifeCycle 應用程式的 URL："https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx"，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="dd0ad-139">![設定應用程式 URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="dd0ad-140">在 [設定在 SCC LifeCycle 單一登入] 頁面上，按一下 [下載中繼資料]，然後將中繼資料檔儲存在您的本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="dd0ad-141">![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="dd0ad-142">將該中繼資料檔轉寄給 SCC LifeCycle 支援小組。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="dd0ad-143">單一登入必須由 SCC LifeCycle 支援小組啟用。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="dd0ad-144">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="dd0ad-145">![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="dd0ad-146">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="dd0ad-146">Configure user provisioning</span></span>

<span data-ttu-id="dd0ad-147">若要讓 Azure AD 使用者可以登入 SCC LifeCycle，則必須將他們佈建至 SCC LifeCycle。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="dd0ad-148">沒有動作項目可讓您設定 SCC LifeCycle 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="dd0ad-149">當受指派使用者嘗試登入 SCC LifeCycle 時，則會自動建立一個 SCC LifeCycle 帳戶 (如有必要)。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="dd0ad-150">您可以使用任何其他的 SCC LifeCycle 使用者帳戶建立工具或 SCC LifeCycle 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="dd0ad-151">指派使用者</span><span class="sxs-lookup"><span data-stu-id="dd0ad-151">Assign users</span></span>
<span data-ttu-id="dd0ad-152">若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="dd0ad-153">**若要將使用者指派給 SCC LifeCycle，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dd0ad-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="dd0ad-154">在 Azure 傳統入口網站中建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="dd0ad-155">在 [SCC LifeCycle] 應用程式整合頁面上，按一下 [指派使用者]。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-155">On the **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="dd0ad-156">![指派使用者](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="dd0ad-157">選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="dd0ad-158">![是](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="dd0ad-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="dd0ad-159">如果要測試您的 SSO 設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="dd0ad-160">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="dd0ad-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

