---
title: "教學課程：Azure Active Directory 與 Google Apps 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Google Apps 之間的單一登入。"
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
ms.openlocfilehash: 065841d6b4fe50e953f01bba4d3f23de82b82726
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="efa84-103">教學課程：Azure Active Directory 與 Google Apps 整合</span><span class="sxs-lookup"><span data-stu-id="efa84-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="efa84-104">在本教學課程中，您會了解如何整合 Google Apps 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="efa84-104">In this tutorial, you learn how to integrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="efa84-105">Google Apps 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="efa84-105">Integrating Google Apps with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="efa84-106">您可以在 Azure AD 中控制可存取 Google Apps 的人員</span><span class="sxs-lookup"><span data-stu-id="efa84-106">You can control in Azure AD who has access to Google Apps</span></span>
- <span data-ttu-id="efa84-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Google Apps (單一登入)</span><span class="sxs-lookup"><span data-stu-id="efa84-107">You can enable your users to automatically get signed-on to Google Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="efa84-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="efa84-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="efa84-109">若您想了解 SaaS app 與 Azure AD 整合的更多資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="efa84-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efa84-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="efa84-110">Prerequisites</span></span>

<span data-ttu-id="efa84-111">若要設定 Azure AD 與 Google Apps 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="efa84-111">To configure Azure AD integration with Google Apps, you need the following items:</span></span>

- <span data-ttu-id="efa84-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="efa84-112">An Azure AD subscription</span></span>
- <span data-ttu-id="efa84-113">啟用 Google Apps 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="efa84-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="efa84-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="efa84-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="efa84-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="efa84-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="efa84-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="efa84-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="efa84-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="efa84-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="efa84-118">影片教學課程</span><span class="sxs-lookup"><span data-stu-id="efa84-118">Video tutorial</span></span>
<span data-ttu-id="efa84-119">如何在 2 分鐘內啟用單一登入至 Google Apps：</span><span class="sxs-lookup"><span data-stu-id="efa84-119">How to Enable Single Sign-On to Google Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="efa84-120">常見問題集</span><span class="sxs-lookup"><span data-stu-id="efa84-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="efa84-121">**問：Chromebook 及其他 Chrome 裝置是否與 Azure AD 單一登入相容？**</span><span class="sxs-lookup"><span data-stu-id="efa84-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="efa84-122">答：是，使用者能夠使用其 Azure AD 認證來登入其 Chromebook 裝置。</span><span class="sxs-lookup"><span data-stu-id="efa84-122">A: Yes, users are able to sign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="efa84-123">若要了解為何使用者可能收到兩次提供認證的提示，請參閱此 [Google Apps 支援文章](https://support.google.com/chrome/a/answer/6060880) 。</span><span class="sxs-lookup"><span data-stu-id="efa84-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="efa84-124">**問：如果我啟用單一登入，使用者是否將能夠使用其 Azure AD 認證來登入任何 Google 產品 (例如 Google Classroom、GMail、Google 雲端硬碟、YouTube 等)？**</span><span class="sxs-lookup"><span data-stu-id="efa84-124">**Q: If I enable single sign-on, will users be able to use their Azure AD credentials to sign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="efa84-125">答：是，視您選擇為您組織啟用或停用的 [Google Apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) 而定。</span><span class="sxs-lookup"><span data-stu-id="efa84-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose to enable or disable for your organization.</span></span>

3. <span data-ttu-id="efa84-126">**問：我是否可以只為一部分 Google Apps 使用者啟用單一登入？**</span><span class="sxs-lookup"><span data-stu-id="efa84-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="efa84-127">答：否，開啟單一登入會立即要求您的所有 Google Apps 使用者使用其 Azure AD 認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="efa84-127">A: No, turning on single sign-on immediately requires all your Google Apps users to authenticate with their Azure AD credentials.</span></span> <span data-ttu-id="efa84-128">由於 Google Apps 不支援使用多個身分識別提供者，因此您 Google Apps 環境的身分識別提供者可以是 Azure AD 或 Google 其中之一，但不可同時是兩者。</span><span class="sxs-lookup"><span data-stu-id="efa84-128">Because Google Apps doesn't support having multiple identity providers, the identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at the same time.</span></span>

4. <span data-ttu-id="efa84-129">**問：如果使用者透過 Windows 登入，他們是否會自動向 Google Apps 進行驗證，而不會收到輸入密碼的提示？**</span><span class="sxs-lookup"><span data-stu-id="efa84-129">**Q: If a user is signed in through Windows, are they automatically authenticate to Google Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="efa84-130">答：有兩個選項可允許這樣的情況。</span><span class="sxs-lookup"><span data-stu-id="efa84-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="efa84-131">第一個是，使用者可以透過 [Azure Active Directory Join](active-directory-azureadjoin-overview.md)登入 Windows 10 裝置。</span><span class="sxs-lookup"><span data-stu-id="efa84-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="efa84-132">另一個是，使用者可以登入已加入某個內部部署 Active Directory 網域的 Windows 裝置，其中此內部部署 Active Directory 已透過 [Active Directory 同盟服務 (AD FS)](active-directory-aadconnect-user-signin.md) 部署而能夠單一登入到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="efa84-132">Alternatively, users could sign into Windows devices that are domain-joined to an on-premises Active Directory that has been enabled for single sign-on to Azure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="efa84-133">這兩個選項都需要您執行下列教學課程的步驟，才能在 Azure AD 與 Google Apps 之間啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="efa84-133">Both options require you to perform the steps in the following tutorial to enable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="efa84-134">案例描述</span><span class="sxs-lookup"><span data-stu-id="efa84-134">Scenario description</span></span>
<span data-ttu-id="efa84-135">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="efa84-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="efa84-136">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="efa84-136">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="efa84-137">從資源庫新增 Google Apps</span><span class="sxs-lookup"><span data-stu-id="efa84-137">Adding Google Apps from the gallery</span></span>
2. <span data-ttu-id="efa84-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="efa84-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-the-gallery"></a><span data-ttu-id="efa84-139">從資源庫新增 Google Apps</span><span class="sxs-lookup"><span data-stu-id="efa84-139">Adding Google Apps from the gallery</span></span>
<span data-ttu-id="efa84-140">若要設定將 Google Apps 整合到 Azure AD 中，您需要從資源庫將 Google Apps 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="efa84-140">To configure the integration of Google Apps into Azure AD, you need to add Google Apps from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="efa84-141">**若要從資源庫新增 Google Apps，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="efa84-141">**To add Google Apps from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="efa84-142">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="efa84-142">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="efa84-144">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="efa84-144">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="efa84-145">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="efa84-145">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="efa84-147">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="efa84-147">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="efa84-149">在搜尋方塊中，輸入 **Google Apps**。</span><span class="sxs-lookup"><span data-stu-id="efa84-149">In the search box, type **Google Apps**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="efa84-151">在結果面板中，選取 [Google Apps]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="efa84-151">In the results panel, select **Google Apps**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="efa84-153">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="efa84-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="efa84-154">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Google Apps 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="efa84-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="efa84-155">若要讓單一登入運作，Azure AD 必須知道 Google Apps 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="efa84-155">For single sign-on to work, Azure AD needs to know what the counterpart user in Google Apps is to a user in Azure AD.</span></span> <span data-ttu-id="efa84-156">換句話說，必須在 Azure AD 使用者和 Google Apps 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="efa84-156">In other words, a link relationship between an Azure AD user and the related user in Google Apps needs to be established.</span></span>

<span data-ttu-id="efa84-157">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值，指派為 Google Apps 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="efa84-157">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Google Apps.</span></span>

<span data-ttu-id="efa84-158">若要設定及測試與 Google Apps 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="efa84-158">To configure and test Azure AD single sign-on with Google Apps, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="efa84-159">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="efa84-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="efa84-160">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="efa84-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="efa84-161">**[建立 Google Apps 測試使用者](#creating-a-google-apps-test-user)** - 使 Google Apps 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="efa84-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - to have a counterpart of Britta Simon in Google Apps that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="efa84-162">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="efa84-162">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="efa84-163">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="efa84-163">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="efa84-164">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="efa84-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="efa84-165">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Google Apps 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="efa84-165">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="efa84-166">**若要設定與 Google Apps 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="efa84-166">**To configure Azure AD single sign-on with Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="efa84-167">在 Azure 入口網站的 [Google Apps] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="efa84-167">In the Azure portal, on the **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="efa84-169">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="efa84-169">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="efa84-171">在 [Google Apps 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="efa84-171">On the **Google Apps Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="efa84-173">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="efa84-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="efa84-174">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="efa84-174">This value is not real.</span></span> <span data-ttu-id="efa84-175">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="efa84-175">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="efa84-176">請連絡 [Google 支援小組](https://www.google.com/contact/)。</span><span class="sxs-lookup"><span data-stu-id="efa84-176">contact the [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="efa84-177">在 [SAML 簽署憑證] 區段上，按一下 [憑證]，然後將憑證儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="efa84-177">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="efa84-179">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="efa84-179">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="efa84-181">在 [Google Apps 組態] 區段上，按一下 [設定 Google Apps] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="efa84-181">On the **Google Apps Configuration** section, click **Configure Google Apps** to open **Configure sign-on** window.</span></span> <span data-ttu-id="efa84-182">從 [快速參考] 區段中，複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="efa84-182">Copy the **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="efa84-184">在瀏覽器中開啟新索引標籤，然後使用系統管理員帳戶登入 [Google Apps 管理控制台](http://admin.google.com/) 。</span><span class="sxs-lookup"><span data-stu-id="efa84-184">Open a new tab in your browser, and sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="efa84-185">按一下 [安全性] 。</span><span class="sxs-lookup"><span data-stu-id="efa84-185">Click **Security**.</span></span> <span data-ttu-id="efa84-186">如果您沒有看到連結，它可能隱藏在畫面底部的 [其他控制項]  功能表之下。</span><span class="sxs-lookup"><span data-stu-id="efa84-186">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![按一下 [安全性]。][10]

9. <span data-ttu-id="efa84-188">在 [安全性] 頁面上，按一下 [設定單一登入 (SSO)]。</span><span class="sxs-lookup"><span data-stu-id="efa84-188">On the **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![按一下 [SSO]。][11]

10. <span data-ttu-id="efa84-190">執行下列組態變更：</span><span class="sxs-lookup"><span data-stu-id="efa84-190">Perform the following configuration changes:</span></span>
   
    ![設定 SSO][12]
   
    <span data-ttu-id="efa84-192">a.</span><span class="sxs-lookup"><span data-stu-id="efa84-192">a.</span></span> <span data-ttu-id="efa84-193">選取 [使用第三方識別提供者來設定 SSO]。</span><span class="sxs-lookup"><span data-stu-id="efa84-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="efa84-194">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="efa84-194">b.</span></span> <span data-ttu-id="efa84-195">在 Google Apps 的 [登入頁面 URL] 欄位中，貼上您從 Azure 入口網站複製的 [單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="efa84-195">In the **Sign-in page URL** field in Google Apps, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="efa84-196">c.</span><span class="sxs-lookup"><span data-stu-id="efa84-196">c.</span></span> <span data-ttu-id="efa84-197">在 Google Apps 的 [登出頁面 URL] 欄位中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="efa84-197">In the **Sign-out page URL** field in Google Apps, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="efa84-198">d.</span><span class="sxs-lookup"><span data-stu-id="efa84-198">d.</span></span> <span data-ttu-id="efa84-199">在 Google Apps 的 [變更密碼 URL] 欄位中，貼上您從 Azure 入口網站複製的 [變更密碼 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="efa84-199">In the **Change password URL** field in Google Apps, paste the value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="efa84-200">e.</span><span class="sxs-lookup"><span data-stu-id="efa84-200">e.</span></span> <span data-ttu-id="efa84-201">在 Google Apps 中，對於 [驗證憑證]，上傳您已從 Azure 入口網站下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="efa84-201">In Google Apps, for the **Verification certificate**, upload the certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="efa84-202">f.</span><span class="sxs-lookup"><span data-stu-id="efa84-202">f.</span></span> <span data-ttu-id="efa84-203">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="efa84-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="efa84-204">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="efa84-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="efa84-205">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="efa84-205">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="efa84-206">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="efa84-206">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="efa84-207">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="efa84-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="efa84-208">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="efa84-208">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="efa84-210">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="efa84-210">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="efa84-211">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="efa84-211">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="efa84-213">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="efa84-213">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="efa84-215">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="efa84-215">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="efa84-217">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="efa84-217">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="efa84-219">a.</span><span class="sxs-lookup"><span data-stu-id="efa84-219">a.</span></span> <span data-ttu-id="efa84-220">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="efa84-220">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="efa84-221">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="efa84-221">b.</span></span> <span data-ttu-id="efa84-222">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="efa84-222">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="efa84-223">c.</span><span class="sxs-lookup"><span data-stu-id="efa84-223">c.</span></span> <span data-ttu-id="efa84-224">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="efa84-224">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="efa84-225">d.</span><span class="sxs-lookup"><span data-stu-id="efa84-225">d.</span></span> <span data-ttu-id="efa84-226">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="efa84-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="efa84-227">建立 Google Apps 測試使用者</span><span class="sxs-lookup"><span data-stu-id="efa84-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="efa84-228">本節目標是要在 Google Apps Software 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="efa84-228">The objective of this section is to create a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="efa84-229">Google Apps 支援預設啟用的自動佈建。</span><span class="sxs-lookup"><span data-stu-id="efa84-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="efa84-230">在這一節沒有您需要進行的動作。</span><span class="sxs-lookup"><span data-stu-id="efa84-230">There is no action for you in this section.</span></span> <span data-ttu-id="efa84-231">如果 Google Apps Software 中還沒有使用者，當您嘗試存取 Google Apps Software 時，就會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="efa84-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt to access Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="efa84-232">如果您需要手動建立使用者，請連絡 [Google 支援小組](https://www.google.com/contact/)。</span><span class="sxs-lookup"><span data-stu-id="efa84-232">If you need to create a user manually, contact the [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="efa84-233">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="efa84-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="efa84-234">在本節中，您會將 Google Apps 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="efa84-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Google Apps.</span></span>

![指派使用者][200] 

<span data-ttu-id="efa84-236">**若要將 Britta Simon 指派給 Google Apps，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="efa84-236">**To assign Britta Simon to Google Apps, perform the following steps:**</span></span>

1. <span data-ttu-id="efa84-237">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="efa84-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="efa84-239">在應用程式清單中，選取 [Google Apps]。</span><span class="sxs-lookup"><span data-stu-id="efa84-239">In the applications list, select **Google Apps**.</span></span>

    ![設定單一登入](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="efa84-241">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="efa84-241">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="efa84-243">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="efa84-243">Click **Add** button.</span></span> <span data-ttu-id="efa84-244">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="efa84-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="efa84-246">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="efa84-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="efa84-247">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="efa84-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="efa84-248">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="efa84-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="efa84-249">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="efa84-249">Testing single sign-on</span></span>

<span data-ttu-id="efa84-250">在本節中，若要測試您的單一登入設定，請開啟位於 [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md) 的存取面板，登入測試帳戶，然後在存取面板中按一下 [Google Apps] 圖格。</span><span class="sxs-lookup"><span data-stu-id="efa84-250">In this section, to test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into the test account, and click **Google Apps** tile in the Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efa84-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="efa84-251">Additional resources</span></span>

* [<span data-ttu-id="efa84-252">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="efa84-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="efa84-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="efa84-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="efa84-254">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="efa84-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

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