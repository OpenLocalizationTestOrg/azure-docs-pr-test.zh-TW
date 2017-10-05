---
title: "教學課程：Azure Active Directory 與 Expensify 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Expensify 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: e45576fd92706881121469ccd82150b3d48059cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="8bf5c-103">教學課程：Azure Active Directory 與 Expensify 整合</span><span class="sxs-lookup"><span data-stu-id="8bf5c-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="8bf5c-104">在本教學課程中，您會了解如何將 Expensify 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8bf5c-105">將 Expensify 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="8bf5c-105">Integrating Expensify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8bf5c-106">您可以在 Azure AD 中控制可存取 Expensify 的人員</span><span class="sxs-lookup"><span data-stu-id="8bf5c-106">You can control in Azure AD who has access to Expensify</span></span>
- <span data-ttu-id="8bf5c-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Expensify (單一登入)</span><span class="sxs-lookup"><span data-stu-id="8bf5c-107">You can enable your users to automatically get signed-on to Expensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8bf5c-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="8bf5c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8bf5c-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bf5c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8bf5c-110">Prerequisites</span></span>

<span data-ttu-id="8bf5c-111">若要設定 Azure AD 與 Expensify 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="8bf5c-111">To configure Azure AD integration with Expensify, you need the following items:</span></span>

- <span data-ttu-id="8bf5c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8bf5c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8bf5c-113">已啟用 Expensify 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8bf5c-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8bf5c-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8bf5c-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8bf5c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8bf5c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8bf5c-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8bf5c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8bf5c-118">Scenario description</span></span>
<span data-ttu-id="8bf5c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8bf5c-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="8bf5c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8bf5c-121">從資源庫新增 Expensify</span><span class="sxs-lookup"><span data-stu-id="8bf5c-121">Adding Expensify from the gallery</span></span>
2. <span data-ttu-id="8bf5c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8bf5c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-the-gallery"></a><span data-ttu-id="8bf5c-123">從資源庫新增 Expensify</span><span class="sxs-lookup"><span data-stu-id="8bf5c-123">Adding Expensify from the gallery</span></span>
<span data-ttu-id="8bf5c-124">若要設定將 Expensify 整合到 Azure AD 中，您需要從資源庫將 Expensify 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8bf5c-125">**若要從資源庫新增 Expensify，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8bf5c-125">**To add Expensify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8bf5c-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8bf5c-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8bf5c-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8bf5c-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8bf5c-133">在搜尋方塊中，輸入 **Expensify**。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-133">In the search box, type **Expensify**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="8bf5c-135">在結果窗格中，選取 [Expensify]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-135">In the results panel, select **Expensify**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8bf5c-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8bf5c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8bf5c-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Expensify 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8bf5c-139">若要讓單一登入能夠運作，Azure AD 必須知道 Expensify 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span></span> <span data-ttu-id="8bf5c-140">換句話說，必須在 Azure AD 使用者與 Expensify 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-140">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span></span>

<span data-ttu-id="8bf5c-141">在 Expensify 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-141">In Expensify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8bf5c-142">若要設定及測試與 Expensify 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="8bf5c-142">To configure and test Azure AD single sign-on with Expensify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8bf5c-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8bf5c-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8bf5c-145">**[建立 Expensify 測試使用者](#creating-an-expensify-test-user)** - 在 Expensify 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8bf5c-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8bf5c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8bf5c-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8bf5c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8bf5c-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Expensify 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="8bf5c-150">**若要設定與 Expensify 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8bf5c-150">**To configure Azure AD single sign-on with Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="8bf5c-151">在 Azure 入口網站的 [Expensify] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-151">In the Azure portal, on the **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8bf5c-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="8bf5c-155">在 [Expensify 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8bf5c-155">On the **Expensify Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="8bf5c-157">a.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-157">a.</span></span> <span data-ttu-id="8bf5c-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="8bf5c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="8bf5c-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-159">b.</span></span> <span data-ttu-id="8bf5c-160">在 [識別碼 URL] 文字方塊中，使用下列模式輸入 URL：`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="8bf5c-160">In the **Identifier URL** textbox, type a URL using the following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="8bf5c-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-161">These values are not real.</span></span> <span data-ttu-id="8bf5c-162">使用實際的登入 URL 和識別碼 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-162">Update these values with the actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="8bf5c-163">請連絡 [Expensify 用戶端支援小組](mailto:help@expensify.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-163">Contact [Expensify Client support team](mailto:help@expensify.com) to get these values.</span></span> 
 
4. <span data-ttu-id="8bf5c-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="8bf5c-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8bf5c-168">若要在 Expensify 中啟用 SSO，您必須先在應用程式中啟用 [網域控制]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-168">To enable SSO in Expensify, you first need to enable **Domain Control** in the application.</span></span> <span data-ttu-id="8bf5c-169">您可以透過[這裡](http://help.expensify.com/domain-control)所列的步驟，在應用程式中啟用 [網域控制]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-169">You can enable Domain Control in the application through the steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="8bf5c-170">如需其他支援，請與 [Expensify 用戶端支援小組](mailto:help@expensify.com)合作。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="8bf5c-171">一旦啟用了 [網域控制]，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8bf5c-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="8bf5c-173">a.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-173">a.</span></span> <span data-ttu-id="8bf5c-174">登入 Expensify 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-174">Sign on to your Expensify application.</span></span>
    
    <span data-ttu-id="8bf5c-175">b.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-175">b.</span></span> <span data-ttu-id="8bf5c-176">在頂端工具列中，按一下 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-176">In the toolbar on the top, click **Admin**.</span></span>
    
    <span data-ttu-id="8bf5c-177">c.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-177">c.</span></span> <span data-ttu-id="8bf5c-178">按一下左面板中的 [網域]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-178">In the left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="8bf5c-179">d.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-179">d.</span></span> <span data-ttu-id="8bf5c-180">按一下已驗證的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="8bf5c-181">e.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-181">e.</span></span> <span data-ttu-id="8bf5c-182">在左面板中按一下 [SAML]，然後選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-182">In the left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="8bf5c-183">f.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-183">f.</span></span> <span data-ttu-id="8bf5c-184">從記事本中的 Azure AD 開啟下載的同盟中繼資料，複製其內容並貼到 [識別提供者中繼資料] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-184">Open the downloaded Federation Metadata from Azure AD in notepad, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="8bf5c-185">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="8bf5c-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8bf5c-186">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8bf5c-187">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8bf5c-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8bf5c-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8bf5c-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="8bf5c-189">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8bf5c-191">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8bf5c-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8bf5c-192">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8bf5c-194">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8bf5c-196">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8bf5c-198">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8bf5c-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8bf5c-200">a.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-200">a.</span></span> <span data-ttu-id="8bf5c-201">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8bf5c-202">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-202">b.</span></span> <span data-ttu-id="8bf5c-203">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8bf5c-204">c.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-204">c.</span></span> <span data-ttu-id="8bf5c-205">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8bf5c-206">d.</span><span class="sxs-lookup"><span data-stu-id="8bf5c-206">d.</span></span> <span data-ttu-id="8bf5c-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="8bf5c-208">建立 Expensify 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8bf5c-208">Creating an Expensify test user</span></span>

<span data-ttu-id="8bf5c-209">在本節中，您會在 Expensify 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="8bf5c-210">請與 [Expensify 用戶端支援小組](mailto:help@expensify.com)合作，在 Expensify 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-210">Work with [Expensify Client support team](mailto:help@expensify.com) to add the users in the Expensify platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8bf5c-211">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8bf5c-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8bf5c-212">在本節中，您會授與 Britta Simon 對 Expensify 的存取權，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Expensify.</span></span>

![指派使用者][200] 

<span data-ttu-id="8bf5c-214">**若要將 Britta Simon 指派給 Expensify，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8bf5c-214">**To assign Britta Simon to Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="8bf5c-215">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8bf5c-217">在應用程式清單中，選取 [Expensify] 。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-217">In the applications list, select **Expensify**.</span></span>

    ![設定單一登入](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="8bf5c-219">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-219">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8bf5c-221">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-221">Click **Add** button.</span></span> <span data-ttu-id="8bf5c-222">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8bf5c-224">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8bf5c-225">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8bf5c-226">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8bf5c-227">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8bf5c-227">Testing single sign-on</span></span>

<span data-ttu-id="8bf5c-228">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="8bf5c-229">當您在「存取面板」中按一下 [Expensify] 圖格時，應該會自動登入您的 Expensify 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8bf5c-229">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8bf5c-230">其他資源</span><span class="sxs-lookup"><span data-stu-id="8bf5c-230">Additional resources</span></span>

* [<span data-ttu-id="8bf5c-231">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="8bf5c-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8bf5c-232">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8bf5c-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

