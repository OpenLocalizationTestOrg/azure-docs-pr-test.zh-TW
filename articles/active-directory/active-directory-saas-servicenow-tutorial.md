---
title: "教學課程：Azure Active Directory 與 ServiceNow 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ServiceNow 和 ServiceNow Express 之間。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="38a7e-103">教學課程：Azure Active Directory 與 ServiceNow 整合</span><span class="sxs-lookup"><span data-stu-id="38a7e-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="38a7e-104">在此教學課程中，您學會如何 toointegrate ServiceNow 和 ServiceNow Express with Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="38a7e-104">In this tutorial, you learn how toointegrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38a7e-105">與 Azure AD 整合 ServiceNow 和 ServiceNow Express 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="38a7e-106">您可以控制存取 tooServiceNow Azure AD 和 ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="38a7e-106">You can control in Azure AD who has access tooServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="38a7e-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooServiceNow 和 ServiceNow 快速 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="38a7e-107">You can enable your users tooautomatically get signed-on tooServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="38a7e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="38a7e-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="38a7e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="38a7e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38a7e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="38a7e-110">Prerequisites</span></span>
<span data-ttu-id="38a7e-111">tooconfigure Azure AD 與 ServiceNow 和 ServiceNow Express 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-111">tooconfigure Azure AD integration with ServiceNow and ServiceNow Express, you need hello following items:</span></span>

* <span data-ttu-id="38a7e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="38a7e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="38a7e-113">若為 ServiceNow，ServiceNow 的執行個體或租用戶 (Calgary 版本或更新版本)</span><span class="sxs-lookup"><span data-stu-id="38a7e-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="38a7e-114">若為 ServiceNow Express，ServiceNow Express 的執行個體 (Helsinki 版本或更新版本)</span><span class="sxs-lookup"><span data-stu-id="38a7e-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="38a7e-115">hello ServiceNow 租用戶必須擁有 hello[多個提供者單一登入外掛程式](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0)啟用。</span><span class="sxs-lookup"><span data-stu-id="38a7e-115">hello ServiceNow tenant must have hello [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="38a7e-116">[提交服務要求](https://hi.service-now.com)即可達到此目的。</span><span class="sxs-lookup"><span data-stu-id="38a7e-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="38a7e-117">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="38a7e-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="38a7e-118">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="38a7e-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="38a7e-119">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="38a7e-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="38a7e-120">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="38a7e-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38a7e-121">案例描述</span><span class="sxs-lookup"><span data-stu-id="38a7e-121">Scenario description</span></span>
<span data-ttu-id="38a7e-122">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="38a7e-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38a7e-123">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="38a7e-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38a7e-124">從 hello 圖庫加入 ServiceNow</span><span class="sxs-lookup"><span data-stu-id="38a7e-124">Adding ServiceNow from hello gallery</span></span>
2. <span data-ttu-id="38a7e-125">為 ServiceNow 或 ServiceNow Express 設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="38a7e-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-hello-gallery"></a><span data-ttu-id="38a7e-126">從 hello 圖庫加入 ServiceNow</span><span class="sxs-lookup"><span data-stu-id="38a7e-126">Adding ServiceNow from hello gallery</span></span>
<span data-ttu-id="38a7e-127">tooconfigure hello 整合 ServiceNow 或 ServiceNow Express 到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd ServiceNow。</span><span class="sxs-lookup"><span data-stu-id="38a7e-127">tooconfigure hello integration of ServiceNow or ServiceNow Express into Azure AD, you need tooadd ServiceNow from hello gallery tooyour list of managed SaaS apps.</span></span> 

<span data-ttu-id="38a7e-128">**tooadd ServiceNow hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="38a7e-128">**tooadd ServiceNow from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="38a7e-129">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-129">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="38a7e-131">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="38a7e-131">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="38a7e-132">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="38a7e-132">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![應用程式][2]
4. <span data-ttu-id="38a7e-134">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="38a7e-134">Click **Add** at hello bottom of hello page.</span></span>
   
    ![應用程式][3]
5. <span data-ttu-id="38a7e-136">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-136">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![應用程式][4]
6. <span data-ttu-id="38a7e-138">在 [hello] 搜尋方塊中，輸入**ServiceNow**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-138">In hello search box, type **ServiceNow**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="38a7e-140">在 hello 結果窗格中，選取  **ServiceNow**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="38a7e-140">In hello results pane, select **ServiceNow**, and then click **Complete** tooadd hello application.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38a7e-142">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="38a7e-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38a7e-143">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試透過 ServiceNow 或 ServiceNow Express 使用 Azure AD 單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="38a7e-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38a7e-144">單一登入 toowork，Azure AD 需要 tooknow ServiceNow 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="38a7e-144">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceNow is tooa user in Azure AD.</span></span> <span data-ttu-id="38a7e-145">換句話說，Azure AD 使用者與 ServiceNow 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="38a7e-145">In other words, a link relationship between an Azure AD user and hello related user in ServiceNow needs toobe established.</span></span>
<span data-ttu-id="38a7e-146">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** ServiceNow 中。</span><span class="sxs-lookup"><span data-stu-id="38a7e-146">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceNow.</span></span> <span data-ttu-id="38a7e-147">tooconfigure 及 Azure AD 單一登入與 ServiceNow 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-147">tooconfigure and test Azure AD single sign-on with ServiceNow, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="38a7e-148">**[設定 Azure AD 單一登入 servicenow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="38a7e-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="38a7e-149">**[設定 Azure AD 單一登入 ServiceNow 快速](#configuring-azure-ad-single-sign-on-for-servicenow-express)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="38a7e-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - tooenable your users toouse this feature.</span></span>
3. <span data-ttu-id="38a7e-150">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="38a7e-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="38a7e-151">**[建立測試使用者 ServiceNow](#creating-a-servicenow-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 ServiceNow 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="38a7e-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - toohave a counterpart of Britta Simon in ServiceNow that is linked toohello Azure AD representation of her.</span></span>
5. <span data-ttu-id="38a7e-152">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="38a7e-152">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="38a7e-153">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="38a7e-153">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="38a7e-154">如果您想要 tooconfigure ServiceNow 略過步驟 2。</span><span class="sxs-lookup"><span data-stu-id="38a7e-154">If you want tooconfigure ServiceNow omit step 2.</span></span> <span data-ttu-id="38a7e-155">同樣地，如果您想要 tooconfigure ServiceNow Express 略過步驟 1。</span><span class="sxs-lookup"><span data-stu-id="38a7e-155">Likewise, if you want tooconfigure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="38a7e-156">為 ServiceNow 設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="38a7e-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="38a7e-157">Hello Azure AD 傳統入口網站中，在 hello **ServiceNow**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊.</span><span class="sxs-lookup"><span data-stu-id="38a7e-157">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="38a7e-158">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749323.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="38a7e-159">在 hello**如何想您使用者 toosign tooServiceNow 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-159">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="38a7e-160">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749324.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="38a7e-161">在 hello**設定應用程式設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-161">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="38a7e-162">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="38a7e-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="38a7e-163">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-163">a.</span></span> <span data-ttu-id="38a7e-164">在 hello **ServiceNow 登入 URL**文字方塊中，輸入您使用者 toosign 上 tooyour ServiceNow 的應用程式遵循 hello 模式所使用的 URL: `https://<instance-name>.service-now.com`。</span><span class="sxs-lookup"><span data-stu-id="38a7e-164">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="38a7e-165">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-165">b.</span></span> <span data-ttu-id="38a7e-166">在 hello**識別碼**文字方塊中，輸入您使用者 toosign 上 tooyour ServiceNow 的應用程式遵循 hello 模式所使用的 URL: `https://<instance-name>.service-now.com`。</span><span class="sxs-lookup"><span data-stu-id="38a7e-166">In hello **Identifier** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="38a7e-167">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-167">c.</span></span> <span data-ttu-id="38a7e-168">按一下 [下一步] </span><span class="sxs-lookup"><span data-stu-id="38a7e-168">Click **Next**</span></span>

4. <span data-ttu-id="38a7e-169">toohave Azure AD 自動設定 ServiceNow SAML 型驗證中，輸入 ServiceNow 執行個體名稱、 管理員使用者名稱，以及系統管理員密碼 hello**自動設定單一登入**按一下*設定*。</span><span class="sxs-lookup"><span data-stu-id="38a7e-169">toohave Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in hello **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="38a7e-170">請注意提供該 hello 管理員使用者名稱必須具有 hello **security_admin**此 toowork ServiceNow 中指派的角色。</span><span class="sxs-lookup"><span data-stu-id="38a7e-170">Note that hello admin username provided must have hello **security_admin** role assigned in ServiceNow for this toowork.</span></span> <span data-ttu-id="38a7e-171">否則，toomanually 設定 ServiceNow toouse Azure AD 做為 SAML 身分識別提供者，請按一下**手動設定進行單一登入的 hello 應用程式**，然後按一下 **下一步**和完整的 hello下列步驟。</span><span class="sxs-lookup"><span data-stu-id="38a7e-171">Otherwise, toomanually configure ServiceNow toouse Azure AD as a SAML identity provider, click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="38a7e-172">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="38a7e-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="38a7e-173">在 hello**在 ServiceNow 設定單一登入**頁面上，按一下**下載憑證**，儲存在本機電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="38a7e-173">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="38a7e-174">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749325.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="38a7e-175">登入 tooyour ServiceNow 的應用程式系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="38a7e-175">Sign-on tooyour ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="38a7e-176">啟動 hello*整合的多個提供者單一登入安裝程式*依照外掛程式 hello 接下來的步驟：</span><span class="sxs-lookup"><span data-stu-id="38a7e-176">Activate hello *Integration - Multiple Provider Single Sign-On Installer* plugin by following hello next steps:</span></span>
   
    <span data-ttu-id="38a7e-177">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-177">a.</span></span> <span data-ttu-id="38a7e-178">Hello hello 左側瀏覽窗格中移過**系統定義**區段，然後按一下**外掛程式**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-178">In hello navigation pane on hello left side, go too**System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="38a7e-179">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "啟動外掛程式")</span><span class="sxs-lookup"><span data-stu-id="38a7e-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="38a7e-180">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-180">b.</span></span> <span data-ttu-id="38a7e-181">搜尋*整合 - 多個提供者單一登入安裝程式*。</span><span class="sxs-lookup"><span data-stu-id="38a7e-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="38a7e-182">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "啟動外掛程式")</span><span class="sxs-lookup"><span data-stu-id="38a7e-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="38a7e-183">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-183">c.</span></span> <span data-ttu-id="38a7e-184">選取 hello 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="38a7e-184">Select hello plugin.</span></span> <span data-ttu-id="38a7e-185">按一下滑鼠右鍵並選取 [啟動/升級]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="38a7e-186">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-186">d.</span></span> <span data-ttu-id="38a7e-187">按一下 hello **Activate**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="38a7e-187">Click hello **Activate** button.</span></span>

8. <span data-ttu-id="38a7e-188">Hello hello 左側瀏覽窗格中按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-188">In hello navigation pane on hello left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="38a7e-189">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="38a7e-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="38a7e-190">在 [hello**多個提供者 SSO 屬性**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-190">On hello **Multiple Provider SSO Properties** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="38a7e-191">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="38a7e-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="38a7e-192">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-192">a.</span></span> <span data-ttu-id="38a7e-193">針對 [啟用多個提供者 SSO]，選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="38a7e-194">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-194">b.</span></span> <span data-ttu-id="38a7e-195">做為**啟用偵錯記錄收到 hello 多個提供者 SSO 整合**，選取**是**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-195">As **Enable debug logging got hello multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="38a7e-196">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-196">c.</span></span> <span data-ttu-id="38a7e-197">在**hello 欄位 hello 使用者資料表，其中...**文字方塊中，輸入**user_name**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-197">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="38a7e-198">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-198">d.</span></span> <span data-ttu-id="38a7e-199">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-199">Click **Save**.</span></span>

10. <span data-ttu-id="38a7e-200">Hello hello 左側瀏覽窗格中按一下**x509 憑證**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-200">In hello navigation pane on hello left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="38a7e-201">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="38a7e-202">在 hello **X.509 憑證** 對話方塊中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-202">On hello **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="38a7e-203">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="38a7e-204">在 [hello **X.509 憑證**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-204">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="38a7e-205">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="38a7e-206">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-206">a.</span></span> <span data-ttu-id="38a7e-207">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-207">Click **New**.</span></span>
    
     <span data-ttu-id="38a7e-208">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-208">b.</span></span> <span data-ttu-id="38a7e-209">在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： **TestSAML2.0**)。</span><span class="sxs-lookup"><span data-stu-id="38a7e-209">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="38a7e-210">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-210">c.</span></span> <span data-ttu-id="38a7e-211">選取 [使用中] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-211">Select **Active**.</span></span>
    
     <span data-ttu-id="38a7e-212">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-212">d.</span></span> <span data-ttu-id="38a7e-213">針對 [格式]，選取 [PEM]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="38a7e-214">e.</span><span class="sxs-lookup"><span data-stu-id="38a7e-214">e.</span></span> <span data-ttu-id="38a7e-215">針對 [類型]，選取 [信任存放區憑證]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="38a7e-216">f.</span><span class="sxs-lookup"><span data-stu-id="38a7e-216">f.</span></span> <span data-ttu-id="38a7e-217">開啟 [記事本]，複製到剪貼簿，其內容的 hello 的 Base64 編碼的憑證，然後將它貼入 toohello **PEM 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="38a7e-217">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="38a7e-218">g.</span><span class="sxs-lookup"><span data-stu-id="38a7e-218">g.</span></span> <span data-ttu-id="38a7e-219">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-219">Click **Update**.</span></span>

13. <span data-ttu-id="38a7e-220">Hello hello 左側瀏覽窗格中按一下**身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-220">In hello navigation pane on hello left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="38a7e-221">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="38a7e-222">在 hello**身分識別提供者** 對話方塊中，按一下 **新增**:</span><span class="sxs-lookup"><span data-stu-id="38a7e-222">On hello **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="38a7e-223">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="38a7e-224">在 hello**身分識別提供者** 對話方塊中，按一下  **SAML2 Update1？**:</span><span class="sxs-lookup"><span data-stu-id="38a7e-224">On hello **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="38a7e-225">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="38a7e-226">Hello SAML2 Update1 屬性 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-226">On hello SAML2 Update1 Properties dialog, perform hello following steps:</span></span>
    
     <span data-ttu-id="38a7e-227">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="38a7e-228">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-228">a.</span></span> <span data-ttu-id="38a7e-229">在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： **SAML 2.0**)。</span><span class="sxs-lookup"><span data-stu-id="38a7e-229">in hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="38a7e-230">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-230">b.</span></span> <span data-ttu-id="38a7e-231">在 hello**使用者欄位**文字方塊中，輸入**電子郵件**或**user_name**，取決於哪一個欄位使用 toouniquely 識別您的 ServiceNow 部署中的使用者。</span><span class="sxs-lookup"><span data-stu-id="38a7e-231">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="38a7e-232">您可以設定 Azure AD tooemit 任一 hello Azure AD 使用者識別碼 （使用者主體名稱），或為所要 toohello hello hello SAML 權杖中的唯一識別碼 hello 電子郵件地址**ServiceNow > 屬性 > 單一登入**區段hello Azure 傳統入口網站和對應所需的 hello 欄位 toohello **nameidentifier**屬性。</span><span class="sxs-lookup"><span data-stu-id="38a7e-232">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="38a7e-233">hello 選屬性儲存在 Azure AD （例如使用者主體名稱） 中的 hello 值必須符合 hello 值儲存在 ServiceNow 中的 hello 輸入欄位 （例如使用者名稱）</span><span class="sxs-lookup"><span data-stu-id="38a7e-233">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>

    <span data-ttu-id="38a7e-234">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-234">c.</span></span> <span data-ttu-id="38a7e-235">在傳統入口網站 hello Azure AD，複製 hello**身分識別提供者識別碼**值並貼到 hello**身分識別提供者 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="38a7e-235">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="38a7e-236">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-236">d.</span></span> <span data-ttu-id="38a7e-237">在傳統入口網站 hello Azure AD，複製 hello**驗證要求 URL**值並貼到 hello**身分識別提供者的 AuthnRequest**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="38a7e-237">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="38a7e-238">e.</span><span class="sxs-lookup"><span data-stu-id="38a7e-238">e.</span></span> <span data-ttu-id="38a7e-239">在傳統入口網站 hello Azure AD，複製 hello**單一登出服務 URL**值並貼到 hello**身分識別提供者 SingleLogoutRequest**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="38a7e-239">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="38a7e-240">f.</span><span class="sxs-lookup"><span data-stu-id="38a7e-240">f.</span></span> <span data-ttu-id="38a7e-241">在 hello **ServiceNow 首頁**文字方塊中，您的 ServiceNow 執行個體首頁的型別 hello URL。</span><span class="sxs-lookup"><span data-stu-id="38a7e-241">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="38a7e-242">hello ServiceNow 執行個體首頁是串連您**ServieNow 租用戶 URL**和**/navpage.do** (例如：`https://fabrikam.service-now.com/navpage.do`)。</span><span class="sxs-lookup"><span data-stu-id="38a7e-242">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="38a7e-243">g.</span><span class="sxs-lookup"><span data-stu-id="38a7e-243">g.</span></span> <span data-ttu-id="38a7e-244">在 hello**實體識別碼 / 簽發者**文字方塊中，您的 ServiceNow 租用戶的型別 hello URL。</span><span class="sxs-lookup"><span data-stu-id="38a7e-244">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="38a7e-245">h.</span><span class="sxs-lookup"><span data-stu-id="38a7e-245">h.</span></span> <span data-ttu-id="38a7e-246">在 hello**觀眾 URL**文字方塊中，您的 ServiceNow 租用戶的型別 hello URL。</span><span class="sxs-lookup"><span data-stu-id="38a7e-246">In hello **Audience URL** textbox, type hello URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="38a7e-247">i.</span><span class="sxs-lookup"><span data-stu-id="38a7e-247">i.</span></span> <span data-ttu-id="38a7e-248">在 hello**通訊協定繫結 hello IDP 的 SingleLogoutRequest**文字方塊中，輸入**urn: oasis： 名稱： tc: SAML:2.0:bindings:HTTP-重新導向**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-248">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="38a7e-249">j.</span><span class="sxs-lookup"><span data-stu-id="38a7e-249">j.</span></span> <span data-ttu-id="38a7e-250">在 hello NameID 原則文字方塊中，輸入**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-格式： 未指定**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-250">In hello NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="38a7e-251">k.</span><span class="sxs-lookup"><span data-stu-id="38a7e-251">k.</span></span> <span data-ttu-id="38a7e-252">取消選取 [建立 AuthnContextClass]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="38a7e-253">l.</span><span class="sxs-lookup"><span data-stu-id="38a7e-253">l.</span></span> <span data-ttu-id="38a7e-254">在 hello **AuthnContextClassRef 方法**，型別`http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`。</span><span class="sxs-lookup"><span data-stu-id="38a7e-254">In hello **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="38a7e-255">只有您是僅限雲端組織時才需要此值。</span><span class="sxs-lookup"><span data-stu-id="38a7e-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="38a7e-256">如果您使用內部部署 ADFS 或 MFA 進行驗證，則不應該設定這個值。</span><span class="sxs-lookup"><span data-stu-id="38a7e-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="38a7e-257">m.</span><span class="sxs-lookup"><span data-stu-id="38a7e-257">m.</span></span> <span data-ttu-id="38a7e-258">在 [時鐘誤差] 文字方塊中，輸入 **60**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="38a7e-259">n.</span><span class="sxs-lookup"><span data-stu-id="38a7e-259">n.</span></span> <span data-ttu-id="38a7e-260">針對**單一登入指令碼**，選取 **MultiSSO_SAML2_Update1**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="38a7e-261">o.</span><span class="sxs-lookup"><span data-stu-id="38a7e-261">o.</span></span> <span data-ttu-id="38a7e-262">做為**x509 憑證**，選取您已建立 hello 上一個步驟中的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="38a7e-262">As **x509 Certificate**, select hello certificate you have created in hello previous step.</span></span>

    <span data-ttu-id="38a7e-263">p.</span><span class="sxs-lookup"><span data-stu-id="38a7e-263">p.</span></span> <span data-ttu-id="38a7e-264">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="38a7e-265">在傳統入口網站 hello Azure AD，選取 hello 單一登入組態確認，然後**下一步**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-265">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="38a7e-266">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="38a7e-267">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-267">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="38a7e-268">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="38a7e-269">為 ServiceNow Express 設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="38a7e-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="38a7e-270">Hello Azure AD 傳統入口網站中，在 hello **ServiceNow**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊.</span><span class="sxs-lookup"><span data-stu-id="38a7e-270">In hello Azure AD classic portal, on hello **ServiceNow** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="38a7e-271">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749323.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="38a7e-272">在 hello**如何想您使用者 toosign tooServiceNow 上**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-272">On hello **How would you like users toosign on tooServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="38a7e-273">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749324.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="38a7e-274">在 hello**設定應用程式設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-274">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="38a7e-275">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="38a7e-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="38a7e-276">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-276">a.</span></span> <span data-ttu-id="38a7e-277">在 hello **ServiceNow 登入 URL**文字方塊中，輸入您使用者 toosign 上 tooyour ServiceNow 的應用程式遵循 hello 模式所使用的 URL: `https://<instance-name>.service-now.com`。</span><span class="sxs-lookup"><span data-stu-id="38a7e-277">in hello **ServiceNow Sign On URL** textbox, type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="38a7e-278">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-278">b.</span></span> <span data-ttu-id="38a7e-279">在 hello**簽發者 URL**文字方塊中，輸入您使用者 toosign 上 tooyour ServiceNow 的應用程式遵循 hello 模式所使用的 URL `https://<instance-name>.service-now.com`。</span><span class="sxs-lookup"><span data-stu-id="38a7e-279">In hello **Issuer URL** textbox,type your URL used by your users toosign-on tooyour ServiceNow application following hello pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="38a7e-280">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-280">c.</span></span> <span data-ttu-id="38a7e-281">按一下 [下一步] </span><span class="sxs-lookup"><span data-stu-id="38a7e-281">Click **Next**</span></span>

4. <span data-ttu-id="38a7e-282">按一下**手動設定 hello 應用程式的單一登入**，然後按一下 **下一步**和 hello 完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="38a7e-282">Click **Manually configure hello application for single sign-on**, then click **Next** and complete hello following steps.</span></span>
   
    <span data-ttu-id="38a7e-283">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="38a7e-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="38a7e-284">在 hello**在 ServiceNow 設定單一登入**頁面上，按一下**下載憑證**，儲存在本機電腦上的 hello 憑證檔案，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-284">On hello **Configure single sign-on at ServiceNow** page, click **Download certificate**, save hello certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="38a7e-285">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC749325.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="38a7e-286">登入 tooyour ServiceNow Express 應用程式，以系統管理員。</span><span class="sxs-lookup"><span data-stu-id="38a7e-286">Sign-on tooyour ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="38a7e-287">Hello hello 左側瀏覽窗格中按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-287">In hello navigation pane on hello left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="38a7e-288">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="38a7e-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="38a7e-289">在 [hello**單一登入**] 對話方塊中，按一下向右鍵和設定 hello 下列屬性的 hello 上限 hello 組態圖示：</span><span class="sxs-lookup"><span data-stu-id="38a7e-289">On hello **Single Sign-On** dialog, click hello configuration icon on hello upper right and set hello following properties:</span></span>
   
    <span data-ttu-id="38a7e-290">![設定應用程式 URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="38a7e-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="38a7e-291">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-291">a.</span></span> <span data-ttu-id="38a7e-292">切換**啟用多個提供者 SSO** toohello 權限。</span><span class="sxs-lookup"><span data-stu-id="38a7e-292">Toggle **Enable multiple provider SSO** toohello right.</span></span>
   
    <span data-ttu-id="38a7e-293">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-293">b.</span></span> <span data-ttu-id="38a7e-294">切換**啟用偵錯記錄多個提供者 SSO 整合 hello** toohello 權限。</span><span class="sxs-lookup"><span data-stu-id="38a7e-294">Toggle **Enable debug logging for hello multiple provider SSO integration** toohello right.</span></span>
   
    <span data-ttu-id="38a7e-295">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-295">c.</span></span> <span data-ttu-id="38a7e-296">在**hello 欄位 hello 使用者資料表，其中...**文字方塊中，輸入**user_name**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-296">In **hello field on hello user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="38a7e-297">在 hello**單一登入** 對話方塊中，按一下 **加入新的憑證**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-297">On hello **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="38a7e-298">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="38a7e-299">在 [hello **X.509 憑證**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-299">On hello **X.509 Certificates** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="38a7e-300">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="38a7e-301">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-301">a.</span></span> <span data-ttu-id="38a7e-302">在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： **TestSAML2.0**)。</span><span class="sxs-lookup"><span data-stu-id="38a7e-302">In hello **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="38a7e-303">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-303">b.</span></span> <span data-ttu-id="38a7e-304">選取 [使用中] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-304">Select **Active**.</span></span>
    
    <span data-ttu-id="38a7e-305">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-305">c.</span></span> <span data-ttu-id="38a7e-306">針對 [格式]，選取 [PEM]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="38a7e-307">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-307">d.</span></span> <span data-ttu-id="38a7e-308">針對 [類型]，選取 [信任存放區憑證]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="38a7e-309">e.</span><span class="sxs-lookup"><span data-stu-id="38a7e-309">e.</span></span> <span data-ttu-id="38a7e-310">從您下載的憑證建立 Base64 編碼的檔案。</span><span class="sxs-lookup"><span data-stu-id="38a7e-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="38a7e-311">如需詳細資訊，請參閱[如何 tooconvert 二進位憑證到文字檔](http://youtu.be/PlgrzUZ-Y1o)。</span><span class="sxs-lookup"><span data-stu-id="38a7e-311">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="38a7e-312">f.</span><span class="sxs-lookup"><span data-stu-id="38a7e-312">f.</span></span> <span data-ttu-id="38a7e-313">開啟 [記事本]，複製到剪貼簿，其內容的 hello 的 Base64 編碼的憑證，然後將它貼入 toohello **PEM 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="38a7e-313">Open your Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="38a7e-314">g.</span><span class="sxs-lookup"><span data-stu-id="38a7e-314">g.</span></span> <span data-ttu-id="38a7e-315">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-315">Click **Update**.</span></span>
11. <span data-ttu-id="38a7e-316">在 hello**單一登入** 對話方塊中，按一下 **加入新的 IdP**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-316">On hello **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="38a7e-317">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="38a7e-318">在 hello**新增身分識別提供者**對話方塊下方**設定身分識別提供者**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-318">On hello **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform hello following steps:</span></span>
    
    <span data-ttu-id="38a7e-319">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="38a7e-320">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-320">a.</span></span> <span data-ttu-id="38a7e-321">在 hello**名稱**文字方塊中，輸入您的組態名稱 (例如： **SAML 2.0**)。</span><span class="sxs-lookup"><span data-stu-id="38a7e-321">In hello **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="38a7e-322">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-322">b.</span></span> <span data-ttu-id="38a7e-323">在傳統入口網站 hello Azure AD，複製 hello**身分識別提供者識別碼**值並貼到 hello**身分識別提供者 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="38a7e-323">In hello Azure AD classic portal, copy hello **Identity Provider ID** value, and then paste it into hello **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="38a7e-324">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-324">c.</span></span> <span data-ttu-id="38a7e-325">在傳統入口網站 hello Azure AD，複製 hello**驗證要求 URL**值並貼到 hello**身分識別提供者的 AuthnRequest**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="38a7e-325">In hello Azure AD classic portal, copy hello **Authentication Request URL** value, and then paste it into hello **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="38a7e-326">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-326">d.</span></span> <span data-ttu-id="38a7e-327">在傳統入口網站 hello Azure AD，複製 hello**單一登出服務 URL**值並貼到 hello**身分識別提供者 SingleLogoutRequest**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="38a7e-327">In hello Azure AD classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="38a7e-328">e.</span><span class="sxs-lookup"><span data-stu-id="38a7e-328">e.</span></span> <span data-ttu-id="38a7e-329">做為**身分識別提供者憑證**，選取您已建立 hello 上一個步驟中的 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="38a7e-329">As **Identity Provider Certificate**, select hello certificate you have created in hello previous step.</span></span>


1. <span data-ttu-id="38a7e-330">按一下**進階設定**，然後在**其他身分識別提供者屬性**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="38a7e-331">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="38a7e-332">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-332">a.</span></span> <span data-ttu-id="38a7e-333">在 hello**通訊協定繫結 hello IDP 的 SingleLogoutRequest**文字方塊中，輸入**urn: oasis： 名稱： tc: SAML:2.0:bindings:HTTP-重新導向**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-333">In hello **Protocol Binding for hello IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="38a7e-334">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-334">b.</span></span> <span data-ttu-id="38a7e-335">在 hello **NameID 原則**文字方塊中，輸入**urn: oasis： 名稱： tc: saml: 1.1 nameid-format-格式： 未指定**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-335">In hello **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="38a7e-336">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-336">c.</span></span> <span data-ttu-id="38a7e-337">在 hello **AuthnContextClassRef 方法**，型別**http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-337">In hello **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="38a7e-338">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-338">d.</span></span> <span data-ttu-id="38a7e-339">取消選取 [建立 AuthnContextClass]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="38a7e-340">在下**其他服務提供者內容**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-340">Under **Additional Service Provider Properties**, perform hello following steps:</span></span>
   
    <span data-ttu-id="38a7e-341">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="38a7e-342">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-342">a.</span></span> <span data-ttu-id="38a7e-343">在 hello **ServiceNow 首頁**文字方塊中，您的 ServiceNow 執行個體首頁的型別 hello URL。</span><span class="sxs-lookup"><span data-stu-id="38a7e-343">In hello **ServiceNow Homepage** textbox, type hello URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="38a7e-344">hello ServiceNow 執行個體首頁是串連您**ServieNow 租用戶 URL**和**/navpage.do** (例如： `https://fabrikam.service-now.com/navpage.do`)。</span><span class="sxs-lookup"><span data-stu-id="38a7e-344">hello ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="38a7e-345">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-345">b.</span></span> <span data-ttu-id="38a7e-346">在 hello**實體識別碼 / 簽發者**文字方塊中，您的 ServiceNow 租用戶的型別 hello URL。</span><span class="sxs-lookup"><span data-stu-id="38a7e-346">In hello **Entity ID / Issuer** textbox, type hello URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="38a7e-347">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-347">c.</span></span> <span data-ttu-id="38a7e-348">在 hello**對象 URI**文字方塊中，您的 ServiceNow 租用戶的型別 hello URL。</span><span class="sxs-lookup"><span data-stu-id="38a7e-348">In hello **Audience URI** textbox, type hello URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="38a7e-349">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-349">d.</span></span> <span data-ttu-id="38a7e-350">在 [時鐘誤差] 文字方塊中，輸入 **60**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="38a7e-351">e.</span><span class="sxs-lookup"><span data-stu-id="38a7e-351">e.</span></span> <span data-ttu-id="38a7e-352">在 hello**使用者欄位**文字方塊中，輸入**電子郵件**或**user_name**，取決於哪一個欄位使用 toouniquely 識別您的 ServiceNow 部署中的使用者。</span><span class="sxs-lookup"><span data-stu-id="38a7e-352">In hello **User Field** textbox, type **email** or **user_name**, depending on which field is used toouniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="38a7e-353">您可以設定 Azure AD tooemit 任一 hello Azure AD 使用者識別碼 （使用者主體名稱），或為所要 toohello hello hello SAML 權杖中的唯一識別碼 hello 電子郵件地址**ServiceNow > 屬性 > 單一登入**區段hello Azure 傳統入口網站和對應所需的 hello 欄位 toohello **nameidentifier**屬性。</span><span class="sxs-lookup"><span data-stu-id="38a7e-353">You can configue Azure AD tooemit either hello Azure AD user ID (user principal name) or hello email address as hello unique identifier in hello SAML token by going toohello **ServiceNow > Attributes > Single Sign-On** section of hello Azure classic portal and mapping hello desired field toohello **nameidentifier** attribute.</span></span> <span data-ttu-id="38a7e-354">hello 選屬性儲存在 Azure AD （例如使用者主體名稱） 中的 hello 值必須符合 hello 值儲存在 ServiceNow 中的 hello 輸入欄位 （例如使用者名稱）</span><span class="sxs-lookup"><span data-stu-id="38a7e-354">hello value stored for hello selected attribute in Azure AD (e.g. user principal name) must match hello value stored in ServiceNow for hello entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="38a7e-355">f.</span><span class="sxs-lookup"><span data-stu-id="38a7e-355">f.</span></span> <span data-ttu-id="38a7e-356">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-356">Click **Save**.</span></span> 

3. <span data-ttu-id="38a7e-357">在傳統入口網站 hello Azure AD，選取 hello 單一登入組態確認，然後**下一步**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-357">On hello Azure AD classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="38a7e-358">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="38a7e-359">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-359">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="38a7e-360">![設定單一登入](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="38a7e-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="38a7e-361">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="38a7e-361">Configuring user provisioning</span></span>
<span data-ttu-id="38a7e-362">hello 本節目標在於 toooutline 如何 tooenable 使用者佈建的 Active Directory 使用者帳戶 tooServiceNow。</span><span class="sxs-lookup"><span data-stu-id="38a7e-362">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooServiceNow.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="38a7e-363">tooconfigure 使用者佈建，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-363">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="38a7e-364">Hello 管理 Azure 傳統入口網站中，在 hello **ServiceNow**應用程式整合頁面上，按一下 **設定使用者佈建**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-364">In hello Azure Management classic portal, on hello **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="38a7e-365">![使用者佈建](./media/active-directory-saas-servicenow-tutorial/IC769498.png "使用者佈建")</span><span class="sxs-lookup"><span data-stu-id="38a7e-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="38a7e-366">在 hello**輸入您 ServiceNow 認證 tooenable 自動使用者佈建**頁面上，提供下列組態設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-366">On hello **Enter your ServiceNow credentials tooenable automatic user provisioning** page, provide hello following configuration settings:</span></span>
   
     <span data-ttu-id="38a7e-367">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-367">a.</span></span> <span data-ttu-id="38a7e-368">在 hello **ServiceNow 執行個體名稱**文字方塊中，型別 hello ServiceNow 執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="38a7e-368">In hello **ServiceNow Instance Name** textbox, type hello ServiceNow instance name.</span></span>
   
     <span data-ttu-id="38a7e-369">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-369">b.</span></span> <span data-ttu-id="38a7e-370">在 hello **ServiceNow 管理使用者名稱**文字方塊中，型別 hello hello ServiceNow 管理員帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="38a7e-370">In hello **ServiceNow Admin User Name** textbox, type hello name of hello ServiceNow admin account.</span></span>
   
     <span data-ttu-id="38a7e-371">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-371">c.</span></span> <span data-ttu-id="38a7e-372">在 hello **ServiceNow 管理員密碼**文字方塊中，此帳戶類型 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="38a7e-372">In hello **ServiceNow Admin Password** textbox, type hello password for this account.</span></span>
   
     <span data-ttu-id="38a7e-373">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-373">d.</span></span> <span data-ttu-id="38a7e-374">按一下**驗證**tooverify 您的設定。</span><span class="sxs-lookup"><span data-stu-id="38a7e-374">Click **validate** tooverify your configuration.</span></span>
   
     <span data-ttu-id="38a7e-375">e.</span><span class="sxs-lookup"><span data-stu-id="38a7e-375">e.</span></span> <span data-ttu-id="38a7e-376">按一下 hello**下一步**按鈕 tooopen hello**後續步驟**頁面。</span><span class="sxs-lookup"><span data-stu-id="38a7e-376">Click hello **Next** button tooopen hello **Next steps** page.</span></span>
   
     <span data-ttu-id="38a7e-377">f.</span><span class="sxs-lookup"><span data-stu-id="38a7e-377">f.</span></span> <span data-ttu-id="38a7e-378">如果您想 tooprovision 所有使用者 toothis 應用程式，選取 「**hello 目錄 toothis 應用程式中的所有使用者帳戶自動佈都建**"。</span><span class="sxs-lookup"><span data-stu-id="38a7e-378">If you want tooprovision all users toothis application, select “**Automatically provision all user accounts in hello directory toothis application**”.</span></span> 
   
    <span data-ttu-id="38a7e-379">![後續步驟](./media/active-directory-saas-servicenow-tutorial/IC698804.png "後續步驟")</span><span class="sxs-lookup"><span data-stu-id="38a7e-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="38a7e-380">g.</span><span class="sxs-lookup"><span data-stu-id="38a7e-380">g.</span></span> <span data-ttu-id="38a7e-381">在 hello**後續步驟**頁面上，按一下**完成**toosave 您的設定。</span><span class="sxs-lookup"><span data-stu-id="38a7e-381">On hello **Next steps** page, click **Complete** toosave your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38a7e-382">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="38a7e-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="38a7e-383">在本節中，您可以建立測試使用者呼叫許 Simon hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="38a7e-383">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="38a7e-385">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="38a7e-385">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="38a7e-386">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-386">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="38a7e-388">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="38a7e-388">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="38a7e-389">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-389">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38a7e-391">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-391">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="38a7e-393">在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-393">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="38a7e-395">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-395">a.</span></span> <span data-ttu-id="38a7e-396">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="38a7e-397">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-397">b.</span></span> <span data-ttu-id="38a7e-398">在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-398">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="38a7e-399">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-399">c.</span></span> <span data-ttu-id="38a7e-400">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-400">Click **Next**.</span></span>

6. <span data-ttu-id="38a7e-401">在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-401">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="38a7e-403">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-403">a.</span></span> <span data-ttu-id="38a7e-404">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-404">In hello **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="38a7e-405">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-405">b.</span></span> <span data-ttu-id="38a7e-406">在 hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-406">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="38a7e-407">c.</span><span class="sxs-lookup"><span data-stu-id="38a7e-407">c.</span></span> <span data-ttu-id="38a7e-408">在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-408">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="38a7e-409">d.</span><span class="sxs-lookup"><span data-stu-id="38a7e-409">d.</span></span> <span data-ttu-id="38a7e-410">在 hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-410">In hello **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="38a7e-411">e.</span><span class="sxs-lookup"><span data-stu-id="38a7e-411">e.</span></span> <span data-ttu-id="38a7e-412">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="38a7e-412">Click **Next**.</span></span>

7. <span data-ttu-id="38a7e-413">在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-413">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="38a7e-415">在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="38a7e-415">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="38a7e-417">a.</span><span class="sxs-lookup"><span data-stu-id="38a7e-417">a.</span></span> <span data-ttu-id="38a7e-418">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-418">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="38a7e-419">b.</span><span class="sxs-lookup"><span data-stu-id="38a7e-419">b.</span></span> <span data-ttu-id="38a7e-420">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="38a7e-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="38a7e-421">建立 ServiceNow 測試使用者</span><span class="sxs-lookup"><span data-stu-id="38a7e-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="38a7e-422">在本節中，您要在 ServiceNow 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="38a7e-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="38a7e-423">在本節中，您要在 ServiceNow 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="38a7e-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="38a7e-424">如果您不知道如何 tooadd 您的 ServiceNow 或 ServiceNow Express 中的使用者帳戶，請連絡 ServiceNow 技術支援小組。</span><span class="sxs-lookup"><span data-stu-id="38a7e-424">If you don't know how tooadd a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="38a7e-425">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="38a7e-425">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="38a7e-426">在本節中，您可以授與他們存取 tooServiceNow 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="38a7e-426">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceNow.</span></span>

![指派使用者][200] 

<span data-ttu-id="38a7e-428">**tooassign 許 Simon tooServiceNow，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="38a7e-428">**tooassign Britta Simon tooServiceNow, perform hello following steps:**</span></span>

1. <span data-ttu-id="38a7e-429">Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="38a7e-429">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![指派使用者][201] 

2. <span data-ttu-id="38a7e-431">在 [hello] 應用程式清單中，選取**ServiceNow**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-431">In hello applications list, select **ServiceNow**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="38a7e-433">在 hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-433">In hello menu on hello top, click **Users**.</span></span>
   
    ![指派使用者][203] 

4. <span data-ttu-id="38a7e-435">在 hello 所有使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-435">In hello All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="38a7e-436">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="38a7e-436">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="38a7e-438">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="38a7e-438">Testing single sign-on</span></span>
<span data-ttu-id="38a7e-439">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="38a7e-439">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="38a7e-440">當您按一下 hello ServiceNow 磚 hello 存取面板中的時，您應該取得自動登入 tooyour ServiceNow 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="38a7e-440">When you click hello ServiceNow tile in hello Access Panel, you should get automatically signed-on tooyour ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38a7e-441">其他資源</span><span class="sxs-lookup"><span data-stu-id="38a7e-441">Additional resources</span></span>
* [<span data-ttu-id="38a7e-442">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38a7e-442">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38a7e-443">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="38a7e-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
