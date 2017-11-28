---
title: "教學課程：Azure Active Directory 與 SkyDesk Email 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 之間 SkyDesk 電子郵件。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="e4872-103">教學課程：Azure Active Directory 與 SkyDesk Email 整合</span><span class="sxs-lookup"><span data-stu-id="e4872-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="e4872-104">在此教學課程中，您學會如何 toointegrate SkyDesk 電子郵件與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e4872-104">In this tutorial, you learn how toointegrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e4872-105">與 Azure AD 整合 SkyDesk 電子郵件可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="e4872-105">Integrating SkyDesk Email with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e4872-106">您可以控制存取 tooSkyDesk 電子郵件的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="e4872-106">You can control in Azure AD who has access tooSkyDesk Email</span></span>
- <span data-ttu-id="e4872-107">您可以啟用您的使用者 tooautomatically get 登入 tooSkyDesk （單一登入） 的電子郵件與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="e4872-107">You can enable your users tooautomatically get signed-on tooSkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e4872-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e4872-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e4872-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e4872-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4872-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e4872-110">Prerequisites</span></span>

<span data-ttu-id="e4872-111">tooconfigure SkyDesk 電子郵件與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="e4872-111">tooconfigure Azure AD integration with SkyDesk Email, you need hello following items:</span></span>

- <span data-ttu-id="e4872-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e4872-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e4872-113">已啟用 Skydesk Email 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e4872-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e4872-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="e4872-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e4872-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e4872-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e4872-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e4872-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e4872-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e4872-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e4872-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e4872-118">Scenario description</span></span>
<span data-ttu-id="e4872-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e4872-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e4872-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e4872-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e4872-121">從 hello 組件庫新增 SkyDesk 電子郵件</span><span class="sxs-lookup"><span data-stu-id="e4872-121">Adding SkyDesk Email from hello gallery</span></span>
2. <span data-ttu-id="e4872-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e4872-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-hello-gallery"></a><span data-ttu-id="e4872-123">從 hello 組件庫新增 SkyDesk 電子郵件</span><span class="sxs-lookup"><span data-stu-id="e4872-123">Adding SkyDesk Email from hello gallery</span></span>
<span data-ttu-id="e4872-124">tooconfigure hello 整合 SkyDesk 電子郵件到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SkyDesk 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e4872-124">tooconfigure hello integration of SkyDesk Email into Azure AD, you need tooadd SkyDesk Email from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e4872-125">**tooadd SkyDesk hello 圖庫中的電子郵件執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e4872-125">**tooadd SkyDesk Email from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4872-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e4872-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e4872-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e4872-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e4872-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e4872-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e4872-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4872-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e4872-133">在 [hello] 搜尋方塊中，輸入**SkyDesk 電子郵件**。</span><span class="sxs-lookup"><span data-stu-id="e4872-133">In hello search box, type **SkyDesk Email**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="e4872-135">在 hello 結果 窗格中，選取  **SkyDesk 電子郵件**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4872-135">In hello results panel, select **SkyDesk Email**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e4872-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e4872-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e4872-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SkyDesk Email 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e4872-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e4872-139">單一登入 toowork，Azure AD 需要 tooknow SkyDesk 電子郵件中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="e4872-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SkyDesk Email is tooa user in Azure AD.</span></span> <span data-ttu-id="e4872-140">換句話說，Azure AD 使用者與 hello SkyDesk 電子郵件中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="e4872-140">In other words, a link relationship between an Azure AD user and hello related user in SkyDesk Email needs toobe established.</span></span>

<span data-ttu-id="e4872-141">在 SkyDesk 電子郵件，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e4872-141">In SkyDesk Email, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e4872-142">tooconfigure 及測試 Azure AD 單一登入與 SkyDesk 電子郵件，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="e4872-142">tooconfigure and test Azure AD single sign-on with SkyDesk Email, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e4872-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="e4872-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e4872-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="e4872-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e4872-145">**[建立 SkyDesk 電子郵件以測試使用者](#creating-a-skydesk-email-test-user)** -toohave 許 Simon SkyDesk 是表示連結的 toohello Azure AD 使用者的電子郵件中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="e4872-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - toohave a counterpart of Britta Simon in SkyDesk Email that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e4872-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e4872-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e4872-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="e4872-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e4872-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e4872-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e4872-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 SkyDesk 電子郵件應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e4872-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="e4872-150">**tooconfigure Azure AD 單一登入具有 SkyDesk 電子郵件中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e4872-150">**tooconfigure Azure AD single sign-on with SkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4872-151">在 Azure 入口網站上 hello hello **SkyDesk 電子郵件**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="e4872-151">In hello Azure portal, on hello **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e4872-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e4872-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="e4872-155">在 hello **SkyDesk 電子郵件網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4872-155">On hello **SkyDesk Email Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="e4872-157">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="e4872-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e4872-158">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="e4872-158">hello value is not real.</span></span> <span data-ttu-id="e4872-159">更新 hello 值與 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="e4872-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="e4872-160">請連絡[SkyDesk 電子郵件用戶端支援小組](https://www.skydesk.sg/support/)tooget hello 值。</span><span class="sxs-lookup"><span data-stu-id="e4872-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="e4872-161">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="e4872-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="e4872-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4872-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e4872-165">在 hello **SkyDesk 電子郵件設定**區段中，按一下**設定 SkyDesk 電子郵件**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="e4872-165">On hello **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e4872-166">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="e4872-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="e4872-168">tooenable SSO 中**SkyDesk 電子郵件**，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4872-168">tooenable SSO in **SkyDesk Email**, perform hello following steps:</span></span>

    <span data-ttu-id="e4872-169">a.</span><span class="sxs-lookup"><span data-stu-id="e4872-169">a.</span></span> <span data-ttu-id="e4872-170">登入 tooyour SkyDesk 電子郵件帳戶，以系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="e4872-170">Sign-on tooyour SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="e4872-171">b.</span><span class="sxs-lookup"><span data-stu-id="e4872-171">b.</span></span> <span data-ttu-id="e4872-172">在 hello 最上層顯示 hello 功能表上，按一下**安裝**，然後選取**組織**。</span><span class="sxs-lookup"><span data-stu-id="e4872-172">In hello menu on hello top, click **Setup**, and select **Org**.</span></span> 
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="e4872-174">c.</span><span class="sxs-lookup"><span data-stu-id="e4872-174">c.</span></span> <span data-ttu-id="e4872-175">按一下**網域**hello 左面板中。</span><span class="sxs-lookup"><span data-stu-id="e4872-175">Click on **Domains** from hello left panel.</span></span>
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="e4872-177">d.</span><span class="sxs-lookup"><span data-stu-id="e4872-177">d.</span></span> <span data-ttu-id="e4872-178">按一下 [加入網域]。</span><span class="sxs-lookup"><span data-stu-id="e4872-178">Click on **Add Domain**.</span></span>
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="e4872-180">e.</span><span class="sxs-lookup"><span data-stu-id="e4872-180">e.</span></span> <span data-ttu-id="e4872-181">輸入您的網域名稱，然後確認 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="e4872-181">Enter your Domain name, and then verify hello Domain.</span></span>
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="e4872-183">f.</span><span class="sxs-lookup"><span data-stu-id="e4872-183">f.</span></span> <span data-ttu-id="e4872-184">按一下**SAML 驗證**hello 左面板中。</span><span class="sxs-lookup"><span data-stu-id="e4872-184">Click on **SAML Authentication** from hello left panel.</span></span>
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="e4872-186">在 hello **SAML 驗證**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4872-186">On hello **SAML Authentication** dialog page, perform hello following steps:</span></span>
   
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="e4872-188">toouse SAML 型驗證，您應該會**驗證網域**或**入口網站 URL**安裝程式。</span><span class="sxs-lookup"><span data-stu-id="e4872-188">toouse SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="e4872-189">您可以設定 hello 入口網站 URL 與 hello 唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="e4872-189">You can set hello portal URL with hello unique name.</span></span>
    > 
    > 
   
    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="e4872-191">a.</span><span class="sxs-lookup"><span data-stu-id="e4872-191">a.</span></span> <span data-ttu-id="e4872-192">在 hello**登入 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="e4872-192">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e4872-193">b.</span><span class="sxs-lookup"><span data-stu-id="e4872-193">b.</span></span> <span data-ttu-id="e4872-194">在 [hello**登出**URL] 文字方塊中，貼上 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="e4872-194">In hello **Logout** URL textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e4872-195">c.</span><span class="sxs-lookup"><span data-stu-id="e4872-195">c.</span></span> <span data-ttu-id="e4872-196">[變更密碼 URL] 是選擇性的，將它保留為空白。</span><span class="sxs-lookup"><span data-stu-id="e4872-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="e4872-197">d.</span><span class="sxs-lookup"><span data-stu-id="e4872-197">d.</span></span> <span data-ttu-id="e4872-198">按一下**從檔案取得金鑰**tooselect 您下載的憑證，從 Azure 入口網站，然後按一下**開啟**tooupload hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="e4872-198">Click on **Get Key From File** tooselect your downloaded certificate from Azure portal, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="e4872-199">e.</span><span class="sxs-lookup"><span data-stu-id="e4872-199">e.</span></span> <span data-ttu-id="e4872-200">選取 [RSA] 做為 [演算法]。</span><span class="sxs-lookup"><span data-stu-id="e4872-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="e4872-201">f.</span><span class="sxs-lookup"><span data-stu-id="e4872-201">f.</span></span> <span data-ttu-id="e4872-202">按一下**確定**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="e4872-202">Click **Ok** toosave hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="e4872-203">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="e4872-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e4872-204">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="e4872-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e4872-205">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e4872-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e4872-206">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e4872-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="e4872-207">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e4872-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e4872-209">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e4872-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4872-210">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="e4872-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e4872-212">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="e4872-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e4872-214">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="e4872-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e4872-216">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e4872-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e4872-218">a.</span><span class="sxs-lookup"><span data-stu-id="e4872-218">a.</span></span> <span data-ttu-id="e4872-219">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e4872-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e4872-220">b.</span><span class="sxs-lookup"><span data-stu-id="e4872-220">b.</span></span> <span data-ttu-id="e4872-221">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="e4872-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e4872-222">c.</span><span class="sxs-lookup"><span data-stu-id="e4872-222">c.</span></span> <span data-ttu-id="e4872-223">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="e4872-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e4872-224">d.</span><span class="sxs-lookup"><span data-stu-id="e4872-224">d.</span></span> <span data-ttu-id="e4872-225">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e4872-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="e4872-226">建立 SkyDesk Email 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e4872-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="e4872-227">在本節中，您要在 SkyDesk Email 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="e4872-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="e4872-228">按一下**使用者存取**從剩餘的 hello 面板 SkyDesk 電子郵件中，然後輸入您的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="e4872-228">Click on **User Access** from hello left panel in SkyDesk Email and then enter your username.</span></span> 

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="e4872-230">如果您需要 toocreate 大量使用者時，您需要 toocontact hello [SkyDesk 電子郵件用戶端支援小組](https://www.skydesk.sg/support/)。</span><span class="sxs-lookup"><span data-stu-id="e4872-230">If you need toocreate bulk users, you need toocontact hello [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e4872-231">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="e4872-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e4872-232">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooSkyDesk 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e4872-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkyDesk Email.</span></span>

![指派使用者][200] 

<span data-ttu-id="e4872-234">**tooassign 許 Simon tooSkyDesk 電子郵件，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="e4872-234">**tooassign Britta Simon tooSkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="e4872-235">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e4872-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e4872-237">在 [hello] 應用程式清單中，選取**SkyDesk 電子郵件**。</span><span class="sxs-lookup"><span data-stu-id="e4872-237">In hello applications list, select **SkyDesk Email**.</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="e4872-239">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="e4872-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e4872-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4872-241">Click **Add** button.</span></span> <span data-ttu-id="e4872-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e4872-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e4872-244">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="e4872-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e4872-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4872-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e4872-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4872-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e4872-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e4872-247">Testing single sign-on</span></span>

<span data-ttu-id="e4872-248">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="e4872-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="e4872-249">當您按一下的 hello SkyDesk 電子郵件磚 hello 存取面板中時，您應該取得自動登入 tooyour SkyDesk 電子郵件應用程式。</span><span class="sxs-lookup"><span data-stu-id="e4872-249">When you click hello SkyDesk Email tile in hello Access Panel, you should get automatically signed-on tooyour SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e4872-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="e4872-250">Additional resources</span></span>

* [<span data-ttu-id="e4872-251">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4872-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e4872-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e4872-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

