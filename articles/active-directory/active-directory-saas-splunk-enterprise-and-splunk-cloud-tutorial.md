---
title: "教學課程：Azure Active Directory 與 Splunk Enterprise and Splunk Cloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Splunk 企業和 Splunk 雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="252ba-103">教學課程：Azure Active Directory 與 Splunk Enterprise and Splunk Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="252ba-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="252ba-104">在此教學課程中，您學會如何 toointegrate Splunk 企業和 Splunk 雲端與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="252ba-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="252ba-105">與 Azure AD 整合 Splunk 企業和 Splunk 雲端可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="252ba-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="252ba-106">您可以控制可以存取 Azure AD 中 tooSplunk 企業和 Splunk 雲端</span><span class="sxs-lookup"><span data-stu-id="252ba-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="252ba-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooSplunk 企業和雲端 Splunk 單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="252ba-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="252ba-108">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="252ba-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="252ba-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="252ba-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="252ba-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="252ba-110">Prerequisites</span></span>

<span data-ttu-id="252ba-111">tooconfigure Splunk 企業與 Splunk 雲端的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="252ba-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="252ba-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="252ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="252ba-113">已啟用 Splunk Enterprise or Splunk Cloud SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="252ba-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="252ba-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="252ba-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="252ba-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="252ba-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="252ba-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="252ba-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="252ba-117">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="252ba-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="252ba-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="252ba-118">Scenario description</span></span>
<span data-ttu-id="252ba-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="252ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="252ba-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="252ba-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="252ba-121">從 hello 圖庫加入 Splunk 企業和 Splunk 雲端</span><span class="sxs-lookup"><span data-stu-id="252ba-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="252ba-122">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="252ba-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="252ba-123">從 hello 圖庫新增 Splunk 企業和 Splunk 雲端</span><span class="sxs-lookup"><span data-stu-id="252ba-123">Add Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="252ba-124">tooconfigure hello 整合 Splunk 企業和 Splunk 雲端到 Azure AD，您需要 tooadd Splunk 企業和 Splunk 雲端 hello 圖庫 tooyour 清單中的受管理 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="252ba-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="252ba-125">**tooadd Splunk 企業和 Splunk 雲端 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="252ba-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="252ba-126">在 [hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="252ba-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![Active Directory][1]

2. <span data-ttu-id="252ba-128">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="252ba-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="252ba-129">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="252ba-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![應用程式][2]

4. <span data-ttu-id="252ba-131">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="252ba-131">Click **Add** at hello bottom of hello page.</span></span>

    ![應用程式][3]

5. <span data-ttu-id="252ba-133">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="252ba-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>

    ![應用程式][4]

6. <span data-ttu-id="252ba-135">在 [hello] 搜尋方塊中，輸入**Splunk 企業或 Splunk 雲端**。</span><span class="sxs-lookup"><span data-stu-id="252ba-135">In hello search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="252ba-137">在 [hello] 結果窗格中，選取 [ **Splunk 企業和 Splunk 雲端**，然後按一下 [**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="252ba-137">In hello results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="252ba-139">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="252ba-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="252ba-140">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Splunk Enterprise and Splunk Cloud 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="252ba-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="252ba-141">單一登入 toowork，Azure AD 需要 tooknow Splunk 企業和 Splunk 雲端中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="252ba-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="252ba-142">換句話說，Azure AD 使用者與 hello Splunk 企業和 Splunk 雲端中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="252ba-142">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="252ba-143">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Splunk 企業和 Splunk 雲端中。</span><span class="sxs-lookup"><span data-stu-id="252ba-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="252ba-144">tooconfigure 及測試 Azure AD 單一登入與 Splunk 企業和 Splunk 雲端，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="252ba-144">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="252ba-145">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="252ba-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="252ba-146">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="252ba-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="252ba-147">**[建立測試使用者 Splunk 企業和 Splunk 雲端](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** -toohave 許 Simon Splunk 企業中，她連結的 toohello Azure AD 表示 Splunk 雲端對應項目。</span><span class="sxs-lookup"><span data-stu-id="252ba-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="252ba-148">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="252ba-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="252ba-149">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="252ba-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="252ba-150">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="252ba-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="252ba-151">在本節中，您可以 hello 傳統入口網站中啟用 Azure AD SSO，並 Splunk 企業和 Splunk 雲端應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="252ba-151">In this section, you enable Azure AD SSO in hello classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="252ba-152">**Azure AD 單一登入的 tooconfigure Splunk 企業與 Splunk 雲端執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="252ba-152">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="252ba-153">Hello 傳統入口網站中，在 [hello **Splunk 企業和 Splunk 雲端**應用程式整合頁面上，按一下 [**設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="252ba-153">In hello classic portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
     
    ![設定單一登入][6] 

2. <span data-ttu-id="252ba-155">在 hello**要如何讓使用者 toosign 上 tooSplunk 企業和 Splunk 雲端**頁面上，選取**Azure AD 單一登入**，然後按一下 [**下一步**。</span><span class="sxs-lookup"><span data-stu-id="252ba-155">On hello **How would you like users toosign on tooSplunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="252ba-157">在 [hello**設定應用程式設定**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="252ba-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="252ba-159">在 [hello**登入 URL**文字方塊中，您的使用者 toosign 上 tooyour Splunk 企業和使用下列模式的 hello Splunk 雲端應用程式所使用的型別 hello URL:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="252ba-159">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour Splunk Enterprise and Splunk Cloud application using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="252ba-160">在 [hello**識別碼**Splunk 伺服器的型別 hello URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="252ba-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="252ba-161">在 [hello**回覆 URL**文字方塊中，以下列模式的 hello 類型 hello URL:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="252ba-161">In hello **Reply URL** textbox, type hello URL with hello following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="252ba-162">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="252ba-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="252ba-163">在 [hello **Splunk 企業和 Splunk 雲端在設定單一登入**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="252ba-163">On hello **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="252ba-165">按一下**下載中繼資料**，然後儲存您的電腦上的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="252ba-165">Click **Download metadata**, and then save hello file on your computer.</span></span>
  2. <span data-ttu-id="252ba-166">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="252ba-166">Click **Next**.</span></span>

5. <span data-ttu-id="252ba-167">tooget SSO 設定應用程式連絡 Splunk 企業和雲端 Splunk 支援小組，並提供 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="252ba-167">tooget SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with hello following:</span></span>

    * <span data-ttu-id="252ba-168">下載的 hello **federaton 中繼資料**</span><span class="sxs-lookup"><span data-stu-id="252ba-168">hello downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="252ba-169">Hello 傳統入口網站中選取 hello 單一登入組態確認，然後**下一步**。</span><span class="sxs-lookup"><span data-stu-id="252ba-169">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD 單一登入][10]

7. <span data-ttu-id="252ba-171">在 [hello**單一登入確認**頁面上，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="252ba-171">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD 單一登入][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="252ba-173">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="252ba-173">Create an Azure AD test user</span></span>
<span data-ttu-id="252ba-174">在本節中，您可以建立測試使用者呼叫許 Simon hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="252ba-174">In this section, you create a test user in hello classic portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][20]

<span data-ttu-id="252ba-176">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="252ba-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="252ba-177">在 [hello **Azure 傳統入口網站**，在 hello 左側的導覽窗格中，按一下**Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="252ba-177">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="252ba-179">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="252ba-179">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="252ba-180">toodisplay hello 清單中的使用者，hello hello 上方的功能表中按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="252ba-180">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="252ba-182">tooopen hello**新增使用者**對話方塊中，在 hello 下方的 hello 工具列中按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="252ba-182">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="252ba-184">在 [hello**告訴我們這位使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="252ba-184">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="252ba-186">針對 [使用者類型]，選取 [您組織中的新使用者]。</span><span class="sxs-lookup"><span data-stu-id="252ba-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="252ba-187">在 [hello 使用者名稱**文字方塊**，型別**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="252ba-187">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="252ba-188">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="252ba-188">Click **Next**.</span></span>

6.  <span data-ttu-id="252ba-189">在 [hello**使用者設定檔**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="252ba-189">On hello **User Profile** dialog page, perform hello following steps:</span></span>
  
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="252ba-191">在 [hello**名字**文字方塊中，輸入**許**。</span><span class="sxs-lookup"><span data-stu-id="252ba-191">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="252ba-192">在 [hello**姓氏**文字方塊中，輸入， **Simon**。</span><span class="sxs-lookup"><span data-stu-id="252ba-192">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="252ba-193">在 [hello**顯示名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="252ba-193">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="252ba-194">在 [hello**角色**清單中，選取**使用者**。</span><span class="sxs-lookup"><span data-stu-id="252ba-194">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="252ba-195">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="252ba-195">Click **Next**.</span></span>

7. <span data-ttu-id="252ba-196">在 [hello**取得暫時密碼**對話方塊頁面上，按一下 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="252ba-196">On hello **Get temporary password** dialog page, click **create**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="252ba-198">在 [hello**取得暫時密碼**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="252ba-198">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="252ba-200">請記下 hello hello 值**新密碼**。</span><span class="sxs-lookup"><span data-stu-id="252ba-200">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="252ba-201">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="252ba-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="252ba-202">建立 Splunk Enterprise and Splunk Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="252ba-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="252ba-203">在本節中，您要在 Splunk Enterprise and Splunk Cloud 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="252ba-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="252ba-204">請使用 Splunk 企業和雲端 Splunk 支援小組 tooadd hello 使用者在 hello Splunk 企業和 Splunk 雲端平台。</span><span class="sxs-lookup"><span data-stu-id="252ba-204">Please work with Splunk Enterprise and Splunk Cloud support team tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="252ba-205">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="252ba-205">Assign hello Azure AD test user</span></span>

<span data-ttu-id="252ba-206">在本節中，您可以啟用許 Simon toouse Azure SSOy 授與他們存取 tooSplunk 企業和 Splunk 雲端。</span><span class="sxs-lookup"><span data-stu-id="252ba-206">In this section, you enable Britta Simon toouse Azure SSOy granting her access tooSplunk Enterprise and Splunk Cloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="252ba-208">**tooassign 許 Simon tooSplunk 企業和 Splunk 雲端，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="252ba-208">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="252ba-209">Hello 傳統入口網站，tooopen hello 應用程式] 檢視，在 hello 目錄檢視中，按一下 [**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="252ba-209">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="252ba-211">在 [hello] 應用程式清單中，選取**Splunk 企業和 Splunk 雲端**。</span><span class="sxs-lookup"><span data-stu-id="252ba-211">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="252ba-213">在 [hello 最上層顯示 hello 功能表上，按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="252ba-213">In hello menu on hello top, click **Users**.</span></span>

    ![指派使用者][203]

4. <span data-ttu-id="252ba-215">在 hello 使用者清單中選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="252ba-215">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="252ba-216">在 hello hello 底部的工具列中按一下**指派**。</span><span class="sxs-lookup"><span data-stu-id="252ba-216">In hello toolbar on hello bottom, click **Assign**.</span></span>

    ![指派使用者][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="252ba-218">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="252ba-218">Test single sign-on</span></span>

<span data-ttu-id="252ba-219">在本節中，您可以測試使用存取面板 hello 您 Azure AD SSOonfiguration。</span><span class="sxs-lookup"><span data-stu-id="252ba-219">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="252ba-220">當您按一下 hello Splunk 企業和雲端 Splunk 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Splunk 企業和 Splunk 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="252ba-220">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="252ba-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="252ba-221">Additional resources</span></span>

* [<span data-ttu-id="252ba-222">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="252ba-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="252ba-223">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="252ba-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
