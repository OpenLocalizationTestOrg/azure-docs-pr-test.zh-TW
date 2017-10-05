---
title: "教學課程：Azure Active Directory 與 Intacct 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Intacct 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c203b192b9da0d280cbd7f6c123219242ee4a3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="7da82-103">教學課程：Azure Active Directory 與 Intacct 整合</span><span class="sxs-lookup"><span data-stu-id="7da82-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="7da82-104">在本教學課程中，您會了解如何整合 Intacct 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7da82-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7da82-105">Intacct 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7da82-105">Integrating Intacct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7da82-106">您可以在 Azure AD 中控制可存取 Intacct 的人員</span><span class="sxs-lookup"><span data-stu-id="7da82-106">You can control in Azure AD who has access to Intacct</span></span>
- <span data-ttu-id="7da82-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Intacct (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7da82-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7da82-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7da82-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7da82-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7da82-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7da82-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7da82-110">Prerequisites</span></span>

<span data-ttu-id="7da82-111">若要設定 Azure AD 與 Intacct 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7da82-111">To configure Azure AD integration with Intacct, you need the following items:</span></span>

- <span data-ttu-id="7da82-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7da82-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7da82-113">已啟用 Intacct 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7da82-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7da82-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7da82-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7da82-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7da82-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7da82-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7da82-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7da82-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7da82-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7da82-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7da82-118">Scenario description</span></span>
<span data-ttu-id="7da82-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7da82-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7da82-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7da82-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7da82-121">從資源庫新增 Intacct</span><span class="sxs-lookup"><span data-stu-id="7da82-121">Adding Intacct from the gallery</span></span>
2. <span data-ttu-id="7da82-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7da82-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-the-gallery"></a><span data-ttu-id="7da82-123">從資源庫新增 Intacct</span><span class="sxs-lookup"><span data-stu-id="7da82-123">Adding Intacct from the gallery</span></span>
<span data-ttu-id="7da82-124">若要設定將 Intacct 整合到 Azure AD 中，您需要從資源庫將 Intacct 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7da82-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7da82-125">**若要從資源庫新增 Intacct，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7da82-125">**To add Intacct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7da82-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7da82-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7da82-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7da82-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7da82-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7da82-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7da82-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7da82-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7da82-133">在搜尋方塊中，輸入 **Intacct**。</span><span class="sxs-lookup"><span data-stu-id="7da82-133">In the search box, type **Intacct**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="7da82-135">在結果窗格中，選取 [Intacct]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da82-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7da82-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7da82-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7da82-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Intacct 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7da82-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7da82-139">若要讓單一登入能夠運作，Azure AD 必須知道 Intacct 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7da82-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span></span> <span data-ttu-id="7da82-140">換句話說，必須建立 Azure AD 使用者和 Intacct 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7da82-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span></span>

<span data-ttu-id="7da82-141">在 Intacct 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7da82-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7da82-142">若要設定及測試與 Intacct 搭配運作的 Azure AD 單一登入，您需要完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="7da82-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7da82-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7da82-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7da82-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7da82-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7da82-145">**[建立 Intacct 測試使用者](#creating-an-intacct-test-user)** - 在 Intacct 中建立 Britta Simon 的對應項目，且該項目必須與 Azure AD 中代表 Britta Simon 的項目連結。</span><span class="sxs-lookup"><span data-stu-id="7da82-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7da82-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7da82-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7da82-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7da82-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7da82-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7da82-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7da82-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Intacct 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7da82-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="7da82-150">**若要設定與 Intacct 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7da82-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="7da82-151">在 Azure 入口網站的 [Intacct] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7da82-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7da82-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7da82-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="7da82-155">在 [Intacct 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7da82-155">On the **Intacct Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="7da82-157">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="7da82-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="7da82-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="7da82-158">This value is not real.</span></span> <span data-ttu-id="7da82-159">請使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="7da82-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="7da82-160">請連絡 [Intacct 支援小組](https://us.intacct.com/support)以取得這個值。</span><span class="sxs-lookup"><span data-stu-id="7da82-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span></span>

4. <span data-ttu-id="7da82-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7da82-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="7da82-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7da82-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7da82-165">在 [Intacct 組態] 區段上，按一下 [設定 Intacct] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="7da82-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7da82-166">從 [快速參考] 區段中複製 [SAML 實體 ID 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="7da82-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="7da82-168">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Intacct 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7da82-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="7da82-169">按一下 [公司] 索引標籤，然後按一下 [公司資訊]。</span><span class="sxs-lookup"><span data-stu-id="7da82-169">Click the **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="7da82-170">![公司](./media/active-directory-saas-intacct-tutorial/ic790037.png "公司")</span><span class="sxs-lookup"><span data-stu-id="7da82-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="7da82-171">按一下 [安全性] 索引標籤，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="7da82-171">Click the **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="7da82-172">![安全性](./media/active-directory-saas-intacct-tutorial/ic790038.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="7da82-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="7da82-173">在 [單一登入 (SSO)]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7da82-173">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

    <span data-ttu-id="7da82-174">![單一登入](./media/active-directory-saas-intacct-tutorial/ic790039.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="7da82-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="7da82-175">a.</span><span class="sxs-lookup"><span data-stu-id="7da82-175">a.</span></span> <span data-ttu-id="7da82-176">選取 [啟用單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="7da82-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="7da82-177">b.</span><span class="sxs-lookup"><span data-stu-id="7da82-177">b.</span></span> <span data-ttu-id="7da82-178">在 [身分識別提供者類型]，選取 **SAML 2.0**。</span><span class="sxs-lookup"><span data-stu-id="7da82-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="7da82-179">c.</span><span class="sxs-lookup"><span data-stu-id="7da82-179">c.</span></span> <span data-ttu-id="7da82-180">在 [簽發者 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="7da82-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="7da82-181">d.</span><span class="sxs-lookup"><span data-stu-id="7da82-181">d.</span></span> <span data-ttu-id="7da82-182">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="7da82-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7da82-183">e.</span><span class="sxs-lookup"><span data-stu-id="7da82-183">e.</span></span> <span data-ttu-id="7da82-184">在記事本中開啟您的 **base-64** 編碼的憑證，將其內容複製到您的剪貼簿，然後貼到 [憑證] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="7da82-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   
    <span data-ttu-id="7da82-185">f.</span><span class="sxs-lookup"><span data-stu-id="7da82-185">f.</span></span> <span data-ttu-id="7da82-186">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7da82-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7da82-187">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7da82-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7da82-188">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7da82-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7da82-189">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7da82-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7da82-190">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7da82-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="7da82-191">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7da82-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7da82-193">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7da82-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7da82-194">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7da82-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7da82-196">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7da82-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7da82-198">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7da82-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7da82-200">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7da82-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7da82-202">a.</span><span class="sxs-lookup"><span data-stu-id="7da82-202">a.</span></span> <span data-ttu-id="7da82-203">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7da82-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7da82-204">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da82-204">b.</span></span> <span data-ttu-id="7da82-205">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7da82-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7da82-206">c.</span><span class="sxs-lookup"><span data-stu-id="7da82-206">c.</span></span> <span data-ttu-id="7da82-207">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7da82-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7da82-208">d.</span><span class="sxs-lookup"><span data-stu-id="7da82-208">d.</span></span> <span data-ttu-id="7da82-209">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7da82-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="7da82-210">建立 Intacct 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7da82-210">Creating an Intacct test user</span></span>

<span data-ttu-id="7da82-211">若要設定 Azure AD 使用者以便讓他們能夠登入 Intacct，則必須將他們佈建到 Intacct。</span><span class="sxs-lookup"><span data-stu-id="7da82-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="7da82-212">在 Intacct 中，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="7da82-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="7da82-213">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7da82-213">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="7da82-214">登入您的 **Intacct** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7da82-214">Sign in to your **Intacct** tenant.</span></span>

2. <span data-ttu-id="7da82-215">按一下 [公司] 索引標籤，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="7da82-215">Click the **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="7da82-216">![使用者](./media/active-directory-saas-intacct-tutorial/ic790041.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="7da82-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="7da82-217">按一下 [新增] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7da82-217">Click the **Add** tab.</span></span>

    <span data-ttu-id="7da82-218">![新增](./media/active-directory-saas-intacct-tutorial/ic790042.png "新增")</span><span class="sxs-lookup"><span data-stu-id="7da82-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="7da82-219">在 [使用者資訊]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7da82-219">In the **User Information** section, perform the following steps:</span></span>

    <span data-ttu-id="7da82-220">![使用者資訊](./media/active-directory-saas-intacct-tutorial/ic790043.png "使用者資訊")</span><span class="sxs-lookup"><span data-stu-id="7da82-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="7da82-221">a.</span><span class="sxs-lookup"><span data-stu-id="7da82-221">a.</span></span> <span data-ttu-id="7da82-222">在 [使用者資訊] 區段中，為您要佈建的 Azure AD 帳戶輸入 [使用者識別碼]、[姓氏]、[名字]、[電子郵件地址]、[職稱] 和 [電話]。</span><span class="sxs-lookup"><span data-stu-id="7da82-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>

    <span data-ttu-id="7da82-223">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da82-223">b.</span></span> <span data-ttu-id="7da82-224">選取您要佈建之 Azure AD 帳戶的 [系統管理員權限]。</span><span class="sxs-lookup"><span data-stu-id="7da82-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   
    <span data-ttu-id="7da82-225">c.</span><span class="sxs-lookup"><span data-stu-id="7da82-225">c.</span></span> <span data-ttu-id="7da82-226">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7da82-226">Click **Save**.</span></span> <span data-ttu-id="7da82-227">Azure AD 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="7da82-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="7da82-228">若要佈建 Azure AD 使用者帳戶，您可以使用 Intacct 所提供的其他 Intacct 使用者帳戶建立工具或 API。</span><span class="sxs-lookup"><span data-stu-id="7da82-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7da82-229">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7da82-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7da82-230">在本節中，您會將 Intacct 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7da82-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span></span>

![指派使用者][200] 

<span data-ttu-id="7da82-232">**若要將 Britta Simon 指派給 Intacct，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7da82-232">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="7da82-233">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7da82-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7da82-235">在應用程式清單中，選取 [Intacct]。</span><span class="sxs-lookup"><span data-stu-id="7da82-235">In the applications list, select **Intacct**.</span></span>

    ![設定單一登入](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="7da82-237">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7da82-237">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7da82-239">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7da82-239">Click **Add** button.</span></span> <span data-ttu-id="7da82-240">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7da82-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7da82-242">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7da82-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7da82-243">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7da82-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7da82-244">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7da82-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7da82-245">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7da82-245">Testing single sign-on</span></span>

<span data-ttu-id="7da82-246">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="7da82-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="7da82-247">當您在存取面板中按一下 [Intacct] 圖格時，應該會自動登入您的 Intacct 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7da82-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7da82-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="7da82-248">Additional resources</span></span>

* [<span data-ttu-id="7da82-249">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7da82-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7da82-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7da82-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

