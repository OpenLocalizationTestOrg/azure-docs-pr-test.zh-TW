---
title: "教學課程：Azure Active Directory 與 Qualtrics 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Qualtrics 單一登入、 自動化佈建，以及更多 ！"
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
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="676f2-103">教學課程：Azure Active Directory 與 Qualtrics 整合</span><span class="sxs-lookup"><span data-stu-id="676f2-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="676f2-104">本教學課程的 hello 目標是 Azure 與 Qualtrics tooshow hello 整合。</span><span class="sxs-lookup"><span data-stu-id="676f2-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="676f2-105">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="676f2-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="676f2-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="676f2-106">A valid Azure subscription</span></span>
* <span data-ttu-id="676f2-107">已啟用 Qualtrics 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="676f2-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="676f2-108">完成本教學課程之後, 您已指派 tooQualtrics hello Azure AD 使用者將能夠 toosingle 登入位於您 Qualtrics 公司網站 （服務提供者起始登入），或使用 hello 的 hello 應用程式[簡介 toohello存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="676f2-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="676f2-109">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="676f2-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="676f2-110">啟用 Qualtrics 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="676f2-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="676f2-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="676f2-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="676f2-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="676f2-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="676f2-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="676f2-113">Assigning users</span></span>

<span data-ttu-id="676f2-114">![案例](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "案例")</span><span class="sxs-lookup"><span data-stu-id="676f2-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="676f2-115">啟用 Qualtrics 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="676f2-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="676f2-116">本節 hello 目標是 toooutline 如何 Qualtrics tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="676f2-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="676f2-117">**tooenable hello 應用程式整合，qualtrics，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="676f2-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="676f2-118">在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="676f2-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="676f2-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="676f2-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="676f2-120">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="676f2-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="676f2-121">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="676f2-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="676f2-122">![應用程式](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="676f2-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="676f2-123">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="676f2-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="676f2-124">![新增應用程式](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="676f2-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="676f2-125">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="676f2-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="676f2-126">![從資源庫新增應用程式](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="676f2-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="676f2-127">在 hello**搜尋方塊**，型別**Qualtrics**。</span><span class="sxs-lookup"><span data-stu-id="676f2-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="676f2-128">![應用程式資源庫](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="676f2-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="676f2-129">在 hello 結果窗格中，選取  **Qualtrics**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="676f2-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="676f2-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="676f2-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="676f2-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="676f2-131">Configure single sign-on</span></span>

<span data-ttu-id="676f2-132">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooQualtrics 的同盟，使用 Azure AD 的帳戶與如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="676f2-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="676f2-133">**tooconfigure 單一登入，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="676f2-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="676f2-134">在 Azure 傳統入口網站，在 hello hello **Qualtrics**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="676f2-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="676f2-135">![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="676f2-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="676f2-136">在 hello**如何想您使用者 toosign tooQualtrics 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="676f2-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="676f2-137">![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="676f2-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="676f2-138">在 hello**設定應用程式 URL**  頁面的 hello **Qualtrics 登入 URL**文字方塊中，輸入您的 URL (例如:"*https://ssotest2ut1.qualtrics.com*")，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="676f2-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="676f2-139">![設定應用程式 URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="676f2-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="676f2-140">在 hello**在 Qualtrics 設定單一登入**頁面上，按一下**下載中繼資料**，然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="676f2-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="676f2-141">![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="676f2-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="676f2-142">傳送嗨中繼資料檔案 toohello Qualtrics 支援小組。</span><span class="sxs-lookup"><span data-stu-id="676f2-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="676f2-143">hello SSO 組態必須 toobe hello Qualtrics 支援小組所執行。</span><span class="sxs-lookup"><span data-stu-id="676f2-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="676f2-144">只要 hello 組態完成之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="676f2-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="676f2-145">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="676f2-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="676f2-146">![設定單一登入](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="676f2-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="676f2-147">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="676f2-147">Configure user provisioning</span></span>

<span data-ttu-id="676f2-148">不沒有您 tooconfigure 使用者佈建 tooQualtrics 任何動作項目。</span><span class="sxs-lookup"><span data-stu-id="676f2-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="676f2-149">當指派的使用者嘗試 toolog 入 Qualtrics 使用 hello 存取面板時，Qualtrics 會檢查 hello 使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="676f2-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="676f2-150">如果尚無可用的使用者帳戶，Qualtrics 就會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="676f2-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="676f2-151">指派使用者</span><span class="sxs-lookup"><span data-stu-id="676f2-151">Assign users</span></span>
<span data-ttu-id="676f2-152">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="676f2-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="676f2-153">**tooassign 使用者 tooQualtrics，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="676f2-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="676f2-154">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="676f2-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="676f2-155">在 hello **Qualtrics**應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="676f2-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="676f2-156">![指派使用者](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="676f2-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="676f2-157">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="676f2-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="676f2-158">![是](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="676f2-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="676f2-159">如果您想 tootest SSO 設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="676f2-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="676f2-160">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="676f2-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

