---
title: "教學課程：Azure Active Directory 與 EverBridge 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 EverBridge 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: f5a97fc8df978dd55a73ae53516a82f884c14bec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="394c9-103">教學課程：Azure Active Directory 與 EverBridge 整合</span><span class="sxs-lookup"><span data-stu-id="394c9-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>

<span data-ttu-id="394c9-104">在本教學課程中，您將了解如何整合 EverBridge 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="394c9-104">In this tutorial, you learn how to integrate EverBridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="394c9-105">EverBridge 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="394c9-105">Integrating EverBridge with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="394c9-106">您可以在 Azure AD 中管控可存取 EverBridge 的人員</span><span class="sxs-lookup"><span data-stu-id="394c9-106">You can control in Azure AD who has access to EverBridge</span></span>
- <span data-ttu-id="394c9-107">您可讓使用者使用他們的 Azure AD 帳戶自動登入 EverBridge (單一登入)</span><span class="sxs-lookup"><span data-stu-id="394c9-107">You can enable your users to automatically get signed-on to EverBridge (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="394c9-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="394c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="394c9-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="394c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="394c9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="394c9-110">Prerequisites</span></span>

<span data-ttu-id="394c9-111">若要設定 Azure AD 與 EverBridge 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="394c9-111">To configure Azure AD integration with EverBridge, you need the following items:</span></span>

- <span data-ttu-id="394c9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="394c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="394c9-113">已啟用 EverBridge 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="394c9-113">An EverBridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="394c9-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="394c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="394c9-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="394c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="394c9-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="394c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="394c9-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="394c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="394c9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="394c9-118">Scenario description</span></span>
<span data-ttu-id="394c9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="394c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="394c9-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="394c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="394c9-121">從資源庫新增 EverBridge</span><span class="sxs-lookup"><span data-stu-id="394c9-121">Adding EverBridge from the gallery</span></span>
2. <span data-ttu-id="394c9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="394c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-the-gallery"></a><span data-ttu-id="394c9-123">從資源庫新增 EverBridge</span><span class="sxs-lookup"><span data-stu-id="394c9-123">Adding EverBridge from the gallery</span></span>
<span data-ttu-id="394c9-124">若要設定 EverBridge 與 Azure AD 的整合作業，您必須從資源庫將 EverBridge 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="394c9-124">To configure the integration of EverBridge into Azure AD, you need to add EverBridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="394c9-125">**若要從資源庫新增 EverBridge，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="394c9-125">**To add EverBridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="394c9-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="394c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="394c9-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="394c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="394c9-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="394c9-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="394c9-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="394c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="394c9-133">在搜尋方塊中，輸入 **EverBridge**。</span><span class="sxs-lookup"><span data-stu-id="394c9-133">In the search box, type **EverBridge**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. <span data-ttu-id="394c9-135">在結果窗格中，選取 [EverBridge]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="394c9-135">In the results panel, select **EverBridge**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="394c9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="394c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="394c9-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 EverBridge 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="394c9-138">In this section, you configure and test Azure AD single sign-on with EverBridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="394c9-139">若要讓單一登入運作，Azure AD 必須知道 EverBridge 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="394c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EverBridge is to a user in Azure AD.</span></span> <span data-ttu-id="394c9-140">換句話說，必須在 Azure AD 使用者和 EverBridge 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="394c9-140">In other words, a link relationship between an Azure AD user and the related user in EverBridge needs to be established.</span></span>

<span data-ttu-id="394c9-141">在 EverBridge 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="394c9-141">In EverBridge, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="394c9-142">若要設定及測試與 EverBridge 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="394c9-142">To configure and test Azure AD single sign-on with EverBridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="394c9-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="394c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="394c9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="394c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="394c9-145">**[建立 EverBridge 測試使用者](#creating-an-everbridge-test-user)** - 在 EverBridge 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="394c9-145">**[Creating an EverBridge test user](#creating-an-everbridge-test-user)** - to have a counterpart of Britta Simon in EverBridge that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="394c9-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="394c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="394c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="394c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="394c9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="394c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="394c9-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 EverBridge 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="394c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EverBridge application.</span></span>

<span data-ttu-id="394c9-150">**若要設定透過 EverBridge 使用 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="394c9-150">**To configure Azure AD single sign-on with EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="394c9-151">在 Azure 入口網站的 [EverBridge] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="394c9-151">In the Azure portal, on the **EverBridge** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="394c9-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="394c9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. <span data-ttu-id="394c9-155">在 [EverBridge 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="394c9-155">On the **EverBridge Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    <span data-ttu-id="394c9-157">a.</span><span class="sxs-lookup"><span data-stu-id="394c9-157">a.</span></span> <span data-ttu-id="394c9-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://sso.everbridge.net/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="394c9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.everbridge.net/<companyname>`</span></span>

    <span data-ttu-id="394c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="394c9-159">b.</span></span> <span data-ttu-id="394c9-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="394c9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="394c9-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="394c9-161">These values are not real.</span></span> <span data-ttu-id="394c9-162">請使用實際的識別碼和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="394c9-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="394c9-163">請連絡 [EverBridge 支援小組](mailto:support@everbridge.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="394c9-163">Contact [EverBridge support team](mailto:support@everbridge.com) to get these values.</span></span>
 
4. <span data-ttu-id="394c9-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="394c9-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. <span data-ttu-id="394c9-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="394c9-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="394c9-168">在 [EverBridge 組態] 區段上，按一下 [設定 EverBridge] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="394c9-168">On the **EverBridge Configuration** section, click **Configure EverBridge** to open **Configure sign-on** window.</span></span> <span data-ttu-id="394c9-169">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="394c9-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. <span data-ttu-id="394c9-171">若要取得為應用程式設定的 SSO，您必須以系統管理員身分登入 Everbridge 租用戶。</span><span class="sxs-lookup"><span data-stu-id="394c9-171">To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.</span></span>

7. <span data-ttu-id="394c9-172">在頂端的功能表中，按一下 [設定] 索引標籤，然後選取 [安全性] 之下的 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="394c9-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="394c9-174">a.</span><span class="sxs-lookup"><span data-stu-id="394c9-174">a.</span></span> <span data-ttu-id="394c9-175">在 [名稱] 文字方塊中，輸入識別碼提供者的名稱 (例如：您的公司名稱)。</span><span class="sxs-lookup"><span data-stu-id="394c9-175">In the **Name** textbox, type the name of Identifier Provider (for example: your company name).</span></span>
   
    <span data-ttu-id="394c9-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="394c9-176">b.</span></span> <span data-ttu-id="394c9-177">在 [API 名稱] 文字方塊中，輸入 API 的名稱。</span><span class="sxs-lookup"><span data-stu-id="394c9-177">In the **API Name** textbox, type the name of API.</span></span>
   
    <span data-ttu-id="394c9-178">c.</span><span class="sxs-lookup"><span data-stu-id="394c9-178">c.</span></span> <span data-ttu-id="394c9-179">按一下 [選擇檔案] 按鈕，上傳您從 Azure 入口網站下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="394c9-179">Click **Choose File** button to upload the metadata file which you downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="394c9-180">d.</span><span class="sxs-lookup"><span data-stu-id="394c9-180">d.</span></span> <span data-ttu-id="394c9-181">在 [SAML 身分識別位置] 中，選取 [身分識別位於 Subject 陳述式的 NameIdentifier 元素中]。</span><span class="sxs-lookup"><span data-stu-id="394c9-181">In the SAML Identity Location, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>
   
    <span data-ttu-id="394c9-182">e.</span><span class="sxs-lookup"><span data-stu-id="394c9-182">e.</span></span> <span data-ttu-id="394c9-183">在 [識別提供者登入 URL] 文字方塊中，貼上來自 Azure AD 的 SAML SSO URL 值。</span><span class="sxs-lookup"><span data-stu-id="394c9-183">In the **Identity Provider Login URL** textbox, paste the value of SAML SSO URL from Azure AD.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="394c9-185">f.</span><span class="sxs-lookup"><span data-stu-id="394c9-185">f.</span></span> <span data-ttu-id="394c9-186">在 [服務提供者起始的要求繫結] 中，選取 [HTTP 重新導向]。</span><span class="sxs-lookup"><span data-stu-id="394c9-186">In the Service Provider Initiated Request Binding, select **HTTP Redirect**.</span></span>

    <span data-ttu-id="394c9-187">g.</span><span class="sxs-lookup"><span data-stu-id="394c9-187">g.</span></span> <span data-ttu-id="394c9-188">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="394c9-188">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="394c9-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="394c9-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="394c9-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="394c9-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="394c9-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="394c9-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="394c9-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="394c9-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="394c9-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="394c9-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="394c9-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="394c9-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="394c9-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="394c9-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="394c9-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="394c9-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="394c9-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="394c9-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="394c9-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="394c9-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="394c9-204">a.</span><span class="sxs-lookup"><span data-stu-id="394c9-204">a.</span></span> <span data-ttu-id="394c9-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="394c9-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="394c9-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="394c9-206">b.</span></span> <span data-ttu-id="394c9-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="394c9-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="394c9-208">c.</span><span class="sxs-lookup"><span data-stu-id="394c9-208">c.</span></span> <span data-ttu-id="394c9-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="394c9-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="394c9-210">d.</span><span class="sxs-lookup"><span data-stu-id="394c9-210">d.</span></span> <span data-ttu-id="394c9-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="394c9-211">Click **Create**.</span></span>
 
### <a name="creating-an-everbridge-test-user"></a><span data-ttu-id="394c9-212">建立 EverBridge 測試使用者</span><span class="sxs-lookup"><span data-stu-id="394c9-212">Creating an EverBridge test user</span></span>

<span data-ttu-id="394c9-213">在本節中，您會在 Everbridge 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="394c9-213">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="394c9-214">與 [Everbridge 支援小組](mailto:support@everbridge.com)合作，在 Everbridge 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="394c9-214">Work with [EverBridge support team](mailto:support@everbridge.com) to add the users in the Everbridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="394c9-215">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="394c9-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="394c9-216">在本節中，您會將 EverBridge 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="394c9-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EverBridge.</span></span>

![指派使用者][200] 

<span data-ttu-id="394c9-218">**若要將 Britta Simon 指派到 EverBridge，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="394c9-218">**To assign Britta Simon to EverBridge, perform the following steps:**</span></span>

1. <span data-ttu-id="394c9-219">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="394c9-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="394c9-221">在應用程式清單中，選取 [EverBridge] 。</span><span class="sxs-lookup"><span data-stu-id="394c9-221">In the applications list, select **EverBridge**.</span></span>

    ![設定單一登入](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. <span data-ttu-id="394c9-223">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="394c9-223">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="394c9-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="394c9-225">Click **Add** button.</span></span> <span data-ttu-id="394c9-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="394c9-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="394c9-228">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="394c9-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="394c9-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="394c9-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="394c9-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="394c9-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="394c9-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="394c9-231">Testing single sign-on</span></span>

<span data-ttu-id="394c9-232">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="394c9-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="394c9-233">當您在存取面板中按一下 [Everbridge] 圖格時，應該會自動登入您的 Everbridge 應用程式。</span><span class="sxs-lookup"><span data-stu-id="394c9-233">When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="394c9-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="394c9-234">Additional resources</span></span>

* [<span data-ttu-id="394c9-235">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="394c9-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="394c9-236">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="394c9-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

