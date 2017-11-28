---
title: "教學課程：Azure Active Directory 與 HackerOne 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Hackerone 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: c9dc033e26e79a7233dcfb3899c62684d4a19652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="204dd-103">教學課程：Azure Active Directory 與 HackerOne 整合</span><span class="sxs-lookup"><span data-stu-id="204dd-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="204dd-104">在此教學課程中，您學會如何 toointegrate HackerOne 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="204dd-104">In this tutorial, you learn how toointegrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="204dd-105">與 Azure AD 整合 HackerOne 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="204dd-105">Integrating HackerOne with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="204dd-106">您可以控制存取 tooHackerOne Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="204dd-106">You can control in Azure AD who has access tooHackerOne</span></span>
- <span data-ttu-id="204dd-107">您可以啟用您的使用者 tooautomatically get 登入 tooHackerOne （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="204dd-107">You can enable your users tooautomatically get signed-on tooHackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="204dd-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="204dd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="204dd-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="204dd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="204dd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="204dd-110">Prerequisites</span></span>

<span data-ttu-id="204dd-111">tooconfigure HackerOne 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="204dd-111">tooconfigure Azure AD integration with HackerOne, you need hello following items:</span></span>

- <span data-ttu-id="204dd-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="204dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="204dd-113">已啟用 HackerOne 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="204dd-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="204dd-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="204dd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="204dd-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="204dd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="204dd-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="204dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="204dd-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="204dd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="204dd-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="204dd-118">Scenario description</span></span>
<span data-ttu-id="204dd-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="204dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="204dd-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="204dd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="204dd-121">從 hello 圖庫加入 HackerOne</span><span class="sxs-lookup"><span data-stu-id="204dd-121">Adding HackerOne from hello gallery</span></span>
2. <span data-ttu-id="204dd-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="204dd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-hello-gallery"></a><span data-ttu-id="204dd-123">從 hello 圖庫加入 HackerOne</span><span class="sxs-lookup"><span data-stu-id="204dd-123">Adding HackerOne from hello gallery</span></span>
<span data-ttu-id="204dd-124">tooconfigure hello 整合 HackerOne 到 Azure AD，您需要 tooadd HackerOne hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="204dd-124">tooconfigure hello integration of HackerOne into Azure AD, you need tooadd HackerOne from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="204dd-125">**tooadd HackerOne 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="204dd-125">**tooadd HackerOne from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="204dd-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="204dd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="204dd-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="204dd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="204dd-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="204dd-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="204dd-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="204dd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="204dd-133">在 [hello] 搜尋方塊中，輸入**HackerOne**。</span><span class="sxs-lookup"><span data-stu-id="204dd-133">In hello search box, type **HackerOne**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="204dd-135">在 hello 結果 窗格中，選取  **HackerOne**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="204dd-135">In hello results panel, select **HackerOne**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="204dd-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="204dd-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="204dd-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 HackerOne 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="204dd-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="204dd-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 HackerOne 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="204dd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HackerOne is tooa user in Azure AD.</span></span> <span data-ttu-id="204dd-140">換句話說，Azure AD 使用者與 hello HackerOne 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="204dd-140">In other words, a link relationship between an Azure AD user and hello related user in HackerOne needs toobe established.</span></span>

<span data-ttu-id="204dd-141">HackerOne 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="204dd-141">In HackerOne, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="204dd-142">tooconfigure 及 HackerOne 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="204dd-142">tooconfigure and test Azure AD single sign-on with HackerOne, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="204dd-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="204dd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="204dd-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="204dd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="204dd-145">**[建立測試使用者 HackerOne](#creating-a-hackerone-test-user)**  -toohave 許 Simon HackerOne 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="204dd-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - toohave a counterpart of Britta Simon in HackerOne that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="204dd-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="204dd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="204dd-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="204dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="204dd-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="204dd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="204dd-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 HackerOne 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="204dd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="204dd-150">**tooconfigure Azure AD 單一登入與 HackerOne，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="204dd-150">**tooconfigure Azure AD single sign-on with HackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="204dd-151">在 Azure 入口網站上 hello hello **HackerOne**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="204dd-151">In hello Azure portal, on hello **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="204dd-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="204dd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="204dd-155">在 hello **HackerOne 單一登入 URL 和識別碼**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="204dd-155">On hello **HackerOne Single sign-on URL and Identifier** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="204dd-157">a.</span><span class="sxs-lookup"><span data-stu-id="204dd-157">a.</span></span> <span data-ttu-id="204dd-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="204dd-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="204dd-159">b.</span><span class="sxs-lookup"><span data-stu-id="204dd-159">b.</span></span> <span data-ttu-id="204dd-160">在 hello**識別碼**文字方塊中，輸入 URL:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="204dd-160">In hello **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="204dd-161">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="204dd-161">This value is not real.</span></span> <span data-ttu-id="204dd-162">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="204dd-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="204dd-163">請連絡[HackerOne 支援小組](mailto:support@hackerone.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="204dd-163">Contact [HackerOne support team](mailto:support@hackerone.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="204dd-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="204dd-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="204dd-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="204dd-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="204dd-168">在 hello **HackerOne 組態**區段中，按一下**設定 HackerOne** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="204dd-168">On hello **HackerOne Configuration** section, click **Configure HackerOne** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="204dd-169">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="204dd-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="204dd-171">登入 tooyour HackerOne 租用戶系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="204dd-171">Sign On tooyour HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="204dd-172">在 hello 最上層顯示 hello 功能表上，按一下 hello"**設定**。 」</span><span class="sxs-lookup"><span data-stu-id="204dd-172">In hello menu on hello top, click hello "**Settings**."</span></span>
   
    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="204dd-174">瀏覽過"**驗證**"和按一下"**新增 SAML 設定**。 」</span><span class="sxs-lookup"><span data-stu-id="204dd-174">Navigate too"**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="204dd-176">在 [hello **SAML 設定**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="204dd-176">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="204dd-178">a.</span><span class="sxs-lookup"><span data-stu-id="204dd-178">a.</span></span> <span data-ttu-id="204dd-179">在 hello**電子郵件網域**文字方塊中，輸入已註冊的網域。</span><span class="sxs-lookup"><span data-stu-id="204dd-179">In hello **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="204dd-180">b.</span><span class="sxs-lookup"><span data-stu-id="204dd-180">b.</span></span> <span data-ttu-id="204dd-181">在**單一登入 URL**等文字方塊中，貼上的 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="204dd-181">In  **Single Sign On URL** textboxes, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="204dd-182">c.</span><span class="sxs-lookup"><span data-stu-id="204dd-182">c.</span></span> <span data-ttu-id="204dd-183">開啟您**憑證檔案**從 Azure 入口網站下載 [記事本] 中的 hello 內容複製到剪貼簿，並貼 toohello **X509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="204dd-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="204dd-184">d.</span><span class="sxs-lookup"><span data-stu-id="204dd-184">d.</span></span> <span data-ttu-id="204dd-185">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="204dd-185">Click **Save**.</span></span>

11. <span data-ttu-id="204dd-186">在 hello 驗證設定對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="204dd-186">On hello Authentication Settings dialog, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="204dd-188">a.</span><span class="sxs-lookup"><span data-stu-id="204dd-188">a.</span></span> <span data-ttu-id="204dd-189">按一下 [執行測試]。</span><span class="sxs-lookup"><span data-stu-id="204dd-189">Click **Run test**.</span></span>

    <span data-ttu-id="204dd-190">b.</span><span class="sxs-lookup"><span data-stu-id="204dd-190">b.</span></span> <span data-ttu-id="204dd-191">如果 hello 值 hello**狀態**欄位等於**上次測試狀態： 建立**，請連絡您[HackerOne 支援小組](mailto:support@hackerone.com)toorequest 檢閱您的設定。</span><span class="sxs-lookup"><span data-stu-id="204dd-191">If hello value of hello **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) toorequest a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="204dd-192">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="204dd-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="204dd-193">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="204dd-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="204dd-194">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="204dd-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="204dd-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="204dd-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="204dd-196">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="204dd-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="204dd-198">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="204dd-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="204dd-199">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="204dd-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="204dd-201">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="204dd-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="204dd-203">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="204dd-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="204dd-205">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="204dd-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="204dd-207">a.</span><span class="sxs-lookup"><span data-stu-id="204dd-207">a.</span></span> <span data-ttu-id="204dd-208">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="204dd-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="204dd-209">b.</span><span class="sxs-lookup"><span data-stu-id="204dd-209">b.</span></span> <span data-ttu-id="204dd-210">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="204dd-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="204dd-211">c.</span><span class="sxs-lookup"><span data-stu-id="204dd-211">c.</span></span> <span data-ttu-id="204dd-212">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="204dd-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="204dd-213">d.</span><span class="sxs-lookup"><span data-stu-id="204dd-213">d.</span></span> <span data-ttu-id="204dd-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="204dd-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="204dd-215">建立 HackerOne 測試使用者</span><span class="sxs-lookup"><span data-stu-id="204dd-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="204dd-216">接下來，您要在 HackerOne 建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="204dd-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="204dd-217">HackerOne 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="204dd-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="204dd-218">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="204dd-218">There is no action item for you in this section.</span></span> <span data-ttu-id="204dd-219">當您存取 HackerOne 時，如果還沒有新的使用者，就會建立一個。</span><span class="sxs-lookup"><span data-stu-id="204dd-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="204dd-220">若要手動 toocreate 使用者，您會需要 toocontact hello Certify 支援小組。</span><span class="sxs-lookup"><span data-stu-id="204dd-220">If you need toocreate a user manually, you need toocontact hello Certify support team.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="204dd-221">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="204dd-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="204dd-222">在本節中，您可以授與存取 tooHackerOne 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="204dd-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHackerOne.</span></span>

![指派使用者][200] 

<span data-ttu-id="204dd-224">**tooassign 許 Simon tooHackerOne，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="204dd-224">**tooassign Britta Simon tooHackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="204dd-225">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="204dd-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="204dd-227">在 [hello] 應用程式清單中，選取**HackerOne**。</span><span class="sxs-lookup"><span data-stu-id="204dd-227">In hello applications list, select **HackerOne**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="204dd-229">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="204dd-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="204dd-231">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="204dd-231">Click **Add** button.</span></span> <span data-ttu-id="204dd-232">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="204dd-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="204dd-234">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="204dd-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="204dd-235">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="204dd-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="204dd-236">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="204dd-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="204dd-237">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="204dd-237">Testing single sign-on</span></span>

<span data-ttu-id="204dd-238">最後，您會測試 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="204dd-238">Finally, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="204dd-239">當您按一下 hello HackerOne 磚 hello 存取面板中的時，您應該取得自動登入 tooyour HackerOne 應用程式。</span><span class="sxs-lookup"><span data-stu-id="204dd-239">When you click hello HackerOne tile in hello Access Panel, you should get automatically signed-on tooyour HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="204dd-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="204dd-240">Additional resources</span></span>

* [<span data-ttu-id="204dd-241">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="204dd-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="204dd-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="204dd-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

