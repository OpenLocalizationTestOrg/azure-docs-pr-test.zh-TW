---
title: "教學課程：Azure Active Directory 與 Halosys 整合 | Microsoft Docs"
description: "了解如何使用 Azure Active Directory tooenable toouse Halosys 單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a><span data-ttu-id="728bf-103">教學課程：Azure Active Directory 與 Halosys 整合</span><span class="sxs-lookup"><span data-stu-id="728bf-103">Tutorial: Azure Active Directory integration with Halosys</span></span>

<span data-ttu-id="728bf-104">在此教學課程中，您學會如何 toointegrate Halosys 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="728bf-104">In this tutorial, you learn how toointegrate Halosys with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="728bf-105">與 Azure AD 整合 Halosys 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="728bf-105">Integrating Halosys with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="728bf-106">您可以控制存取 tooHalosys Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="728bf-106">You can control in Azure AD who has access tooHalosys</span></span>
- <span data-ttu-id="728bf-107">您可以啟用您的使用者 tooautomatically get 登入 tooHalosys （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="728bf-107">You can enable your users tooautomatically get signed-on tooHalosys (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="728bf-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="728bf-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="728bf-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="728bf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="728bf-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="728bf-110">Prerequisites</span></span>

<span data-ttu-id="728bf-111">tooconfigure Halosys 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="728bf-111">tooconfigure Azure AD integration with Halosys, you need hello following items:</span></span>

- <span data-ttu-id="728bf-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="728bf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="728bf-113">已啟用 Halosys 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="728bf-113">A Halosys single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="728bf-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="728bf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="728bf-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="728bf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="728bf-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="728bf-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="728bf-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="728bf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="728bf-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="728bf-118">Scenario description</span></span>
<span data-ttu-id="728bf-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="728bf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="728bf-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="728bf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="728bf-121">從 hello 圖庫加入 Halosys</span><span class="sxs-lookup"><span data-stu-id="728bf-121">Adding Halosys from hello gallery</span></span>
2. <span data-ttu-id="728bf-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="728bf-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-halosys-from-hello-gallery"></a><span data-ttu-id="728bf-123">從 hello 圖庫加入 Halosys</span><span class="sxs-lookup"><span data-stu-id="728bf-123">Adding Halosys from hello gallery</span></span>
<span data-ttu-id="728bf-124">tooconfigure hello 整合 Halosys 到 Azure AD，您需要 tooadd Halosys hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="728bf-124">tooconfigure hello integration of Halosys into Azure AD, you need tooadd Halosys from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="728bf-125">**tooadd Halosys 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="728bf-125">**tooadd Halosys from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="728bf-126">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="728bf-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]
2. <span data-ttu-id="728bf-128">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="728bf-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="728bf-129">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="728bf-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![應用程式][2]

4. <span data-ttu-id="728bf-131">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="728bf-131">Click **Add** at hello bottom of hello page.</span></span>

    ![應用程式][3]

5. <span data-ttu-id="728bf-133">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="728bf-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![應用程式][4]

6. <span data-ttu-id="728bf-135">在 [hello] 搜尋方塊中，輸入**Halosys**。</span><span class="sxs-lookup"><span data-stu-id="728bf-135">In hello search box, type **Halosys**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. <span data-ttu-id="728bf-137">在 hello 結果窗格中，選取  **Halosys**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="728bf-137">In hello results pane, select **Halosys**, and then click **Complete** tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="728bf-139">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="728bf-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="728bf-140">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Halosys 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="728bf-140">In this section, you configure and test Azure AD single sign-on with Halosys based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="728bf-141">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Halosys 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="728bf-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halosys is tooa user in Azure AD.</span></span> <span data-ttu-id="728bf-142">換句話說，Azure AD 使用者與 hello Halosys 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="728bf-142">In other words, a link relationship between an Azure AD user and hello related user in Halosys needs toobe established.</span></span>

<span data-ttu-id="728bf-143">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Halosys 中。</span><span class="sxs-lookup"><span data-stu-id="728bf-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Halosys.</span></span>

<span data-ttu-id="728bf-144">tooconfigure 及 Halosys 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="728bf-144">tooconfigure and test Azure AD single sign-on with Halosys, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="728bf-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="728bf-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="728bf-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="728bf-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="728bf-147">**[建立測試使用者 Halosys](#creating-a-halosys-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 表示她的 Halosys 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="728bf-147">**[Creating a Halosys test user](#creating-a-halosys-test-user)** - toohave a counterpart of Britta Simon in Halosys that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="728bf-148">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="728bf-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="728bf-149">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="728bf-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="728bf-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="728bf-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="728bf-151">在本節中，您可以啟用 Azure AD 單一登入 hello 傳統入口網站中，並 Halosys 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="728bf-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Halosys application.</span></span>


<span data-ttu-id="728bf-152">**tooconfigure Azure AD 單一登入與 Halosys，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="728bf-152">**tooconfigure Azure AD single sign-on with Halosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="728bf-153">Hello 傳統入口網站中，在 hello **Halosys**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="728bf-153">In hello classic portal, on hello **Halosys** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![設定單一登入][6] 

2. <span data-ttu-id="728bf-155">在 hello**如何想您使用者 toosign tooHalosys 上**頁面上，選取**Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="728bf-155">On hello **How would you like users toosign on tooHalosys** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. <span data-ttu-id="728bf-157">在 hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="728bf-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    <span data-ttu-id="728bf-159">a.</span><span class="sxs-lookup"><span data-stu-id="728bf-159">a.</span></span> <span data-ttu-id="728bf-160">在 hello**登入 URL**文字方塊中，應用程式所使用的使用者 toosign 上 tooyour Halosys 使用 hello 遵循模式的型別 hello URL: `https://<company-name>.Halosys.com/client-api/api`。</span><span class="sxs-lookup"><span data-stu-id="728bf-160">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Halosys application using hello following pattern: `https://<company-name>.Halosys.com/client-api/api`.</span></span>

    <span data-ttu-id="728bf-161">b.In hello**識別項 URL** hello 遵循模式中的型別 hello URL 文字方塊中： `https://<company-name>.Halosys.com`。</span><span class="sxs-lookup"><span data-stu-id="728bf-161">b.In hello **Identifier URL** textbox, type hello URL in hello following pattern: `https://<company-name>.Halosys.com`.</span></span> 
         
4. <span data-ttu-id="728bf-162">在 hello **Halosys 在設定單一登入**頁面上，按一下**下載中繼資料**，然後儲存您的電腦上的 hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="728bf-162">On hello **Configure single sign-on at Halosys** page, click **Download metadata**, and then save hello file on your computer:</span></span>

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. <span data-ttu-id="728bf-164">設定應用程式的 SSO tooget 連絡 Halosys 支援小組，並提供他們最 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="728bf-164">tooget SSO configured for your application, contact Halosys support team and provide them with hello following:</span></span>

    <span data-ttu-id="728bf-165">• hello 下載**中繼資料檔案**</span><span class="sxs-lookup"><span data-stu-id="728bf-165">• hello downloaded **metadata file**</span></span>
    
    <span data-ttu-id="728bf-166">• hello **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="728bf-166">• hello **SAML SSO URL**</span></span>
    

6. <span data-ttu-id="728bf-167">Hello 傳統入口網站中選取 hello 單一登入組態確認，然後**下一步**。</span><span class="sxs-lookup"><span data-stu-id="728bf-167">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD 單一登入][10]

7. <span data-ttu-id="728bf-169">在 hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="728bf-169">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD 單一登入][11]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="728bf-171">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="728bf-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="728bf-172">在本節中，您可以建立測試使用者呼叫許 Simon hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="728bf-172">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>


![建立 Azure AD 使用者][20]

<span data-ttu-id="728bf-174">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="728bf-174">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="728bf-175">在 hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="728bf-175">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="728bf-177">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="728bf-177">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="728bf-178">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="728bf-178">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="728bf-180">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="728bf-180">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="728bf-182">在 hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="728bf-182">On hello **Tell us about this user** dialog page, perform hello following steps:  ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png)</span></span> 

    <span data-ttu-id="728bf-183">a.</span><span class="sxs-lookup"><span data-stu-id="728bf-183">a.</span></span> <span data-ttu-id="728bf-184">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="728bf-184">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="728bf-185">b.</span><span class="sxs-lookup"><span data-stu-id="728bf-185">b.</span></span> <span data-ttu-id="728bf-186">在 hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="728bf-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="728bf-187">c.</span><span class="sxs-lookup"><span data-stu-id="728bf-187">c.</span></span> <span data-ttu-id="728bf-188">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="728bf-188">Click **Next**.</span></span>

6.  <span data-ttu-id="728bf-189">在 hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="728bf-189">On hello **User Profile** dialog page, perform hello following steps: ![Creating an Azure AD test user](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png)</span></span> 

    <span data-ttu-id="728bf-190">a.</span><span class="sxs-lookup"><span data-stu-id="728bf-190">a.</span></span> <span data-ttu-id="728bf-191">在 hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="728bf-191">In hello **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="728bf-192">b.</span><span class="sxs-lookup"><span data-stu-id="728bf-192">b.</span></span> <span data-ttu-id="728bf-193">在 hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="728bf-193">In hello **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="728bf-194">c.</span><span class="sxs-lookup"><span data-stu-id="728bf-194">c.</span></span> <span data-ttu-id="728bf-195">在 hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="728bf-195">In hello **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="728bf-196">d.</span><span class="sxs-lookup"><span data-stu-id="728bf-196">d.</span></span> <span data-ttu-id="728bf-197">在 hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="728bf-197">In hello **Role** list, select **User**.</span></span>

    <span data-ttu-id="728bf-198">e.</span><span class="sxs-lookup"><span data-stu-id="728bf-198">e.</span></span> <span data-ttu-id="728bf-199">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="728bf-199">Click **Next**.</span></span>

7. <span data-ttu-id="728bf-200">在 hello**取得暫時密碼**對話方塊頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="728bf-200">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="728bf-202">在 hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="728bf-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="728bf-204">a.</span><span class="sxs-lookup"><span data-stu-id="728bf-204">a.</span></span> <span data-ttu-id="728bf-205">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="728bf-205">Write down hello value of hello **New Password**.</span></span>

    <span data-ttu-id="728bf-206">b.</span><span class="sxs-lookup"><span data-stu-id="728bf-206">b.</span></span> <span data-ttu-id="728bf-207">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="728bf-207">Click **Complete**.</span></span>   



### <a name="creating-a-halosys-test-user"></a><span data-ttu-id="728bf-208">建立 Halosys 測試使用者</span><span class="sxs-lookup"><span data-stu-id="728bf-208">Creating a Halosys test user</span></span>

<span data-ttu-id="728bf-209">在本節中，您要在 Halosys 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="728bf-209">In this section, you create a user called Britta Simon in Halosys.</span></span> <span data-ttu-id="728bf-210">請使用 Halosys 支援小組 tooadd hello 使用者在 hello Halosys 平台。</span><span class="sxs-lookup"><span data-stu-id="728bf-210">Please work with Halosys support team tooadd hello users in hello Halosys platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="728bf-211">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="728bf-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="728bf-212">在本節中，您可以授與他們存取 tooHalosys 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="728bf-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHalosys.</span></span>

![指派使用者][200] 

<span data-ttu-id="728bf-214">**tooassign 許 Simon tooHalosys，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="728bf-214">**tooassign Britta Simon tooHalosys, perform hello following steps:**</span></span>

1. <span data-ttu-id="728bf-215">Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="728bf-215">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="728bf-217">在 [hello] 應用程式清單中，選取**Halosys**。</span><span class="sxs-lookup"><span data-stu-id="728bf-217">In hello applications list, select **Halosys**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. <span data-ttu-id="728bf-219">在 hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="728bf-219">In hello menu on hello top, click **Users**.</span></span>

    ![指派使用者][203]

4. <span data-ttu-id="728bf-221">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="728bf-221">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="728bf-222">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="728bf-222">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![指派使用者][205]


### <a name="testing-single-sign-on"></a><span data-ttu-id="728bf-224">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="728bf-224">Testing single sign-on</span></span>

<span data-ttu-id="728bf-225">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="728bf-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="728bf-226">當您按一下的 hello Halosys 磚 hello 存取面板中時，您應該取得自動登入 tooyour Halosys 應用程式。</span><span class="sxs-lookup"><span data-stu-id="728bf-226">When you click hello Halosys tile in hello Access Panel, you should get automatically signed-on tooyour Halosys application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="728bf-227">其他資源</span><span class="sxs-lookup"><span data-stu-id="728bf-227">Additional resources</span></span>

* [<span data-ttu-id="728bf-228">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="728bf-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="728bf-229">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="728bf-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
