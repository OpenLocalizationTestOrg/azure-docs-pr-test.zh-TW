---
title: "教學課程：Azure Active Directory 與 Panorama9 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Panorama9 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="01880-103">教學課程：Azure Active Directory 與 Panorama9 整合</span><span class="sxs-lookup"><span data-stu-id="01880-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="01880-104">在此教學課程中，您學會如何與 Azure Active Directory (Azure AD) toointegrate Panorama9。</span><span class="sxs-lookup"><span data-stu-id="01880-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01880-105">與 Azure AD 整合 Panorama9 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="01880-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="01880-106">您可以控制存取 tooPanorama9 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="01880-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="01880-107">您可以啟用您的使用者 tooautomatically get 登入 tooPanorama9 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="01880-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01880-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="01880-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="01880-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="01880-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01880-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="01880-110">Prerequisites</span></span>

<span data-ttu-id="01880-111">tooconfigure 與 Panorama9 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="01880-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="01880-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="01880-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01880-113">啟用 Panorama9 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="01880-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="01880-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="01880-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="01880-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="01880-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01880-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="01880-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="01880-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="01880-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01880-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="01880-118">Scenario description</span></span>
<span data-ttu-id="01880-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="01880-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="01880-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="01880-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01880-121">從 hello 圖庫加入 Panorama9</span><span class="sxs-lookup"><span data-stu-id="01880-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="01880-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="01880-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="01880-123">從 hello 圖庫加入 Panorama9</span><span class="sxs-lookup"><span data-stu-id="01880-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="01880-124">tooconfigure hello 整合 Panorama9 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Panorama9。</span><span class="sxs-lookup"><span data-stu-id="01880-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="01880-125">**tooadd Panorama9 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="01880-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="01880-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="01880-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="01880-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="01880-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="01880-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="01880-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="01880-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="01880-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="01880-133">在 [hello] 搜尋方塊中，輸入**Panorama9**。</span><span class="sxs-lookup"><span data-stu-id="01880-133">In hello search box, type **Panorama9**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="01880-135">在 hello 結果 窗格中，選取  **Panorama9**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01880-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01880-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="01880-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="01880-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Panorama9 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="01880-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="01880-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Panorama9 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="01880-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="01880-140">換句話說，Azure AD 使用者與 hello Panorama9 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="01880-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="01880-141">在 Panorama9 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="01880-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="01880-142">tooconfigure 及測試 Azure AD 單一登入 Panorama9，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="01880-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="01880-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="01880-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="01880-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="01880-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="01880-145">**[建立測試使用者 Panorama9](#creating-a-panorama9-test-user)**  -toohave 許 Simon Panorama9 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="01880-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="01880-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="01880-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="01880-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="01880-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01880-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="01880-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="01880-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Panorama9 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="01880-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="01880-150">**tooconfigure Azure AD 單一登入 Panorama9，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="01880-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="01880-151">在 Azure 入口網站上 hello hello **Panorama9**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="01880-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="01880-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="01880-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="01880-155">在 hello **Panorama9 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="01880-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="01880-157">a.</span><span class="sxs-lookup"><span data-stu-id="01880-157">a.</span></span> <span data-ttu-id="01880-158">在 hello**登入 URL**文字方塊中，輸入與 URL:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="01880-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="01880-159">b.</span><span class="sxs-lookup"><span data-stu-id="01880-159">b.</span></span> <span data-ttu-id="01880-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="01880-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="01880-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="01880-161">These values are not real.</span></span> <span data-ttu-id="01880-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="01880-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="01880-163">請連絡[Panorama9 用戶端支援小組](https://support.panorama9.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="01880-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="01880-164">在 hello **SAML 簽章憑證**區段，複製 hello**指紋**憑證值。</span><span class="sxs-lookup"><span data-stu-id="01880-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="01880-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="01880-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="01880-168">在 hello **Panorama9 設定**區段中，按一下**設定 Panorama9** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="01880-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="01880-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="01880-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="01880-171">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Panorama9 公司網站。</span><span class="sxs-lookup"><span data-stu-id="01880-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="01880-172">在 hello hello 上方的工具列中按一下**管理**，然後按一下**延伸**。</span><span class="sxs-lookup"><span data-stu-id="01880-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="01880-173">![擴充功能](./media/active-directory-saas-panorama9-tutorial/ic790023.png "擴充功能")</span><span class="sxs-lookup"><span data-stu-id="01880-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="01880-174">在 [hello**延伸**] 對話方塊中，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="01880-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="01880-175">![單一登入](./media/active-directory-saas-panorama9-tutorial/ic790024.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="01880-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="01880-176">在 hello**設定**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="01880-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="01880-177">![設定](./media/active-directory-saas-panorama9-tutorial/ic790025.png "設定")</span><span class="sxs-lookup"><span data-stu-id="01880-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="01880-178">a.</span><span class="sxs-lookup"><span data-stu-id="01880-178">a.</span></span> <span data-ttu-id="01880-179">在**身分識別提供者 URL**文字方塊中，貼上 hello 值**單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="01880-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="01880-180">b.</span><span class="sxs-lookup"><span data-stu-id="01880-180">b.</span></span> <span data-ttu-id="01880-181">在**憑證指紋**文字方塊中，貼上 hello**指紋**憑證，您從 Azure 入口網站複製的值。</span><span class="sxs-lookup"><span data-stu-id="01880-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="01880-182">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="01880-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="01880-183">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="01880-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="01880-184">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="01880-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="01880-185">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="01880-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01880-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="01880-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="01880-187">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="01880-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="01880-189">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="01880-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="01880-190">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="01880-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="01880-192">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="01880-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="01880-194">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="01880-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01880-196">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="01880-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="01880-198">a.</span><span class="sxs-lookup"><span data-stu-id="01880-198">a.</span></span> <span data-ttu-id="01880-199">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="01880-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01880-200">b.</span><span class="sxs-lookup"><span data-stu-id="01880-200">b.</span></span> <span data-ttu-id="01880-201">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="01880-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="01880-202">c.</span><span class="sxs-lookup"><span data-stu-id="01880-202">c.</span></span> <span data-ttu-id="01880-203">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="01880-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="01880-204">d.</span><span class="sxs-lookup"><span data-stu-id="01880-204">d.</span></span> <span data-ttu-id="01880-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="01880-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="01880-206">建立 Panorama9 測試使用者</span><span class="sxs-lookup"><span data-stu-id="01880-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="01880-207">在訂單 tooenable Azure AD 使用者 toolog 入 Panorama9，它們必須佈建到 Panorama9。</span><span class="sxs-lookup"><span data-stu-id="01880-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="01880-208">在 Panorama9 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="01880-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="01880-209">**tooconfigure 使用者佈建，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="01880-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="01880-210">登入 tooyour **Panorama9**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="01880-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="01880-211">在 hello 最上層顯示 hello 功能表上，按一下**管理**，然後按一下**使用者**。</span><span class="sxs-lookup"><span data-stu-id="01880-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="01880-212">![使用者](./media/active-directory-saas-panorama9-tutorial/ic790027.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="01880-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="01880-213">在 hello 使用者 區段中，按一下   **+**  tooadd 新使用者。</span><span class="sxs-lookup"><span data-stu-id="01880-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="01880-214">![使用者](./media/active-directory-saas-panorama9-tutorial/ic790028.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="01880-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="01880-215">移 toohello 使用者資料 區段中，類型 hello 電子郵件地址的有效的 Azure Active Directory 使用者，您想要 tooprovision 到 hello**電子郵件**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="01880-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="01880-216">來自 toohello 使用者 區段中，按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="01880-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="01880-217">hello Azure Active Directory 帳戶持有者會收到一封電子郵件，並且遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="01880-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="01880-218">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="01880-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="01880-219">在本節中，您可以授與存取 tooPanorama9 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="01880-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![指派使用者][200] 

<span data-ttu-id="01880-221">**tooassign 許 Simon tooPanorama9，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="01880-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="01880-222">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="01880-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="01880-224">在 [hello] 應用程式清單中，選取**Panorama9**。</span><span class="sxs-lookup"><span data-stu-id="01880-224">In hello applications list, select **Panorama9**.</span></span>

    ![設定單一登入](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="01880-226">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="01880-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="01880-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="01880-228">Click **Add** button.</span></span> <span data-ttu-id="01880-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="01880-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="01880-231">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="01880-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="01880-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="01880-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="01880-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="01880-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="01880-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="01880-234">Testing single sign-on</span></span>

<span data-ttu-id="01880-235">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="01880-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="01880-236">當您按一下 hello 存取面板中的 hello Panorama9 磚時，您應該取得自動登入 tooPanorama9 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01880-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="01880-237">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="01880-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="01880-238">其他資源</span><span class="sxs-lookup"><span data-stu-id="01880-238">Additional resources</span></span>

* [<span data-ttu-id="01880-239">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01880-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01880-240">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="01880-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

