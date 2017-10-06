---
title: "教學課程：Azure Active Directory 與 Google Apps 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Google 應用程式之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="1ce51-103">教學課程：Azure Active Directory 與 Google Apps 整合</span><span class="sxs-lookup"><span data-stu-id="1ce51-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="1ce51-104">在此教學課程中，您學會如何 toointegrate Google 應用程式與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1ce51-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ce51-105">整合 Azure AD 與 Google Apps 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1ce51-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1ce51-106">您可以控制存取 tooGoogle 應用程式的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="1ce51-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="1ce51-107">您可以啟用您的使用者 tooautomatically get 登入 tooGoogle （單一登入） 的應用程式使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="1ce51-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ce51-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1ce51-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1ce51-109">如果您想 tooknow 與 Azure AD SaaS 應用程式整合的詳細資訊，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1ce51-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ce51-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1ce51-110">Prerequisites</span></span>

<span data-ttu-id="1ce51-111">tooconfigure Azure AD 與 Google Apps 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1ce51-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="1ce51-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1ce51-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ce51-113">啟用 Google Apps 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1ce51-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ce51-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1ce51-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ce51-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1ce51-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ce51-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1ce51-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ce51-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1ce51-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="1ce51-118">影片教學課程</span><span class="sxs-lookup"><span data-stu-id="1ce51-118">Video tutorial</span></span>
<span data-ttu-id="1ce51-119">如何 tooEnable 單一登入 tooGoogle 在 2 分鐘內的應用程式：</span><span class="sxs-lookup"><span data-stu-id="1ce51-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="1ce51-120">常見問題集</span><span class="sxs-lookup"><span data-stu-id="1ce51-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="1ce51-121">**問：Chromebook 及其他 Chrome 裝置是否與 Azure AD 單一登入相容？**</span><span class="sxs-lookup"><span data-stu-id="1ce51-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="1ce51-122">答: [是]，使用者將無法使用其 Azure AD 認證其 Chromebook 裝置到 toosign。</span><span class="sxs-lookup"><span data-stu-id="1ce51-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="1ce51-123">若要了解為何使用者可能收到兩次提供認證的提示，請參閱此 [Google Apps 支援文章](https://support.google.com/chrome/a/answer/6060880) 。</span><span class="sxs-lookup"><span data-stu-id="1ce51-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="1ce51-124">**問： 如果我啟用單一登入，將使用者要能夠 toouse 到任何 Google 產品，例如 Google 教室、 GMail、 google 雲端硬碟、 YouTube，等其 Azure AD 認證 toosign 嗎？**</span><span class="sxs-lookup"><span data-stu-id="1ce51-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="1ce51-125">答: [是]，取決於[的 Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583)您選擇 tooenable 或為您的組織停用。</span><span class="sxs-lookup"><span data-stu-id="1ce51-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="1ce51-126">**問：我是否可以只為一部分 Google Apps 使用者啟用單一登入？**</span><span class="sxs-lookup"><span data-stu-id="1ce51-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="1ce51-127">答： 否，立即開啟在 [單一登入需要所有您 Google Apps 使用者 tooauthenticate 使用他們的 Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="1ce51-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="1ce51-128">Google Apps 不支援多重身分識別提供者，因為您的 Google Apps 環境的 hello 身分識別提供者可以是 Azure AD 或 Google-但不是能同時執行 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="1ce51-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="1ce51-129">**問： 如果使用者透過 Windows 登入，會自動驗證 tooGoogle 應用程式而不取得提示輸入密碼嗎？**</span><span class="sxs-lookup"><span data-stu-id="1ce51-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="1ce51-130">答：有兩個選項可允許這樣的情況。</span><span class="sxs-lookup"><span data-stu-id="1ce51-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="1ce51-131">第一個是，使用者可以透過 [Azure Active Directory Join](active-directory-azureadjoin-overview.md)登入 Windows 10 裝置。</span><span class="sxs-lookup"><span data-stu-id="1ce51-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="1ce51-132">或者，使用者無法登入加入網域的 tooan 內部單一登入 tooAzure AD 透過已啟用的 Active Directory 的 Windows 裝置[Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md)部署。</span><span class="sxs-lookup"><span data-stu-id="1ce51-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="1ce51-133">這兩個選項需要您遵循教學課程 tooenable 單一登入 Azure AD 之間的 hello tooperform hello 步驟和 Google Apps。</span><span class="sxs-lookup"><span data-stu-id="1ce51-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ce51-134">案例描述</span><span class="sxs-lookup"><span data-stu-id="1ce51-134">Scenario description</span></span>
<span data-ttu-id="1ce51-135">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ce51-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ce51-136">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1ce51-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ce51-137">從 hello 圖庫加入 Google Apps</span><span class="sxs-lookup"><span data-stu-id="1ce51-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="1ce51-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1ce51-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="1ce51-139">從 hello 圖庫加入 Google Apps</span><span class="sxs-lookup"><span data-stu-id="1ce51-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="1ce51-140">tooconfigure hello 整合 Google 應用程式到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Google Apps。</span><span class="sxs-lookup"><span data-stu-id="1ce51-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1ce51-141">**tooadd Google Apps hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1ce51-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ce51-142">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1ce51-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1ce51-144">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1ce51-145">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-145">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1ce51-147">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ce51-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1ce51-149">在 [hello] 搜尋方塊中，輸入**Google Apps**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-149">In hello search box, type **Google Apps**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="1ce51-151">在 [hello [結果] 窗格中，選取 [ **Google Apps**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1ce51-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ce51-153">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1ce51-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1ce51-154">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Google Apps 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ce51-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1ce51-155">單一登入 toowork，Azure AD 需要 tooknow Google Apps 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1ce51-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="1ce51-156">換句話說，Azure AD 使用者與 Google Apps 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1ce51-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="1ce51-157">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Google Apps 中。</span><span class="sxs-lookup"><span data-stu-id="1ce51-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="1ce51-158">tooconfigure 及 Azure AD 單一登入與 Google Apps 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1ce51-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1ce51-159">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1ce51-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1ce51-160">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1ce51-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ce51-161">**[建立 Google Apps 的測試使用者](#creating-a-google-apps-test-user)** -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示法的 Google Apps 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="1ce51-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ce51-162">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ce51-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ce51-163">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1ce51-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ce51-164">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1ce51-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ce51-165">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Google Apps 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1ce51-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="1ce51-166">**tooconfigure Azure AD 單一登入與 Google Apps，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1ce51-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ce51-167">在 Azure 入口網站上 hello hello **Google Apps**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1ce51-169">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1ce51-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="1ce51-171">在 [hello **Google Apps 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1ce51-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="1ce51-173">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="1ce51-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1ce51-174">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="1ce51-174">This value is not real.</span></span> <span data-ttu-id="1ce51-175">更新 hello 值與 hello 實際登入 URL。</span><span class="sxs-lookup"><span data-stu-id="1ce51-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="1ce51-176">請連絡 hello [Google 支援小組](https://www.google.com/contact/)。</span><span class="sxs-lookup"><span data-stu-id="1ce51-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="1ce51-177">在 [hello **SAML 簽章憑證**區段中，按一下**憑證**，然後儲存您的電腦上的 [hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="1ce51-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="1ce51-179">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ce51-179">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1ce51-181">在 [hello **Google 應用程式組態**區段中，按一下**設定 Google Apps** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="1ce51-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1ce51-182">複製 hello**登出 URL、 SAML 單一登入服務 URL 和變更密碼 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="1ce51-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="1ce51-184">在您的瀏覽器中開啟新索引標籤，並登入 hello [Google 應用程式系統管理員主控台](http://admin.google.com/)使用您的系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="1ce51-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="1ce51-185">按一下 [安全性] 。</span><span class="sxs-lookup"><span data-stu-id="1ce51-185">Click **Security**.</span></span> <span data-ttu-id="1ce51-186">如果您沒有看到 hello 連結，它可能會隱藏在 hello**其他控制項**功能表底部 hello 囉 」 畫面。</span><span class="sxs-lookup"><span data-stu-id="1ce51-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![按一下 [安全性]。][10]

9. <span data-ttu-id="1ce51-188">在 [hello**安全性**頁面上，按一下**設定單一登入 (SSO)。**</span><span class="sxs-lookup"><span data-stu-id="1ce51-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![按一下 [SSO]。][11]

10. <span data-ttu-id="1ce51-190">執行下列組態變更的 hello:</span><span class="sxs-lookup"><span data-stu-id="1ce51-190">Perform hello following configuration changes:</span></span>
   
    ![設定 SSO][12]
   
    <span data-ttu-id="1ce51-192">a.</span><span class="sxs-lookup"><span data-stu-id="1ce51-192">a.</span></span> <span data-ttu-id="1ce51-193">選取 [使用第三方識別提供者來設定 SSO]。</span><span class="sxs-lookup"><span data-stu-id="1ce51-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="1ce51-194">b.</span><span class="sxs-lookup"><span data-stu-id="1ce51-194">b.</span></span> <span data-ttu-id="1ce51-195">在**登入頁面 URL** Google Apps] 欄位中，貼上的 hello 值**單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="1ce51-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1ce51-196">c.</span><span class="sxs-lookup"><span data-stu-id="1ce51-196">c.</span></span> <span data-ttu-id="1ce51-197">在 [hello**登出頁面 URL** Google Apps] 欄位中，貼上的 hello 值**登出 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="1ce51-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1ce51-198">d.</span><span class="sxs-lookup"><span data-stu-id="1ce51-198">d.</span></span> <span data-ttu-id="1ce51-199">在 [hello**變更密碼 URL** Google Apps] 欄位中，貼上的 hello 值**變更密碼 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="1ce51-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="1ce51-200">e.</span><span class="sxs-lookup"><span data-stu-id="1ce51-200">e.</span></span> <span data-ttu-id="1ce51-201">在 Google Apps，hello**驗證憑證**，hello 將憑證上傳您從 Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="1ce51-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="1ce51-202">f.</span><span class="sxs-lookup"><span data-stu-id="1ce51-202">f.</span></span> <span data-ttu-id="1ce51-203">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="1ce51-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="1ce51-204">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1ce51-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1ce51-205">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1ce51-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1ce51-206">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ce51-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ce51-207">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1ce51-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="1ce51-208">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1ce51-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1ce51-210">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1ce51-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ce51-211">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1ce51-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ce51-213">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ce51-215">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="1ce51-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ce51-217">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1ce51-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ce51-219">a.</span><span class="sxs-lookup"><span data-stu-id="1ce51-219">a.</span></span> <span data-ttu-id="1ce51-220">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ce51-221">b.</span><span class="sxs-lookup"><span data-stu-id="1ce51-221">b.</span></span> <span data-ttu-id="1ce51-222">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="1ce51-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ce51-223">c.</span><span class="sxs-lookup"><span data-stu-id="1ce51-223">c.</span></span> <span data-ttu-id="1ce51-224">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1ce51-225">d.</span><span class="sxs-lookup"><span data-stu-id="1ce51-225">d.</span></span> <span data-ttu-id="1ce51-226">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1ce51-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="1ce51-227">建立 Google Apps 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1ce51-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="1ce51-228">hello 本節目標在於 toocreate 呼叫許 Simon Google 應用程式軟體中的使用者。</span><span class="sxs-lookup"><span data-stu-id="1ce51-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="1ce51-229">Google Apps 支援預設啟用的自動佈建。</span><span class="sxs-lookup"><span data-stu-id="1ce51-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="1ce51-230">在這一節沒有您需要進行的動作。</span><span class="sxs-lookup"><span data-stu-id="1ce51-230">There is no action for you in this section.</span></span> <span data-ttu-id="1ce51-231">如果使用者不存在於 Google 應用程式軟體，當您嘗試 tooaccess Google 應用程式軟體時，會建立一個新。</span><span class="sxs-lookup"><span data-stu-id="1ce51-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="1ce51-232">若要手動 toocreate 使用者，請連絡 hello [Google 支援小組](https://www.google.com/contact/)。</span><span class="sxs-lookup"><span data-stu-id="1ce51-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1ce51-233">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="1ce51-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1ce51-234">在本節中，以啟用 Azure 單一登入許 Simon toouse tooGoogle 應用程式授與存取權。</span><span class="sxs-lookup"><span data-stu-id="1ce51-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![指派使用者][200] 

<span data-ttu-id="1ce51-236">**tooassign 許 Simon tooGoogle 應用程式，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1ce51-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ce51-237">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1ce51-239">在 [hello] 應用程式清單中，選取**Google Apps**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-239">In hello applications list, select **Google Apps**.</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="1ce51-241">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1ce51-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1ce51-243">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ce51-243">Click **Add** button.</span></span> <span data-ttu-id="1ce51-244">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1ce51-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1ce51-246">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="1ce51-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1ce51-247">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ce51-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ce51-248">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1ce51-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1ce51-249">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1ce51-249">Testing single sign-on</span></span>

<span data-ttu-id="1ce51-250">在此區段中，您的單一登入設定，開啟 hello 存取面板 tootest [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md)，然後登入 hello 測試帳戶，然後按一下**Google Apps**磚 hello 存取面板中。</span><span class="sxs-lookup"><span data-stu-id="1ce51-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ce51-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="1ce51-251">Additional resources</span></span>

* [<span data-ttu-id="1ce51-252">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ce51-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ce51-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1ce51-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1ce51-254">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="1ce51-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png