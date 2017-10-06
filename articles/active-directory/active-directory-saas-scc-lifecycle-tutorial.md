---
title: "教學課程：Azure Active Directory 與 SCC LifeCycle 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse SCC LifeCycle 單一登入、 自動化佈建，以及更多 ！"
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
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="27a6f-103">教學課程：Azure Active Directory 與 SCC LifeCycle 整合</span><span class="sxs-lookup"><span data-stu-id="27a6f-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="27a6f-104">本教學課程的 hello 目標是 Azure 與 SCC LifeCycle tooshow hello 整合。</span><span class="sxs-lookup"><span data-stu-id="27a6f-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="27a6f-105">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="27a6f-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="27a6f-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="27a6f-106">A valid Azure subscription</span></span>
* <span data-ttu-id="27a6f-107">已啟用 SCC LifeCycle 單一登入 (SSO) 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27a6f-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="27a6f-108">完成本教學課程之後, hello 您已指派的 tooSCC 生命週期將會無法 toosingle 登入 hello 應用程式位於您 SCC LifeCycle 公司網站 （服務提供者起始登入），Azure AD 使用者，或使用 hello[簡介存取面板 toohello](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="27a6f-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="27a6f-109">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="27a6f-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="27a6f-110">啟用 SCC LifeCycle 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="27a6f-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="27a6f-111">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="27a6f-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="27a6f-112">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="27a6f-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="27a6f-113">指派使用者</span><span class="sxs-lookup"><span data-stu-id="27a6f-113">Assigning users</span></span>

<span data-ttu-id="27a6f-114">![案例](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "案例")</span><span class="sxs-lookup"><span data-stu-id="27a6f-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="27a6f-115">啟用 SCC LifeCycle 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="27a6f-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="27a6f-116">本節 hello 目標是 toooutline 如何 SCC LifeCycle tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="27a6f-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="27a6f-117">**SCC LifeCycle tooenable hello 應用程式整合執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27a6f-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="27a6f-118">在 hello Azure 傳統入口網站，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="27a6f-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="27a6f-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="27a6f-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="27a6f-120">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="27a6f-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="27a6f-121">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="27a6f-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="27a6f-122">![應用程式](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="27a6f-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="27a6f-123">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="27a6f-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="27a6f-124">![新增應用程式](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="27a6f-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="27a6f-125">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="27a6f-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="27a6f-126">![從資源庫新增應用程式](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="27a6f-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="27a6f-127">在 hello**搜尋方塊**，型別**SCC LifeCycle**。</span><span class="sxs-lookup"><span data-stu-id="27a6f-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="27a6f-128">![應用程式資源庫](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="27a6f-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="27a6f-129">在 hello 結果窗格中，選取  **SCC LifeCycle**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27a6f-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="27a6f-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span><span class="sxs-lookup"><span data-stu-id="27a6f-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="27a6f-131">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="27a6f-131">Configure single sign-on</span></span>

<span data-ttu-id="27a6f-132">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooSCC 透過同盟，使用 Azure AD 的帳戶生命週期如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="27a6f-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="27a6f-133">**tooconfigure 單一登入，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="27a6f-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="27a6f-134">在 Azure 傳統入口網站，在 hello hello **SCC LifeCycle**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello * * 設定單一登入 * * 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="27a6f-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="27a6f-135">![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="27a6f-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="27a6f-136">Hello 上**如何想您 tooSCC 生命週期上的使用者 toosign**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="27a6f-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="27a6f-137">![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="27a6f-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="27a6f-138">在 hello**設定應用程式 URL**  頁面的 hello**登入 URL**文字方塊中，型別 hello URL 上使用的使用者 toosign tooyour SCC LifeCycle 的應用程式使用下列模式的 hello"*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*"，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="27a6f-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="27a6f-139">![設定應用程式 URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="27a6f-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="27a6f-140">在 hello **SCC LifeCycle 在設定單一登入**頁面上，按一下**下載中繼資料**，然後儲存在本機電腦上的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="27a6f-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="27a6f-141">![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="27a6f-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="27a6f-142">轉寄該中繼資料檔案 tooSCC LifeCycle 支援小組。</span><span class="sxs-lookup"><span data-stu-id="27a6f-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="27a6f-143">單一登入具有 toobe hello SCC LifeCycle 支援小組啟用。</span><span class="sxs-lookup"><span data-stu-id="27a6f-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="27a6f-144">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**完成**tooclose hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="27a6f-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="27a6f-145">![設定單一登入](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="27a6f-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="27a6f-146">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="27a6f-146">Configure user provisioning</span></span>

<span data-ttu-id="27a6f-147">在訂單 tooenable Azure AD 使用者 toolog 入 SCC LifeCycle，它們必須佈建到 SCC LifeCycle。</span><span class="sxs-lookup"><span data-stu-id="27a6f-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="27a6f-148">沒有您 tooconfigure 使用者佈建 tooSCC 生命週期的動作項目。</span><span class="sxs-lookup"><span data-stu-id="27a6f-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="27a6f-149">當入 SCC LifeCycle 指派的使用者嘗試 toolog 時，SCC LifeCycle 帳戶會在必要時自動建立。</span><span class="sxs-lookup"><span data-stu-id="27a6f-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="27a6f-150">您可以使用任何其他 SCC LifeCycle 使用者帳戶建立工具或 Api 提供 SCC LifeCycle tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="27a6f-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="27a6f-151">指派使用者</span><span class="sxs-lookup"><span data-stu-id="27a6f-151">Assign users</span></span>
<span data-ttu-id="27a6f-152">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="27a6f-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="27a6f-153">**tooassign 使用者 tooSCC 生命週期，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="27a6f-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="27a6f-154">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="27a6f-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="27a6f-155">在 hello * * SCC LifeCycle * * 應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="27a6f-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="27a6f-156">![指派使用者](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="27a6f-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="27a6f-157">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="27a6f-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="27a6f-158">![是](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="27a6f-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="27a6f-159">如果您想 tootest SSO 設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="27a6f-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="27a6f-160">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="27a6f-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

