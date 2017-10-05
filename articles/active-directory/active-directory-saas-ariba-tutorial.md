---
title: "教學課程：Azure Active Directory 與 Ariba 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Ariba 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 214367847055ba38ee03a28d0afdcc58f68333cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="f5fd5-103">教學課程：Azure Active Directory 與 Ariba 整合</span><span class="sxs-lookup"><span data-stu-id="f5fd5-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="f5fd5-104">在本教學課程中，您會了解如何將 Ariba 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-104">In this tutorial, you learn how to integrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5fd5-105">將 Ariba 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f5fd5-105">Integrating Ariba with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5fd5-106">您可以在 Azure AD 中控制可存取 Ariba 的人員</span><span class="sxs-lookup"><span data-stu-id="f5fd5-106">You can control in Azure AD who has access to Ariba</span></span>
- <span data-ttu-id="f5fd5-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Ariba (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f5fd5-107">You can enable your users to automatically get signed-on to Ariba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f5fd5-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f5fd5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f5fd5-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5fd5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f5fd5-110">Prerequisites</span></span>

<span data-ttu-id="f5fd5-111">若要設定與 Ariba 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f5fd5-111">To configure Azure AD integration with Ariba, you need the following items:</span></span>

- <span data-ttu-id="f5fd5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f5fd5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5fd5-113">已啟用 Ariba 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f5fd5-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5fd5-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5fd5-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f5fd5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5fd5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5fd5-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5fd5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f5fd5-118">Scenario description</span></span>
<span data-ttu-id="f5fd5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5fd5-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f5fd5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5fd5-121">從資源庫新增 Ariba</span><span class="sxs-lookup"><span data-stu-id="f5fd5-121">Adding Ariba from the gallery</span></span>
2. <span data-ttu-id="f5fd5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f5fd5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-the-gallery"></a><span data-ttu-id="f5fd5-123">從資源庫新增 Ariba</span><span class="sxs-lookup"><span data-stu-id="f5fd5-123">Adding Ariba from the gallery</span></span>
<span data-ttu-id="f5fd5-124">若要設定將 Ariba 整合到 Azure AD 中，您需要從資源庫將 Ariba 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5fd5-125">**若要從資源庫加入 Ariba，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f5fd5-125">**To add Ariba from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5fd5-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f5fd5-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5fd5-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f5fd5-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f5fd5-133">在搜尋方塊中，輸入 **Ariba**。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-133">In the search box, type **Ariba**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="f5fd5-135">在結果面板中，選取 [Ariba]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-135">In the results panel, select **Ariba**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f5fd5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f5fd5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f5fd5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Ariba 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f5fd5-139">若要讓單一登入能夠運作，Azure AD 必須知道 Ariba 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Ariba is to a user in Azure AD.</span></span> <span data-ttu-id="f5fd5-140">換句話說，必須在 Azure AD 使用者和 Ariba 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-140">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span></span>

<span data-ttu-id="f5fd5-141">在 Ariba 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-141">In Ariba, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f5fd5-142">若要設定及測試與 Ariba 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="f5fd5-142">To configure and test Azure AD single sign-on with Ariba, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5fd5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f5fd5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f5fd5-145">**[建立 Ariba 測試使用者](#creating-an-ariba-test-user)** - 在 Ariba 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f5fd5-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f5fd5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f5fd5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f5fd5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f5fd5-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Ariba 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="f5fd5-150">**若要設定與 Ariba 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f5fd5-150">**To configure Azure AD single sign-on with Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="f5fd5-151">在 Azure 入口網站的 [Ariba] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-151">In the Azure portal, on the **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f5fd5-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="f5fd5-155">在 [Ariba 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f5fd5-155">On the **Ariba Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="f5fd5-157">a.</span><span class="sxs-lookup"><span data-stu-id="f5fd5-157">a.</span></span> <span data-ttu-id="f5fd5-158">在 [登入 URL] 文字方塊中，使用下列模式來輸入 URL：`https://<subdomain>.sourcing.ariba.com` 或 `https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="f5fd5-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="f5fd5-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-159">b.</span></span> <span data-ttu-id="f5fd5-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="f5fd5-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5fd5-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-161">These values are not real.</span></span> <span data-ttu-id="f5fd5-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f5fd5-163">在此建議您在 [識別碼] 中使用唯一的字串值。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="f5fd5-164">請連絡 Ariba 用戶端支援小組 (電話號碼為 **1-866-218-2155**) 以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-164">Contact Ariba Client support team at **1-866-218-2155** to get these values.</span></span> 
 

4. <span data-ttu-id="f5fd5-165">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate  file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="f5fd5-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f5fd5-169">若要為您的應用程式設定 SSO，請撥打電話 (**1-866-218-2155**) 給 Ariba 支援小組，他們將會進一步協助您將所下載的「憑證 (Base64)」檔案提供給他們。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-169">To get SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how to provide them the downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="f5fd5-170">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="f5fd5-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f5fd5-171">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f5fd5-172">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f5fd5-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f5fd5-173">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f5fd5-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="f5fd5-174">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f5fd5-176">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f5fd5-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5fd5-177">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f5fd5-179">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f5fd5-181">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f5fd5-183">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f5fd5-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f5fd5-185">a.</span><span class="sxs-lookup"><span data-stu-id="f5fd5-185">a.</span></span> <span data-ttu-id="f5fd5-186">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5fd5-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-187">b.</span></span> <span data-ttu-id="f5fd5-188">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f5fd5-189">c.</span><span class="sxs-lookup"><span data-stu-id="f5fd5-189">c.</span></span> <span data-ttu-id="f5fd5-190">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f5fd5-191">d.</span><span class="sxs-lookup"><span data-stu-id="f5fd5-191">d.</span></span> <span data-ttu-id="f5fd5-192">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="f5fd5-193">建立 Ariba 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f5fd5-193">Creating an Ariba test user</span></span>

<span data-ttu-id="f5fd5-194">本節的目標是要在 Ariba 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-194">The objective of this section is to create a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="f5fd5-195">請與 Ariba 支援小組 (電話號碼為 **1-866-218-2155**) 合作，在 Ariba 系統中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-195">Work with Ariba support team at **1-866-218-2155** to add the users in the Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="f5fd5-196">如果您需要手動建立使用者，則必須連絡 Ariba 支援小組 (電話號碼為 **1-866-218-2155**)。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-196">If you need to create a user manually, you need to contact the Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f5fd5-197">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f5fd5-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f5fd5-198">在本節中，您會將 Ariba 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ariba.</span></span>

![指派使用者][200] 

<span data-ttu-id="f5fd5-200">**若要將 Britta Simon 指派給 Ariba，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f5fd5-200">**To assign Britta Simon to Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="f5fd5-201">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f5fd5-203">在應用程式清單中，選取 [Ariba]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-203">In the applications list, select **Ariba**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="f5fd5-205">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-205">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f5fd5-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-207">Click **Add** button.</span></span> <span data-ttu-id="f5fd5-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f5fd5-210">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f5fd5-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f5fd5-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f5fd5-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f5fd5-213">Testing single sign-on</span></span>
<span data-ttu-id="f5fd5-214">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f5fd5-215">當您在「存取面板」中按一下 Ariba 磚時，應該會自動登入您的 Ariba 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5fd5-215">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f5fd5-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="f5fd5-216">Additional resources</span></span>

* [<span data-ttu-id="f5fd5-217">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f5fd5-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f5fd5-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f5fd5-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

