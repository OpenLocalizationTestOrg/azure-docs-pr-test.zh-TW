---
title: "教學課程：Azure Active Directory 與 LCVista 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 LCVista 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c19f81da495eb7116b62797d1755d312a23f3805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="38f2a-103">教學課程：Azure Active Directory 與 LCVista 整合</span><span class="sxs-lookup"><span data-stu-id="38f2a-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="38f2a-104">在本教學課程中，您會了解如何將 LCVista 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="38f2a-104">In this tutorial, you learn how to integrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38f2a-105">LCVista 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="38f2a-105">Integrating LCVista with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38f2a-106">您可以在 Azure AD 中控制可存取 LCVista 的人員</span><span class="sxs-lookup"><span data-stu-id="38f2a-106">You can control in Azure AD who has access to LCVista</span></span>
- <span data-ttu-id="38f2a-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 LCVista (單一登入)</span><span class="sxs-lookup"><span data-stu-id="38f2a-107">You can enable your users to automatically get signed-on to LCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38f2a-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="38f2a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="38f2a-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="38f2a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38f2a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="38f2a-110">Prerequisites</span></span>

<span data-ttu-id="38f2a-111">若要設定與 LCVista 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="38f2a-111">To configure Azure AD integration with LCVista, you need the following items:</span></span>

- <span data-ttu-id="38f2a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="38f2a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38f2a-113">啟用 LCVista 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="38f2a-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38f2a-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="38f2a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38f2a-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="38f2a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38f2a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="38f2a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38f2a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="38f2a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38f2a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="38f2a-118">Scenario description</span></span>
<span data-ttu-id="38f2a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="38f2a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38f2a-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="38f2a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38f2a-121">從資源庫新增 LCVista</span><span class="sxs-lookup"><span data-stu-id="38f2a-121">Adding LCVista from the gallery</span></span>
2. <span data-ttu-id="38f2a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="38f2a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-the-gallery"></a><span data-ttu-id="38f2a-123">從資源庫新增 LCVista</span><span class="sxs-lookup"><span data-stu-id="38f2a-123">Adding LCVista from the gallery</span></span>
<span data-ttu-id="38f2a-124">若要設定將 LCVista 整合到 Azure AD 中，您需要從資源庫將 LCVista 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="38f2a-124">To configure the integration of LCVista into Azure AD, you need to add LCVista from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38f2a-125">**若要從資源庫新增 LCVista，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="38f2a-125">**To add LCVista from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38f2a-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="38f2a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38f2a-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38f2a-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="38f2a-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="38f2a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="38f2a-133">在搜尋方塊中，輸入 **LCVista**。</span><span class="sxs-lookup"><span data-stu-id="38f2a-133">In the search box, type **LCVista**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="38f2a-135">在結果窗格中，選取 [LCVista]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="38f2a-135">In the results panel, select **LCVista**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38f2a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="38f2a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38f2a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 LCVista 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="38f2a-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="38f2a-139">若要讓單一登入運作，Azure AD 必須知道 LCVista 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="38f2a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LCVista is to a user in Azure AD.</span></span> <span data-ttu-id="38f2a-140">換句話說，必須在 Azure AD 使用者與 LCVista 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="38f2a-140">In other words, a link relationship between an Azure AD user and the related user in LCVista needs to be established.</span></span>

<span data-ttu-id="38f2a-141">建立此連結關聯性的方法，是將 Azure AD 中**使用者名稱**的值，指派為 LCVista 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="38f2a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in LCVista.</span></span>

<span data-ttu-id="38f2a-142">若要設定及測試與 LCVista 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="38f2a-142">To configure and test Azure AD single sign-on with LCVista, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38f2a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="38f2a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38f2a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="38f2a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38f2a-145">**[建立 LCVista 測試使用者](#creating-a-lcvista-test-user)** - 使 LCVista 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="38f2a-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - to have a counterpart of Britta Simon in LCVista that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="38f2a-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="38f2a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38f2a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="38f2a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38f2a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="38f2a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38f2a-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 LCVista 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="38f2a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="38f2a-150">**若要設定與 LCVista 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="38f2a-150">**To configure Azure AD single sign-on with LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="38f2a-151">在 Azure 入口網站的 [LCVista] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-151">In the Azure portal, on the **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="38f2a-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="38f2a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="38f2a-155">在 [LCVista 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="38f2a-155">On the **LCVista Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="38f2a-157">a.</span><span class="sxs-lookup"><span data-stu-id="38f2a-157">a.</span></span> <span data-ttu-id="38f2a-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="38f2a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="38f2a-159">b.</span><span class="sxs-lookup"><span data-stu-id="38f2a-159">b.</span></span> <span data-ttu-id="38f2a-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="38f2a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="38f2a-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="38f2a-161">These values are not the real.</span></span> <span data-ttu-id="38f2a-162">請使用實際的識別碼和登入 URL 將這些值更新。</span><span class="sxs-lookup"><span data-stu-id="38f2a-162">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="38f2a-163">請連絡 [LCVista 用戶端支援小組](https://lcvista.com/contact)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="38f2a-163">Contact [LCVista Client support team](https://lcvista.com/contact) to get these values.</span></span> 

4. <span data-ttu-id="38f2a-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="38f2a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="38f2a-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="38f2a-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="38f2a-168">在 [LCVista 組態] 區段上，按一下 [設定 LCVista] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="38f2a-168">On the **LCVista Configuration** section, click **Configure LCVista** to open **Configure sign-on** window.</span></span> <span data-ttu-id="38f2a-169">從 [快速參考] 區段中複製 [SAML 實體 ID] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-169">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="38f2a-171">以系統管理員身分登入您的 LCVista 應用程式。</span><span class="sxs-lookup"><span data-stu-id="38f2a-171">Sign on to your LCVista application as an administrator.</span></span>

8. <span data-ttu-id="38f2a-172">在 [SAML 組態] 區段中，請勾選 [啟用 SAML 登入]，並輸入如下列映像中所述的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="38f2a-172">In the **SAML Config** section, check the **Enable SAML login** and enter the details as mentioned in below image.</span></span> 

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="38f2a-174">a.</span><span class="sxs-lookup"><span data-stu-id="38f2a-174">a.</span></span> <span data-ttu-id="38f2a-175">在 [實體識別碼] 區段中，將您從 Azure AD 複製的 [簽發者 URL] 貼上。</span><span class="sxs-lookup"><span data-stu-id="38f2a-175">Paste the **Issuer URL** which you have copied from Azure AD in the **Entity ID** section.</span></span> 

    <span data-ttu-id="38f2a-176">b.</span><span class="sxs-lookup"><span data-stu-id="38f2a-176">b.</span></span> <span data-ttu-id="38f2a-177">在 [URL] 區段中，將您從 Azure AD 複製的 [單一登入服務 URL] 貼上。</span><span class="sxs-lookup"><span data-stu-id="38f2a-177">Paste the **Single Sign-On Service URL** which you have copied from Azure AD in the **URL** section.</span></span>

    <span data-ttu-id="38f2a-178">c.</span><span class="sxs-lookup"><span data-stu-id="38f2a-178">c.</span></span> <span data-ttu-id="38f2a-179">將您從 Azure 入口網站下載之中繼資料 (XML) 中的 **X509Certificate** 值複製，並貼在 [x509 憑證] 區段中。</span><span class="sxs-lookup"><span data-stu-id="38f2a-179">From Metadata (XML) which you have downloaded from Azure portal, copy the value **X509Certificate** and paste it in the **x509 Certificate** section.</span></span>

    <span data-ttu-id="38f2a-180">d.</span><span class="sxs-lookup"><span data-stu-id="38f2a-180">d.</span></span> <span data-ttu-id="38f2a-181">在 [名字屬性] 文字方塊中，將 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname` 值貼上。</span><span class="sxs-lookup"><span data-stu-id="38f2a-181">In the **First name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="38f2a-182">e.</span><span class="sxs-lookup"><span data-stu-id="38f2a-182">e.</span></span> <span data-ttu-id="38f2a-183">在 [姓氏屬性] 文字方塊中，將 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname` 值貼上。</span><span class="sxs-lookup"><span data-stu-id="38f2a-183">In the **Last name attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="38f2a-184">f.</span><span class="sxs-lookup"><span data-stu-id="38f2a-184">f.</span></span> <span data-ttu-id="38f2a-185">在 [電子郵件屬性] 文字方塊中，將 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` 值貼上。</span><span class="sxs-lookup"><span data-stu-id="38f2a-185">In the **Email attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="38f2a-186">g.</span><span class="sxs-lookup"><span data-stu-id="38f2a-186">g.</span></span> <span data-ttu-id="38f2a-187">在 [使用者屬性] 文字方塊中，將 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name` 值貼上。</span><span class="sxs-lookup"><span data-stu-id="38f2a-187">In the **Username attribute** textbox, paste the value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="38f2a-188">e.</span><span class="sxs-lookup"><span data-stu-id="38f2a-188">e.</span></span> <span data-ttu-id="38f2a-189">按一下 [儲存]  來儲存這些設定。</span><span class="sxs-lookup"><span data-stu-id="38f2a-189">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="38f2a-190">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="38f2a-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="38f2a-191">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="38f2a-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="38f2a-192">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="38f2a-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38f2a-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="38f2a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="38f2a-194">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="38f2a-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="38f2a-196">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="38f2a-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38f2a-197">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="38f2a-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38f2a-199">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38f2a-201">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38f2a-203">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="38f2a-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38f2a-205">a.</span><span class="sxs-lookup"><span data-stu-id="38f2a-205">a.</span></span> <span data-ttu-id="38f2a-206">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="38f2a-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38f2a-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="38f2a-207">b.</span></span> <span data-ttu-id="38f2a-208">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="38f2a-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38f2a-209">c.</span><span class="sxs-lookup"><span data-stu-id="38f2a-209">c.</span></span> <span data-ttu-id="38f2a-210">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="38f2a-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="38f2a-211">d.</span><span class="sxs-lookup"><span data-stu-id="38f2a-211">d.</span></span> <span data-ttu-id="38f2a-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="38f2a-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="38f2a-213">建立 LCVista 測試使用者</span><span class="sxs-lookup"><span data-stu-id="38f2a-213">Creating a LCVista test user</span></span>

<span data-ttu-id="38f2a-214">在本節中，您要在 LCVista 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="38f2a-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="38f2a-215">若要在 LCVista 應用程式中新增使用者，您必須連絡 [LCVista 用戶端支援小組](https://lcvista.com/contact)。</span><span class="sxs-lookup"><span data-stu-id="38f2a-215">You need to contact [LCVista Client support team](https://lcvista.com/contact) to add the users in the LCVista application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="38f2a-216">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="38f2a-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="38f2a-217">在本節中，您會將 LCVista 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="38f2a-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LCVista.</span></span>

![指派使用者][200] 

<span data-ttu-id="38f2a-219">**若要將 Britta Simon 指派給 LCVista，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="38f2a-219">**To assign Britta Simon to LCVista, perform the following steps:**</span></span>

1. <span data-ttu-id="38f2a-220">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="38f2a-222">在應用程式清單中，選取 [LCVista]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-222">In the applications list, select **LCVista**.</span></span>

    ![設定單一登入](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="38f2a-224">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-224">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="38f2a-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="38f2a-226">Click **Add** button.</span></span> <span data-ttu-id="38f2a-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="38f2a-229">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="38f2a-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38f2a-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="38f2a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38f2a-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="38f2a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38f2a-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="38f2a-232">Testing single sign-on</span></span>

<span data-ttu-id="38f2a-233">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="38f2a-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="38f2a-234">在存取面板中按一下 [LCVista] 圖格，系統會將您重新導向至組織登入頁面。</span><span class="sxs-lookup"><span data-stu-id="38f2a-234">Click the LCVista tile in the Access Panel, you will be redirected to Organization sign on page.</span></span> <span data-ttu-id="38f2a-235">成功登入之後，系統會將您登入 LCVista 應用程式。</span><span class="sxs-lookup"><span data-stu-id="38f2a-235">After successful login, you will be signed-on to your LCVista application.</span></span> <span data-ttu-id="38f2a-236">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="38f2a-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38f2a-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="38f2a-237">Additional resources</span></span>

* [<span data-ttu-id="38f2a-238">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="38f2a-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38f2a-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="38f2a-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png
