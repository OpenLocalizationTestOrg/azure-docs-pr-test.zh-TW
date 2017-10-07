---
title: "教學課程：Azure Active Directory 與 AppDynamics 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 AppDynamics 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9b63afec73d7442e6ac1ce34b511beea6f43ffe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="8a8c0-103">教學課程：Azure Active Directory 與 AppDynamics 整合</span><span class="sxs-lookup"><span data-stu-id="8a8c0-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="8a8c0-104">在此教學課程中，您學會如何 toointegrate AppDynamics 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-104">In this tutorial, you learn how toointegrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a8c0-105">與 Azure AD 整合 AppDynamics 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="8a8c0-105">Integrating AppDynamics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8a8c0-106">您可以控制存取 tooAppDynamics Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="8a8c0-106">You can control in Azure AD who has access tooAppDynamics</span></span>
- <span data-ttu-id="8a8c0-107">您可以啟用您的使用者 tooautomatically get 登入 tooAppDynamics （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="8a8c0-107">You can enable your users tooautomatically get signed-on tooAppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a8c0-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8a8c0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8a8c0-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a8c0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8a8c0-110">Prerequisites</span></span>

<span data-ttu-id="8a8c0-111">tooconfigure 與 AppDynamics 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="8a8c0-111">tooconfigure Azure AD integration with AppDynamics, you need hello following items:</span></span>

- <span data-ttu-id="8a8c0-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8a8c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a8c0-113">已啟用 AppDynamics 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8a8c0-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a8c0-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a8c0-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8a8c0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a8c0-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a8c0-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a8c0-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8a8c0-118">Scenario description</span></span>
<span data-ttu-id="8a8c0-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a8c0-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8a8c0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a8c0-121">從 hello 圖庫加入 AppDynamics</span><span class="sxs-lookup"><span data-stu-id="8a8c0-121">Adding AppDynamics from hello gallery</span></span>
2. <span data-ttu-id="8a8c0-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8a8c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-hello-gallery"></a><span data-ttu-id="8a8c0-123">從 hello 圖庫加入 AppDynamics</span><span class="sxs-lookup"><span data-stu-id="8a8c0-123">Adding AppDynamics from hello gallery</span></span>
<span data-ttu-id="8a8c0-124">tooconfigure hello 整合 AppDynamics 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd AppDynamics。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-124">tooconfigure hello integration of AppDynamics into Azure AD, you need tooadd AppDynamics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8a8c0-125">**tooadd AppDynamics 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8a8c0-125">**tooadd AppDynamics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a8c0-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a8c0-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8a8c0-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8a8c0-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8a8c0-133">在 [hello] 搜尋方塊中，輸入**AppDynamics**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-133">In hello search box, type **AppDynamics**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="8a8c0-135">在 hello 結果 窗格中，選取  **AppDynamics**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-135">In hello results panel, select **AppDynamics**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a8c0-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8a8c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a8c0-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 AppDynamics 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8a8c0-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 AppDynamics 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppDynamics is tooa user in Azure AD.</span></span> <span data-ttu-id="8a8c0-140">換句話說，Azure AD 使用者與 hello AppDynamics 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-140">In other words, a link relationship between an Azure AD user and hello related user in AppDynamics needs toobe established.</span></span>

<span data-ttu-id="8a8c0-141">在 AppDynamics 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-141">In AppDynamics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8a8c0-142">tooconfigure 及測試 Azure AD 單一登入 AppDynamics，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="8a8c0-142">tooconfigure and test Azure AD single sign-on with AppDynamics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8a8c0-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8a8c0-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a8c0-145">**[建立測試使用者 AppDynamics](#creating-an-appdynamics-test-user)**  -toohave 許 Simon AppDynamics 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - toohave a counterpart of Britta Simon in AppDynamics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a8c0-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a8c0-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a8c0-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8a8c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a8c0-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 AppDynamics 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="8a8c0-150">**tooconfigure Azure AD 單一登入 AppDynamics，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8a8c0-150">**tooconfigure Azure AD single sign-on with AppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a8c0-151">在 Azure 入口網站上 hello hello **AppDynamics**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-151">In hello Azure portal, on hello **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8a8c0-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="8a8c0-155">在 hello **AppDynamics 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8a8c0-155">On hello **AppDynamics Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="8a8c0-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-157">a.</span></span> <span data-ttu-id="8a8c0-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="8a8c0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="8a8c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-159">b.</span></span> <span data-ttu-id="8a8c0-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="8a8c0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a8c0-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-161">These values are not real.</span></span> <span data-ttu-id="8a8c0-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8a8c0-163">請連絡[AppDynamics 用戶端支援小組](https://www.appdynamics.com/support/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="8a8c0-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="8a8c0-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8a8c0-168">在 hello **AppDynamics 組態**區段中，按一下**設定 AppDynamics** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-168">On hello **AppDynamics Configuration** section, click **Configure AppDynamics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8a8c0-169">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="8a8c0-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="8a8c0-171">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour AppDynamics 公司網站。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-171">In a different web browser window, log in tooyour AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="8a8c0-172">在 hello hello 上方的工具列中按一下**設定**，然後按一下**管理**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-172">In hello toolbar on hello top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="8a8c0-173">![管理](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "管理")</span><span class="sxs-lookup"><span data-stu-id="8a8c0-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="8a8c0-174">按一下 hello**驗證提供者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-174">Click hello **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="8a8c0-175">![驗證提供者](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "驗證提供者")</span><span class="sxs-lookup"><span data-stu-id="8a8c0-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="8a8c0-176">在 hello**驗證提供者**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8a8c0-176">In hello **Authentication Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8a8c0-177">![SAML 設定](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="8a8c0-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="8a8c0-178">a.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-178">a.</span></span> <span data-ttu-id="8a8c0-179">針對 [驗證提供者]，選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="8a8c0-180">b.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-180">b.</span></span> <span data-ttu-id="8a8c0-181">在 hello**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-181">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8a8c0-182">c.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-182">c.</span></span> <span data-ttu-id="8a8c0-183">在 hello**登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-183">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="8a8c0-184">d.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-184">d.</span></span> <span data-ttu-id="8a8c0-185">在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後將它貼入 toohello**憑證**文字方塊</span><span class="sxs-lookup"><span data-stu-id="8a8c0-185">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox</span></span>

    <span data-ttu-id="8a8c0-186">e.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-186">e.</span></span> <span data-ttu-id="8a8c0-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-187">Click **Save**.</span></span>

     <span data-ttu-id="8a8c0-188">![儲存](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "儲存")</span><span class="sxs-lookup"><span data-stu-id="8a8c0-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="8a8c0-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="8a8c0-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8a8c0-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8a8c0-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a8c0-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a8c0-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8a8c0-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a8c0-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8a8c0-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8a8c0-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a8c0-196">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a8c0-198">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a8c0-200">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a8c0-202">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8a8c0-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a8c0-204">a.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-204">a.</span></span> <span data-ttu-id="8a8c0-205">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a8c0-206">b.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-206">b.</span></span> <span data-ttu-id="8a8c0-207">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a8c0-208">c.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-208">c.</span></span> <span data-ttu-id="8a8c0-209">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8a8c0-210">d.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-210">d.</span></span> <span data-ttu-id="8a8c0-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="8a8c0-212">建立 AppDynamics 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8a8c0-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="8a8c0-213">tooenable Azure AD 使用者 toolog 中 tooAppDynamics，它們必須佈建到 AppDynamics。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-213">tooenable Azure AD users toolog in tooAppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="8a8c0-214">在 AppDynamics 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-214">In hello case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="8a8c0-215">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8a8c0-215">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a8c0-216">登入 tooyour AppDynamics 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-216">Log in tooyour AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="8a8c0-217">跳過**使用者**，然後按一下  **+**  tooopen hello **Create User**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-217">Go too**Users**, and then click **+** tooopen hello **Create User** dialog.</span></span>
   
    <span data-ttu-id="8a8c0-218">![使用者](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="8a8c0-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="8a8c0-219">在 hello **Create User**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8a8c0-219">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8a8c0-220">![建立使用者](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="8a8c0-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="8a8c0-221">a.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-221">a.</span></span> <span data-ttu-id="8a8c0-222">型別 hello **Username**，**名稱**，**電子郵件**，**新密碼**，**重覆新密碼**的有效 AAD想成 hello tooprovision 帳戶相關的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-222">Type hello **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="8a8c0-223">b.</span><span class="sxs-lookup"><span data-stu-id="8a8c0-223">b.</span></span> <span data-ttu-id="8a8c0-224">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8a8c0-225">您可以使用任何其他 AppDynamics 使用者帳戶建立工具或 Api 提供 AppDynamics tooprovision Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8a8c0-226">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="8a8c0-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8a8c0-227">在本節中，您可以授與存取 tooAppDynamics 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppDynamics.</span></span>

![指派使用者][200] 

<span data-ttu-id="8a8c0-229">**tooassign 許 Simon tooAppDynamics，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8a8c0-229">**tooassign Britta Simon tooAppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="8a8c0-230">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8a8c0-232">在 [hello] 應用程式清單中，選取**AppDynamics**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-232">In hello applications list, select **AppDynamics**.</span></span>

    ![設定單一登入](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="8a8c0-234">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8a8c0-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-236">Click **Add** button.</span></span> <span data-ttu-id="8a8c0-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8a8c0-239">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8a8c0-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a8c0-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a8c0-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8a8c0-242">Testing single sign-on</span></span>

<span data-ttu-id="8a8c0-243">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8a8c0-244">當您按一下的 hello AppDynamics 磚 hello 存取面板中時，您應該取得自動登入 tooyour AppDynamics 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8a8c0-244">When you click hello AppDynamics tile in hello Access Panel, you should get automatically signed-on tooyour AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a8c0-245">其他資源</span><span class="sxs-lookup"><span data-stu-id="8a8c0-245">Additional resources</span></span>

* [<span data-ttu-id="8a8c0-246">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a8c0-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a8c0-247">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8a8c0-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

