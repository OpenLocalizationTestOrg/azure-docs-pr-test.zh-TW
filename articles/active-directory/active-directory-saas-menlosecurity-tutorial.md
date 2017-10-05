---
title: "教學課程：Azure Active Directory 與 Menlo Security 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Menlo Security 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="7df98-103">教學課程：Azure Active Directory 與 Menlo Security 整合</span><span class="sxs-lookup"><span data-stu-id="7df98-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="7df98-104">在本教學課程中，您會了解如何將 Menlo Security 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="7df98-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7df98-105">將 Menlo Security 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7df98-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7df98-106">您可以在 Azure AD 中控制可存取 Menlo Security 的人員</span><span class="sxs-lookup"><span data-stu-id="7df98-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="7df98-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 Menlo Security (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7df98-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7df98-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7df98-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7df98-109">如果您想要知道與 Azure AD 整合的 SaaS 應用程式詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="7df98-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="7df98-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7df98-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7df98-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="7df98-111">Prerequisites</span></span>

<span data-ttu-id="7df98-112">若要設定 Azure AD 與 Menlo Security 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7df98-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="7df98-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7df98-113">An Azure AD subscription</span></span>
- <span data-ttu-id="7df98-114">已啟用 Menlo Security 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7df98-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7df98-115">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7df98-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7df98-116">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7df98-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7df98-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7df98-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7df98-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7df98-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7df98-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="7df98-119">Scenario description</span></span>
<span data-ttu-id="7df98-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7df98-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7df98-121">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7df98-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7df98-122">從資源庫新增 Menlo Security 安全性</span><span class="sxs-lookup"><span data-stu-id="7df98-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="7df98-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7df98-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="7df98-124">從資源庫新增 Menlo Security 安全性</span><span class="sxs-lookup"><span data-stu-id="7df98-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="7df98-125">如要設定將 Menlo Security 整合到 Azure AD 中，您需要從資源庫將 Menlo Security 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7df98-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7df98-126">**若要從資源庫新增 Menlo Security，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7df98-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7df98-127">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7df98-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7df98-129">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7df98-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7df98-130">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7df98-130">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7df98-132">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7df98-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7df98-134">在搜尋方塊中，輸入 **Menlo Security**。</span><span class="sxs-lookup"><span data-stu-id="7df98-134">In the search box, type **Menlo Security**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="7df98-136">在結果窗格中，選取 [Menlo Security]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7df98-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7df98-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7df98-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7df98-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Menlo Security 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7df98-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7df98-140">若要讓單一登入能夠運作，Azure AD 必須知道 Menlo Security 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7df98-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="7df98-141">換句話說，必須要建立某位 Azure AD 使用者與 Menlo Security 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7df98-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="7df98-142">建立此連結關聯性的方法，是將 Azure AD 中**使用者名稱**的值，指派為 Menlo Security 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="7df98-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="7df98-143">若要設定及測試與 Menlo Security 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7df98-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7df98-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7df98-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7df98-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7df98-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7df98-146">**[建立 Menlo Security 測試使用者](#creating-a-menlo-security-test-user)** - 使 Menlo Security 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="7df98-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7df98-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7df98-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7df98-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7df98-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7df98-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7df98-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7df98-150">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Menlo Security 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7df98-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="7df98-151">**若要使用 Menlo Security 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7df98-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="7df98-152">在 Azure 入口網站的 [Menlo Security] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7df98-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7df98-154">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7df98-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="7df98-156">在 [Menlo Security 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7df98-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="7df98-158">a.</span><span class="sxs-lookup"><span data-stu-id="7df98-158">a.</span></span> <span data-ttu-id="7df98-159">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="7df98-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="7df98-160">b.</span><span class="sxs-lookup"><span data-stu-id="7df98-160">b.</span></span> <span data-ttu-id="7df98-161">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="7df98-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7df98-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7df98-162">These values are not the real.</span></span> <span data-ttu-id="7df98-163">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="7df98-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7df98-164">請連絡 [Menlo Security 用戶端支援小組](https://www.menlosecurity.com/menlo-contact)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="7df98-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="7df98-165">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7df98-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="7df98-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7df98-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7df98-169">在 [Menlo Security 組態] 區段上，按一下 [設定 Menlo Security] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="7df98-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7df98-170">從 [快速參考] 區段中複製 [SAML 實體 ID] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="7df98-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="7df98-172">若要在 **Menlo Security** 端設定單一登入，請以系統管理員身分登入 **Menlo Security** 網站。</span><span class="sxs-lookup"><span data-stu-id="7df98-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="7df98-173">前往 [設定] 下的 [驗證] 並執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="7df98-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="7df98-175">a.</span><span class="sxs-lookup"><span data-stu-id="7df98-175">a.</span></span> <span data-ttu-id="7df98-176">勾選 [使用 SAML 啟用使用者驗證] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7df98-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="7df98-177">b.</span><span class="sxs-lookup"><span data-stu-id="7df98-177">b.</span></span> <span data-ttu-id="7df98-178">在 [允許外部存取] 選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="7df98-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="7df98-179">c.</span><span class="sxs-lookup"><span data-stu-id="7df98-179">c.</span></span> <span data-ttu-id="7df98-180">在 [SAML 提供者] 下選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="7df98-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="7df98-181">d.</span><span class="sxs-lookup"><span data-stu-id="7df98-181">d.</span></span> <span data-ttu-id="7df98-182">**SAML 2.0 端點**：將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 貼上。</span><span class="sxs-lookup"><span data-stu-id="7df98-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7df98-183">e.</span><span class="sxs-lookup"><span data-stu-id="7df98-183">e.</span></span> <span data-ttu-id="7df98-184">**服務識別項 (發行者)**︰將您從 Azure 入口網站複製的 **SAML 實體識別碼**貼上。</span><span class="sxs-lookup"><span data-stu-id="7df98-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7df98-185">f.</span><span class="sxs-lookup"><span data-stu-id="7df98-185">f.</span></span> <span data-ttu-id="7df98-186">**X.509 憑證**：在記事本中，將您從 Azure 入口網站下載的**憑證 (Base64)** 開啟，並在此方塊中將它貼上。</span><span class="sxs-lookup"><span data-stu-id="7df98-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="7df98-187">g.</span><span class="sxs-lookup"><span data-stu-id="7df98-187">g.</span></span> <span data-ttu-id="7df98-188">按一下 [儲存]  來儲存這些設定。</span><span class="sxs-lookup"><span data-stu-id="7df98-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="7df98-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7df98-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7df98-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7df98-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7df98-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7df98-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7df98-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7df98-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="7df98-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7df98-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7df98-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7df98-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7df98-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7df98-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7df98-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7df98-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7df98-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7df98-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7df98-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7df98-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7df98-204">a.</span><span class="sxs-lookup"><span data-stu-id="7df98-204">a.</span></span> <span data-ttu-id="7df98-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7df98-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7df98-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7df98-206">b.</span></span> <span data-ttu-id="7df98-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7df98-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7df98-208">c.</span><span class="sxs-lookup"><span data-stu-id="7df98-208">c.</span></span> <span data-ttu-id="7df98-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7df98-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7df98-210">d.</span><span class="sxs-lookup"><span data-stu-id="7df98-210">d.</span></span> <span data-ttu-id="7df98-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7df98-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="7df98-212">建立 Menlo Security 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7df98-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="7df98-213">在本節中，您要在 Menlo Security 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7df98-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="7df98-214">使用 [Menlo Security 用戶端支援小組](https://www.menlosecurity.com/menlo-contact)，在 Menlo Security 平台新增使用者。</span><span class="sxs-lookup"><span data-stu-id="7df98-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="7df98-215">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7df98-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7df98-216">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7df98-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7df98-217">在本節中，您會將 Menlo Security 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7df98-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![指派使用者][200] 

<span data-ttu-id="7df98-219">**若要將 Britta Simon 指派給 Menlo Security，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7df98-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="7df98-220">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7df98-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7df98-222">在應用程式清單中，選取 [Menlo Security]。</span><span class="sxs-lookup"><span data-stu-id="7df98-222">In the applications list, select **Menlo Security**.</span></span>

    ![設定單一登入](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="7df98-224">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7df98-224">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7df98-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7df98-226">Click **Add** button.</span></span> <span data-ttu-id="7df98-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7df98-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7df98-229">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7df98-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7df98-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7df98-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7df98-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7df98-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7df98-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7df98-232">Testing single sign-on</span></span>

<span data-ttu-id="7df98-233">在本節中，您會測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="7df98-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="7df98-234">在 "InPrivate" 或 "Incognito" 模式中開啟瀏覽器視窗，以觸發新的驗證。</span><span class="sxs-lookup"><span data-stu-id="7df98-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="7df98-235">在 Internet Explorer 中，使用 Ctrl+Shift+P。</span><span class="sxs-lookup"><span data-stu-id="7df98-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="7df98-236">在 Chrome 中，使用 Ctrl+Shift+N。</span><span class="sxs-lookup"><span data-stu-id="7df98-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="7df98-237">在隱私瀏覽視窗中，瀏覽受保護的資源並執行 Azure AD 登入。</span><span class="sxs-lookup"><span data-stu-id="7df98-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="7df98-238">成功登入後，即會在隔離的工作階段中將您帶往要求的網站。</span><span class="sxs-lookup"><span data-stu-id="7df98-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7df98-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="7df98-239">Additional resources</span></span>

* [<span data-ttu-id="7df98-240">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7df98-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7df98-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7df98-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

