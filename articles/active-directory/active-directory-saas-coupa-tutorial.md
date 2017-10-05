---
title: "教學課程：Azure Active Directory 與 Coupa 整合 | Microsoft Docs"
description: "了解如何使用 Coupa 搭配 Azure Active Directory 來啟用單一登入、自動化佈建和更多功能！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="dde70-103">教學課程：Azure Active Directory 與 Coupa 整合</span><span class="sxs-lookup"><span data-stu-id="dde70-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="dde70-104">本教學課程的目的是要示範 Azure 與 Coupa 的整合。</span><span class="sxs-lookup"><span data-stu-id="dde70-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="dde70-105">本教學課程中說明的案例假設您已經具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="dde70-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="dde70-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="dde70-106">A valid Azure subscription</span></span>
* <span data-ttu-id="dde70-107">已啟用 Coupa 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dde70-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="dde70-108">完成本教學課程之後，您指派給 Coupa 的 Azure AD 使用者就能夠使用使用 [存取面板簡介](active-directory-saas-access-panel-introduction.md)單一登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="dde70-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="dde70-109">本教學課程中說明的案例由下列建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="dde70-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="dde70-110">啟用 Coupa 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="dde70-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="dde70-111">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="dde70-111">Configuring single sign-on</span></span>
* <span data-ttu-id="dde70-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="dde70-112">Configuring user provisioning</span></span>
* <span data-ttu-id="dde70-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="dde70-113">Assigning users</span></span>

<span data-ttu-id="dde70-114">![案例](./media/active-directory-saas-coupa-tutorial/IC791897.png "案例")</span><span class="sxs-lookup"><span data-stu-id="dde70-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="dde70-115">啟用 Coupa 的應用程式整合</span><span class="sxs-lookup"><span data-stu-id="dde70-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="dde70-116">本節的目的是要說明如何啟用 Coupa 的應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="dde70-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="dde70-117">**若要啟用 Coupa 的應用程式整合，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dde70-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="dde70-118">在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。</span><span class="sxs-lookup"><span data-stu-id="dde70-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="dde70-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="dde70-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="dde70-120">從 [目錄]  清單中，選取要啟用目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="dde70-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="dde70-121">若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。</span><span class="sxs-lookup"><span data-stu-id="dde70-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="dde70-122">![應用程式](./media/active-directory-saas-coupa-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="dde70-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="dde70-123">按一下頁面底部的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="dde70-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="dde70-124">![新增應用程式](./media/active-directory-saas-coupa-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="dde70-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="dde70-125">在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。</span><span class="sxs-lookup"><span data-stu-id="dde70-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="dde70-126">![從資源庫新增應用程式](./media/active-directory-saas-coupa-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="dde70-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="dde70-127">在**搜尋方塊**中，輸入 **Coupa**。</span><span class="sxs-lookup"><span data-stu-id="dde70-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="dde70-128">![應用程式資源庫](./media/active-directory-saas-coupa-tutorial/IC791898.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="dde70-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="dde70-129">在結果窗格中，選取 [Coupa]，然後按一下 [完成] 來加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="dde70-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="dde70-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="dde70-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="dde70-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="dde70-131">Configure single sign-on</span></span>

<span data-ttu-id="dde70-132">本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己的 Azure AD 帳戶驗證到 Coupa。</span><span class="sxs-lookup"><span data-stu-id="dde70-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="dde70-133">設定 Coupa 的單一登入需要您從憑證擷取憑證指紋值。</span><span class="sxs-lookup"><span data-stu-id="dde70-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="dde70-134">如果您不熟悉這個程序，請參閱 [如何抓取憑證的指紋值](http://youtu.be/YKQF266SAxI)。</span><span class="sxs-lookup"><span data-stu-id="dde70-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="dde70-135">**若要設定單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dde70-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="dde70-136">以系統管理員身分登入您的 Coupa 公司網站。</span><span class="sxs-lookup"><span data-stu-id="dde70-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="dde70-137">移至 [設定] \> [安全性控制]。</span><span class="sxs-lookup"><span data-stu-id="dde70-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="dde70-138">![安全性控制項](./media/active-directory-saas-coupa-tutorial/IC791900.png "安全性控制項")</span><span class="sxs-lookup"><span data-stu-id="dde70-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="dde70-139">若要將 Coupa 中繼資料檔案下載至您的電腦，按一下 [下載和匯入預存程序的中繼資料] 。</span><span class="sxs-lookup"><span data-stu-id="dde70-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="dde70-140">![Coupa 預存程序中繼資料](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa 預存程序中繼資料")</span><span class="sxs-lookup"><span data-stu-id="dde70-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="dde70-141">在不同的瀏覽器視窗中，登入 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="dde70-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="dde70-142">在 [Coupa] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dde70-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="dde70-143">![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791902.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="dde70-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="dde70-144">在 [要如何讓使用者登入 Coupa] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="dde70-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="dde70-145">![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791903.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="dde70-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="dde70-146">在 [設定應用程式 URL]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dde70-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="dde70-147">![設定應用程式 URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="dde70-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="dde70-148">在 [登入 URL] 文字方塊中，輸入您的使用者用來登入 Coupa 應用程式的 URL (例如： “*http://company.Coupa.com*”)。</span><span class="sxs-lookup"><span data-stu-id="dde70-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="dde70-149">開啟您已下載的 Coupa 中繼資料檔案，然後複製 **AssertionConsumerService index/URL**。</span><span class="sxs-lookup"><span data-stu-id="dde70-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="dde70-150">在 [Coupa 回覆 URL] 文字方塊中，貼上 **AssertionConsumerService index/URL** 值。</span><span class="sxs-lookup"><span data-stu-id="dde70-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="dde70-151">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="dde70-151">Click **Next**.</span></span>
8. <span data-ttu-id="dde70-152">在 [設定在 Coupa 單一登入] 頁面上，請按一下 [下載中繼資料] 來下載您的中繼資料，然後將檔案儲存在您的本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="dde70-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="dde70-153">![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791905.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="dde70-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="dde70-154">在 Coupa 公司網站上，請移至 [設定] \> [安全性控制]。</span><span class="sxs-lookup"><span data-stu-id="dde70-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="dde70-155">![安全性控制項](./media/active-directory-saas-coupa-tutorial/IC791900.png "安全性控制項")</span><span class="sxs-lookup"><span data-stu-id="dde70-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="dde70-156">在 [使用 Coupa 認證登入]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dde70-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="dde70-157">![使用 Coupa 認證登入](./media/active-directory-saas-coupa-tutorial/IC791906.png "使用 Coupa 認證登入")</span><span class="sxs-lookup"><span data-stu-id="dde70-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="dde70-158">選取 [使用 SAML 登入] 。</span><span class="sxs-lookup"><span data-stu-id="dde70-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="dde70-159">按一下 [瀏覽]  來上傳您下載的 Azure Active Directory 中繼資料檔。</span><span class="sxs-lookup"><span data-stu-id="dde70-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="dde70-160">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="dde70-160">Click **Save**.</span></span>
11. <span data-ttu-id="dde70-161">在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dde70-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="dde70-162">![設定單一登入](./media/active-directory-saas-coupa-tutorial/IC791907.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="dde70-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="dde70-163">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="dde70-163">Configure user provisioning</span></span>

<span data-ttu-id="dde70-164">若要讓 Azure AD 使用者可以登入 Coupa，則必須將他們佈建到 Coupa。</span><span class="sxs-lookup"><span data-stu-id="dde70-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="dde70-165">Coupa 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="dde70-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="dde70-166">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dde70-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="dde70-167">以系統管理員身分登入您的 **Coupa** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="dde70-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="dde70-168">在頂端的功能表中，按一下 [設定]，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="dde70-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="dde70-169">![使用者](./media/active-directory-saas-coupa-tutorial/IC791908.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="dde70-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="dde70-170">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="dde70-170">Click **Create**.</span></span>
   
   <span data-ttu-id="dde70-171">![建立使用者](./media/active-directory-saas-coupa-tutorial/IC791909.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="dde70-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="dde70-172">在 [使用者建立]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="dde70-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="dde70-173">![使用者詳細資料](./media/active-directory-saas-coupa-tutorial/IC791910.png "使用者詳細資料")</span><span class="sxs-lookup"><span data-stu-id="dde70-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="dde70-174">在相關的文字方塊中，輸入您要佈建之有效 Azure Active Directory 帳戶的 [登入]、[名字]、[姓氏]、[單一登入識別碼]、[電子郵件] 屬性。</span><span class="sxs-lookup"><span data-stu-id="dde70-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="dde70-175">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="dde70-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="dde70-176">Azure Active Directory 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="dde70-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="dde70-177">您可以使用任何其他的 Coupa 使用者帳戶建立工具或 Coupa 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="dde70-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="dde70-178">指派使用者</span><span class="sxs-lookup"><span data-stu-id="dde70-178">Assign users</span></span>
<span data-ttu-id="dde70-179">若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。</span><span class="sxs-lookup"><span data-stu-id="dde70-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="dde70-180">**若要指派使用者給 Coupa，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dde70-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="dde70-181">在 Azure 傳統入口網站中建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="dde70-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="dde70-182">在 * * Coupa * * 應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="dde70-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="dde70-183">![指派使用者](./media/active-directory-saas-coupa-tutorial/IC791911.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="dde70-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="dde70-184">選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。</span><span class="sxs-lookup"><span data-stu-id="dde70-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="dde70-185">![是](./media/active-directory-saas-coupa-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="dde70-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="dde70-186">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="dde70-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="dde70-187">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="dde70-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

