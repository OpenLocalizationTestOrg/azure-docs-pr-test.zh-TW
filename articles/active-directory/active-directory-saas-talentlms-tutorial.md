---
title: "教學課程：Azure Active Directory 與 TalentLMS 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 TalentLMS 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="787e4-103">教學課程：Azure Active Directory 與 TalentLMS 整合</span><span class="sxs-lookup"><span data-stu-id="787e4-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="787e4-104">在此教學課程中，您學會如何 toointegrate TalentLMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="787e4-104">In this tutorial, you learn how toointegrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="787e4-105">整合 Azure AD 與 TalentLMS 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="787e4-105">Integrating TalentLMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="787e4-106">您可以控制存取 tooTalentLMS Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="787e4-106">You can control in Azure AD who has access tooTalentLMS</span></span>
- <span data-ttu-id="787e4-107">您可以啟用您的使用者 tooautomatically get 登入 tooTalentLMS （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="787e4-107">You can enable your users tooautomatically get signed-on tooTalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="787e4-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="787e4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="787e4-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="787e4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="787e4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="787e4-110">Prerequisites</span></span>

<span data-ttu-id="787e4-111">tooconfigure Azure AD 與 TalentLMS 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="787e4-111">tooconfigure Azure AD integration with TalentLMS, you need hello following items:</span></span>

- <span data-ttu-id="787e4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="787e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="787e4-113">已啟用 TalentLMS 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="787e4-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="787e4-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="787e4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="787e4-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="787e4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="787e4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="787e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="787e4-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="787e4-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="787e4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="787e4-118">Scenario description</span></span>
<span data-ttu-id="787e4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="787e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="787e4-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="787e4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="787e4-121">從 hello 圖庫加入 TalentLMS</span><span class="sxs-lookup"><span data-stu-id="787e4-121">Adding TalentLMS from hello gallery</span></span>
2. <span data-ttu-id="787e4-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="787e4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-hello-gallery"></a><span data-ttu-id="787e4-123">從 hello 圖庫加入 TalentLMS</span><span class="sxs-lookup"><span data-stu-id="787e4-123">Adding TalentLMS from hello gallery</span></span>
<span data-ttu-id="787e4-124">tooconfigure hello 整合 TalentLMS 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd TalentLMS。</span><span class="sxs-lookup"><span data-stu-id="787e4-124">tooconfigure hello integration of TalentLMS into Azure AD, you need tooadd TalentLMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="787e4-125">**tooadd TalentLMS 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="787e4-125">**tooadd TalentLMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="787e4-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="787e4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="787e4-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="787e4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="787e4-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="787e4-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="787e4-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="787e4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="787e4-133">在 [hello] 搜尋方塊中，輸入**TalentLMS**。</span><span class="sxs-lookup"><span data-stu-id="787e4-133">In hello search box, type **TalentLMS**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="787e4-135">在 hello 結果 窗格中，選取  **TalentLMS**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="787e4-135">In hello results panel, select **TalentLMS**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="787e4-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="787e4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="787e4-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 TalentLMS 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="787e4-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="787e4-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 TalentLMS 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="787e4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TalentLMS is tooa user in Azure AD.</span></span> <span data-ttu-id="787e4-140">換句話說，Azure AD 使用者與 hello TalentLMS 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="787e4-140">In other words, a link relationship between an Azure AD user and hello related user in TalentLMS needs toobe established.</span></span>

<span data-ttu-id="787e4-141">在 TalentLMS 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="787e4-141">In TalentLMS, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="787e4-142">tooconfigure 和測試 Azure AD 單一登入與 TalentLMS，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="787e4-142">tooconfigure and test Azure AD single sign-on with TalentLMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="787e4-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="787e4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="787e4-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="787e4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="787e4-145">**[建立測試使用者 TalentLMS](#creating-a-talentlms-test-user)**  -toohave 許 Simon TalentLMS 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="787e4-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - toohave a counterpart of Britta Simon in TalentLMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="787e4-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="787e4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="787e4-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="787e4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="787e4-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="787e4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="787e4-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 TalentLMS 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="787e4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="787e4-150">**tooconfigure Azure AD 單一登入與 TalentLMS，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="787e4-150">**tooconfigure Azure AD single sign-on with TalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="787e4-151">在 Azure 入口網站上 hello hello **TalentLMS**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="787e4-151">In hello Azure portal, on hello **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="787e4-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="787e4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="787e4-155">在 hello **TalentLMS 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="787e4-155">On hello **TalentLMS Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="787e4-157">a.</span><span class="sxs-lookup"><span data-stu-id="787e4-157">a.</span></span> <span data-ttu-id="787e4-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="787e4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="787e4-159">b.</span><span class="sxs-lookup"><span data-stu-id="787e4-159">b.</span></span> <span data-ttu-id="787e4-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="787e4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="787e4-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="787e4-161">These values are not real.</span></span> <span data-ttu-id="787e4-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="787e4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="787e4-163">請連絡[TalentLMS 用戶端支援小組](https://www.talentlms.com/contact)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="787e4-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="787e4-164">在 hello **SAML 簽章憑證**區段，複製 hello**指紋**hello 憑證中的值。</span><span class="sxs-lookup"><span data-stu-id="787e4-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="787e4-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="787e4-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="787e4-168">在 hello **TalentLMS 組態**區段中，按一下**設定 TalentLMS** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="787e4-168">On hello **TalentLMS Configuration** section, click **Configure TalentLMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="787e4-169">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="787e4-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="787e4-171">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour TalentLMS 公司網站。</span><span class="sxs-lookup"><span data-stu-id="787e4-171">In a different web browser window, log in tooyour TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="787e4-172">在 [hello**帳戶和設定**區段中，按一下 hello**使用者**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="787e4-172">In hello **Account & Settings** section, click hello **Users** tab.</span></span>
   
    <span data-ttu-id="787e4-173">![帳戶和設定](./media/active-directory-saas-talentlms-tutorial/IC777296.png "帳戶和設定")</span><span class="sxs-lookup"><span data-stu-id="787e4-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="787e4-174">按一下 [單一登入 (SSO)] 。</span><span class="sxs-lookup"><span data-stu-id="787e4-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="787e4-175">在 hello 單一登入區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="787e4-175">In hello Single Sign-On section, perform hello following steps:</span></span>
   
    <span data-ttu-id="787e4-176">![單一登入](./media/active-directory-saas-talentlms-tutorial/IC777297.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="787e4-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="787e4-177">a.</span><span class="sxs-lookup"><span data-stu-id="787e4-177">a.</span></span> <span data-ttu-id="787e4-178">從 hello **SSO 整合型別**清單中，選取**SAML 2.0**。</span><span class="sxs-lookup"><span data-stu-id="787e4-178">From hello **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="787e4-179">b.</span><span class="sxs-lookup"><span data-stu-id="787e4-179">b.</span></span> <span data-ttu-id="787e4-180">在 hello**身分識別提供者 (IDP)**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="787e4-180">In hello **Identity provider (IDP)** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="787e4-181">c.</span><span class="sxs-lookup"><span data-stu-id="787e4-181">c.</span></span> <span data-ttu-id="787e4-182">貼上 hello**指紋**值從 Azure 入口網站，將 hello**憑證指紋**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="787e4-182">Paste hello **Thumbprint** value from Azure portal into hello **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="787e4-183">d.</span><span class="sxs-lookup"><span data-stu-id="787e4-183">d.</span></span>  <span data-ttu-id="787e4-184">在 hello**遠端登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="787e4-184">In hello **Remote sign-in URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="787e4-185">e.</span><span class="sxs-lookup"><span data-stu-id="787e4-185">e.</span></span> <span data-ttu-id="787e4-186">在 hello**遠端登出 URL**文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="787e4-186">In hello **Remote sign-out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="787e4-187">f.</span><span class="sxs-lookup"><span data-stu-id="787e4-187">f.</span></span> <span data-ttu-id="787e4-188">填寫下列 hello:</span><span class="sxs-lookup"><span data-stu-id="787e4-188">Fill in hello following:</span></span> 

    * <span data-ttu-id="787e4-189">在 hello**目標識別碼**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="787e4-189">In hello **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="787e4-190">在 hello**名字**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="787e4-190">In hello **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="787e4-191">在 hello**姓氏**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="787e4-191">In hello **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="787e4-192">在 hello**電子郵件**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="787e4-192">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="787e4-193">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="787e4-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="787e4-194">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="787e4-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="787e4-195">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="787e4-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="787e4-196">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="787e4-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="787e4-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="787e4-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="787e4-198">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="787e4-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="787e4-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="787e4-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="787e4-201">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="787e4-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="787e4-203">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="787e4-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="787e4-205">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="787e4-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="787e4-207">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="787e4-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="787e4-209">a.</span><span class="sxs-lookup"><span data-stu-id="787e4-209">a.</span></span> <span data-ttu-id="787e4-210">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="787e4-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="787e4-211">b.</span><span class="sxs-lookup"><span data-stu-id="787e4-211">b.</span></span> <span data-ttu-id="787e4-212">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="787e4-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="787e4-213">c.</span><span class="sxs-lookup"><span data-stu-id="787e4-213">c.</span></span> <span data-ttu-id="787e4-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="787e4-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="787e4-215">d.</span><span class="sxs-lookup"><span data-stu-id="787e4-215">d.</span></span> <span data-ttu-id="787e4-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="787e4-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="787e4-217">建立 TalentLMS 測試使用者</span><span class="sxs-lookup"><span data-stu-id="787e4-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="787e4-218">tooenable Azure AD 使用者 toolog 中 tooTalentLMS，它們必須佈建到 TalentLMS。</span><span class="sxs-lookup"><span data-stu-id="787e4-218">tooenable Azure AD users toolog in tooTalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="787e4-219">在 TalentLMS 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="787e4-219">In hello case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="787e4-220">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="787e4-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="787e4-221">登入 tooyour **TalentLMS**租用戶。</span><span class="sxs-lookup"><span data-stu-id="787e4-221">Log in tooyour **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="787e4-222">按一下 使用者，然後按一下加入使用者。</span><span class="sxs-lookup"><span data-stu-id="787e4-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="787e4-223">在 hello**新增使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="787e4-223">On hello **Add user** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="787e4-224">![新增使用者](./media/active-directory-saas-talentlms-tutorial/IC777299.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="787e4-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="787e4-225">a.</span><span class="sxs-lookup"><span data-stu-id="787e4-225">a.</span></span> <span data-ttu-id="787e4-226">在 hello**名字**文字方塊中，輸入 hello 名字，例如使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="787e4-226">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="787e4-227">b.</span><span class="sxs-lookup"><span data-stu-id="787e4-227">b.</span></span> <span data-ttu-id="787e4-228">在 hello**姓氏**文字方塊中，輸入 hello 姓氏的使用者，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="787e4-228">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="787e4-229">c.</span><span class="sxs-lookup"><span data-stu-id="787e4-229">c.</span></span> <span data-ttu-id="787e4-230">在 hello**電子郵件地址**文字方塊中，輸入 hello 電子郵件的使用者，例如 **brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="787e4-230">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="787e4-231">d.</span><span class="sxs-lookup"><span data-stu-id="787e4-231">d.</span></span> <span data-ttu-id="787e4-232">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="787e4-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="787e4-233">您可以使用任何其他 TalentLMS 使用者帳戶建立工具或 Api 提供 TalentLMS tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="787e4-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="787e4-234">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="787e4-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="787e4-235">在本節中，您可以授與存取 tooTalentLMS 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="787e4-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTalentLMS.</span></span>

![指派使用者][200] 

<span data-ttu-id="787e4-237">**tooassign 許 Simon tooTalentLMS，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="787e4-237">**tooassign Britta Simon tooTalentLMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="787e4-238">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="787e4-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="787e4-240">在 [hello] 應用程式清單中，選取**TalentLMS**。</span><span class="sxs-lookup"><span data-stu-id="787e4-240">In hello applications list, select **TalentLMS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="787e4-242">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="787e4-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="787e4-244">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="787e4-244">Click **Add** button.</span></span> <span data-ttu-id="787e4-245">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="787e4-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="787e4-247">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="787e4-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="787e4-248">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="787e4-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="787e4-249">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="787e4-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="787e4-250">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="787e4-250">Testing single sign-on</span></span>

<span data-ttu-id="787e4-251">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="787e4-251">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="787e4-252">當您按一下的 hello TalentLMS 磚 hello 存取面板中時，您應該取得自動登入 tooyour TalentLMS 的應用程式</span><span class="sxs-lookup"><span data-stu-id="787e4-252">When you click hello TalentLMS tile in hello Access Panel, you should get automatically signed-on tooyour TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="787e4-253">其他資源</span><span class="sxs-lookup"><span data-stu-id="787e4-253">Additional resources</span></span>

* [<span data-ttu-id="787e4-254">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="787e4-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="787e4-255">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="787e4-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

