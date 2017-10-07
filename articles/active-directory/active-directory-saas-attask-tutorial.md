---
title: "教學課程： Azure Active Directory 整合與@Task|Microsoft 文件"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間和@Task。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="a19c6-103">教學課程：Azure Active Directory 與 @Task 整合</span><span class="sxs-lookup"><span data-stu-id="a19c6-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="a19c6-104">本教學課程的 hello 目標是 tooshow 您如何 toointegrate@Task與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a19c6-104">hello objective of this tutorial is tooshow you how toointegrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="a19c6-105">整合@Task與 Azure AD 為您提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a19c6-105">Integrating @Task with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="a19c6-106">您可以控制可以存取 Azure AD 中too@Task</span><span class="sxs-lookup"><span data-stu-id="a19c6-106">You can control in Azure AD who has access too@Task</span></span>
* <span data-ttu-id="a19c6-107">您可以讓的使用者登入取得 tooautomatically too@Task （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a19c6-107">You can enable your users tooautomatically get signed-on too@Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="a19c6-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="a19c6-108">You can manage your accounts in one central location - hello Azure classic Portal</span></span>

<span data-ttu-id="a19c6-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a19c6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a19c6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a19c6-110">Prerequisites</span></span>
<span data-ttu-id="a19c6-111">與 tooconfigure Azure AD 整合@Task，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a19c6-111">tooconfigure Azure AD integration with @Task, you need hello following items:</span></span>

* <span data-ttu-id="a19c6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a19c6-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a19c6-113">啟用 @Task 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a19c6-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a19c6-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a19c6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="a19c6-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a19c6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a19c6-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="a19c6-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a19c6-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="a19c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="a19c6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a19c6-118">Scenario Description</span></span>
<span data-ttu-id="a19c6-119">本教學課程的 hello 目標是 tooenable 您 tootest Azure AD 單一登入的測試環境中。</span><span class="sxs-lookup"><span data-stu-id="a19c6-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="a19c6-120">本教學課程所述的 hello 案例包含三個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a19c6-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="a19c6-121">加入@Task從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="a19c6-121">Adding @Task from hello gallery</span></span> 
2. <span data-ttu-id="a19c6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a19c6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-hello-gallery"></a><span data-ttu-id="a19c6-123">加入@Task從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="a19c6-123">Adding @Task from hello gallery</span></span>
<span data-ttu-id="a19c6-124">tooconfigure hello 整合@Task到 Azure AD，您需要 tooadd @Task hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a19c6-124">tooconfigure hello integration of @Task into Azure AD, you need tooadd @Task from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a19c6-125">**tooadd @Task hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a19c6-125">**tooadd @Task from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a19c6-126">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1] 
2. <span data-ttu-id="a19c6-128">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="a19c6-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="a19c6-129">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="a19c6-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![應用程式][2] 
4. <span data-ttu-id="a19c6-131">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="a19c6-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![應用程式][3] 
5. <span data-ttu-id="a19c6-133">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![應用程式][4] 
6. <span data-ttu-id="a19c6-135">在 [hello] 搜尋方塊中，輸入 **@Task** 。</span><span class="sxs-lookup"><span data-stu-id="a19c6-135">In hello search box, type **@Task**.</span></span>
   
    ![應用程式][5] 
7. <span data-ttu-id="a19c6-137">在 hello 結果窗格中，選取   **@Task** ，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a19c6-137">In hello results pane, select **@Task**, and then click **Complete** tooadd hello application.</span></span>
   
    ![應用程式][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a19c6-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a19c6-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a19c6-140">hello 本節的目標是您 tooconfigure 和測試 Azure AD 的單一登入與 tooshow@Task根據稱為 「 許 Simon"的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a19c6-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a19c6-141">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中@Tasktooan 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a19c6-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in @Task tooan user in Azure AD is.</span></span> <span data-ttu-id="a19c6-142">換句話說，Azure AD 使用者與 hello 中相關的使用者之間的連結關聯性@Task需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a19c6-142">In other words, a link relationship between an Azure AD user and hello related user in @Task needs toobe established.</span></span>   
<span data-ttu-id="a19c6-143">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**中@Task。</span><span class="sxs-lookup"><span data-stu-id="a19c6-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in @Task.</span></span>

<span data-ttu-id="a19c6-144">tooconfigure 和測試 Azure AD 單一登入與@Task，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a19c6-144">tooconfigure and test Azure AD single sign-on with @Task, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a19c6-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a19c6-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a19c6-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a19c6-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a19c6-147">**[建立@Tasktest使用者](#creating-a-halogen-software-test-user)** -toohave 的對應項目中的許 Simon@Taskthat是連結的 toohello Azure AD 的她的表示法。</span><span class="sxs-lookup"><span data-stu-id="a19c6-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in @Taskthat is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a19c6-148">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a19c6-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a19c6-149">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a19c6-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a19c6-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a19c6-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="a19c6-151">hello 本節目標在於 tooenable Azure AD 單一登入 Azure 傳統入口網站 hello 和 tooconfigure 單一登入您@Task應用程式。</span><span class="sxs-lookup"><span data-stu-id="a19c6-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your @Task application.</span></span>

<span data-ttu-id="a19c6-152">**使用 Azure AD 單一登入 tooconfigure @Task，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a19c6-152">**tooconfigure Azure AD single sign-on with @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="a19c6-153">在 Azure 傳統入口網站，在 hello hello  **@Task** 應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a19c6-153">In hello Azure classic portal, on hello **@Task** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![設定單一登入][6] 
2. <span data-ttu-id="a19c6-155">在 hello**如何想您使用者 toosign 上too@Task**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-155">On hello **How would you like users toosign on too@Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD 單一登入][7] 
3. <span data-ttu-id="a19c6-157">在 hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a19c6-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![設定 App 設定][8] 
   
     <span data-ttu-id="a19c6-159">a.</span><span class="sxs-lookup"><span data-stu-id="a19c6-159">a.</span></span> <span data-ttu-id="a19c6-160">在 hello**登入 URL**文字方塊中，供您使用者 toosign 上 tooyour 類型 hello URL@Task應用程式 (例如：*https://<Tenant name>.attask ondemand.com*)。</span><span class="sxs-lookup"><span data-stu-id="a19c6-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="a19c6-161">b.</span><span class="sxs-lookup"><span data-stu-id="a19c6-161">b.</span></span> <span data-ttu-id="a19c6-162">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a19c6-162">Click **Next**.</span></span>
4. <span data-ttu-id="a19c6-163">在 hello**設定單一登入在@Task**頁面上，按一下**下載中繼資料**，儲存在本機電腦上的 hello 中繼資料檔案，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-163">On hello **Configure single sign-on at @Task** page, click **Download metadata**, save hello metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![何謂 Azure AD Connect][9] 
5. <span data-ttu-id="a19c6-165">登入 tooyour@Task以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="a19c6-165">Sign-on tooyour @Task company site as administrator.</span></span>
6. <span data-ttu-id="a19c6-166">跳過**單一登入組態**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-166">Go too**Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="a19c6-167">在 [hello**單一登入**] 對話方塊中，執行下列步驟的 hello</span><span class="sxs-lookup"><span data-stu-id="a19c6-167">On hello **Single Sign-On** dialog, perform hello following steps</span></span>
   
    ![設定單一登入][23]
   
    <span data-ttu-id="a19c6-169">a.</span><span class="sxs-lookup"><span data-stu-id="a19c6-169">a.</span></span> <span data-ttu-id="a19c6-170">針對 [類型]，選取 [SAML 2.0]。</span><span class="sxs-lookup"><span data-stu-id="a19c6-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="a19c6-171">b.</span><span class="sxs-lookup"><span data-stu-id="a19c6-171">b.</span></span> <span data-ttu-id="a19c6-172">選取 [服務提供者識別碼]。</span><span class="sxs-lookup"><span data-stu-id="a19c6-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="a19c6-173">c.</span><span class="sxs-lookup"><span data-stu-id="a19c6-173">c.</span></span> <span data-ttu-id="a19c6-174">在 hello Azure 傳統入口網站中，複製 hello**遠端登入 URL**，然後將它貼入 hello**登入入口網站 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a19c6-174">On hello Azure classic portal, copy hello **Remote Login URL**, and then paste it into hello **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="a19c6-175">d.</span><span class="sxs-lookup"><span data-stu-id="a19c6-175">d.</span></span> <span data-ttu-id="a19c6-176">在 hello Azure 傳統入口網站中，複製 hello**單一登出服務 URL**，然後將它貼入 hello**登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a19c6-176">On hello Azure classic portal, copy hello **Single Sign-Out Service URL**, and then paste it into hello **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="a19c6-177">e.</span><span class="sxs-lookup"><span data-stu-id="a19c6-177">e.</span></span> <span data-ttu-id="a19c6-178">在 hello Azure 傳統入口網站中，複製 hello**變更密碼 URL**，然後將它貼入 hello**變更密碼 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a19c6-178">On hello Azure classic portal, copy hello **Change Password URL**, and then paste it into hello **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="a19c6-179">f.</span><span class="sxs-lookup"><span data-stu-id="a19c6-179">f.</span></span> <span data-ttu-id="a19c6-180">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="a19c6-180">Click **Save**.</span></span>
8. <span data-ttu-id="a19c6-181">在 hello Azure 傳統入口網站，選取 hello 單一登入組態確認，，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-181">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![何謂 Azure AD Connect][10]
9. <span data-ttu-id="a19c6-183">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-183">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![何謂 Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a19c6-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a19c6-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="a19c6-186">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 傳統入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a19c6-186">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>  

![建立 Azure AD 使用者][20]

<span data-ttu-id="a19c6-188">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a19c6-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a19c6-189">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-189">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="a19c6-191">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="a19c6-191">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="a19c6-192">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-192">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="a19c6-194">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-194">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="a19c6-196">在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a19c6-196">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="a19c6-198">a.</span><span class="sxs-lookup"><span data-stu-id="a19c6-198">a.</span></span> <span data-ttu-id="a19c6-199">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="a19c6-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="a19c6-200">b.</span><span class="sxs-lookup"><span data-stu-id="a19c6-200">b.</span></span> <span data-ttu-id="a19c6-201">在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-201">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="a19c6-202">c.</span><span class="sxs-lookup"><span data-stu-id="a19c6-202">c.</span></span> <span data-ttu-id="a19c6-203">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a19c6-203">Click **Next**.</span></span>
6. <span data-ttu-id="a19c6-204">在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a19c6-204">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="a19c6-206">a.</span><span class="sxs-lookup"><span data-stu-id="a19c6-206">a.</span></span> <span data-ttu-id="a19c6-207">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-207">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="a19c6-208">b.</span><span class="sxs-lookup"><span data-stu-id="a19c6-208">b.</span></span> <span data-ttu-id="a19c6-209">在 hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-209">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="a19c6-210">c.</span><span class="sxs-lookup"><span data-stu-id="a19c6-210">c.</span></span> <span data-ttu-id="a19c6-211">在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-211">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="a19c6-212">d.</span><span class="sxs-lookup"><span data-stu-id="a19c6-212">d.</span></span> <span data-ttu-id="a19c6-213">在 hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-213">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="a19c6-214">e.</span><span class="sxs-lookup"><span data-stu-id="a19c6-214">e.</span></span> <span data-ttu-id="a19c6-215">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a19c6-215">Click **Next**.</span></span>

7. <span data-ttu-id="a19c6-216">在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-216">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="a19c6-218">在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a19c6-218">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="a19c6-220">a.</span><span class="sxs-lookup"><span data-stu-id="a19c6-220">a.</span></span> <span data-ttu-id="a19c6-221">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-221">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="a19c6-222">b.</span><span class="sxs-lookup"><span data-stu-id="a19c6-222">b.</span></span> <span data-ttu-id="a19c6-223">按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="a19c6-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="a19c6-224">建立 @Task 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a19c6-224">Creating an @Task test user</span></span>
<span data-ttu-id="a19c6-225">hello 本節目標在於 toocreate 使用者，在呼叫許 Simon @Task。</span><span class="sxs-lookup"><span data-stu-id="a19c6-225">hello objective of this section is toocreate a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="a19c6-226">**使用者在呼叫許 Simon toocreate @Task，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a19c6-226">**toocreate a user called Britta Simon in @Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="a19c6-227">登入 tooyour@Task以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="a19c6-227">Sign on tooyour @Task company site as administrator.</span></span>
2. <span data-ttu-id="a19c6-228">在 hello 最上層顯示 hello 功能表上，按一下**人員**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-228">In hello menu on hello top, click **People**.</span></span>
3. <span data-ttu-id="a19c6-229">按一下 [新增人員] 。</span><span class="sxs-lookup"><span data-stu-id="a19c6-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="a19c6-230">在 hello 新增人員 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a19c6-230">On hello New Person dialog, perform hello following steps:</span></span>
   
    ![建立 @Task 測試使用者][21] 
   
    <span data-ttu-id="a19c6-232">a.</span><span class="sxs-lookup"><span data-stu-id="a19c6-232">a.</span></span> <span data-ttu-id="a19c6-233">在 hello**名字**文字方塊中，輸入 「 許"。</span><span class="sxs-lookup"><span data-stu-id="a19c6-233">In hello **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="a19c6-234">b.</span><span class="sxs-lookup"><span data-stu-id="a19c6-234">b.</span></span> <span data-ttu-id="a19c6-235">在 hello**姓氏**文字方塊中，輸入 「 Simon"。</span><span class="sxs-lookup"><span data-stu-id="a19c6-235">In hello **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="a19c6-236">c.</span><span class="sxs-lookup"><span data-stu-id="a19c6-236">c.</span></span> <span data-ttu-id="a19c6-237">在 hello**電子郵件地址**文字方塊中，輸入 Azure Active Directory 中許 Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="a19c6-237">In hello **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="a19c6-238">d.</span><span class="sxs-lookup"><span data-stu-id="a19c6-238">d.</span></span> <span data-ttu-id="a19c6-239">按一下 [新增人員] 。</span><span class="sxs-lookup"><span data-stu-id="a19c6-239">Click **Add Person**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a19c6-240">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a19c6-240">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="a19c6-241">本節 hello 目標是 tooenabling 許 Simon toouse Azure 單一登入授與他們存取too@Task。</span><span class="sxs-lookup"><span data-stu-id="a19c6-241">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access too@Task.</span></span>

![指派使用者][200] 

<span data-ttu-id="a19c6-243">**tooassign 許 Simon too@Task，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a19c6-243">**tooassign Britta Simon too@Task, perform hello following steps:**</span></span>

1. <span data-ttu-id="a19c6-244">在 hello Azure 傳統入口網站，tooopen hello 應用程式 檢視，在 hello 目錄檢視中，按一下 **應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="a19c6-244">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![指派使用者][201] 
2. <span data-ttu-id="a19c6-246">在 [hello] 應用程式清單中，選取 **@Task** 。</span><span class="sxs-lookup"><span data-stu-id="a19c6-246">In hello applications list, select **@Task**.</span></span>
   
    ![指派使用者][202] 
3. <span data-ttu-id="a19c6-248">在 hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-248">In hello menu on hello top, click **Users**.</span></span>
   
    ![指派使用者][203] 
4. <span data-ttu-id="a19c6-250">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-250">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="a19c6-251">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="a19c6-251">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![指派使用者][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="a19c6-253">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a19c6-253">Testing Single Sign-On</span></span>
<span data-ttu-id="a19c6-254">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="a19c6-254">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="a19c6-255">當您按一下 hello@Task以並排顯示 hello 存取面板中，您應該取得自動登入 tooyour@Task應用程式。</span><span class="sxs-lookup"><span data-stu-id="a19c6-255">When you click hello @Task tile in hello Access Panel, you should get automatically signed-on tooyour @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a19c6-256">其他資源</span><span class="sxs-lookup"><span data-stu-id="a19c6-256">Additional Resources</span></span>
* [<span data-ttu-id="a19c6-257">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a19c6-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a19c6-258">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a19c6-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






