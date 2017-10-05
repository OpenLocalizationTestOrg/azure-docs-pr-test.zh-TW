---
title: "教學課程：Azure Active Directory 與 Nexonia 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Nexonia 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 1370fa64c2ddc25d3121c567ceea4828b1e50921
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="5ba8a-103">教學課程：Azure Active Directory 與 Nexonia 整合</span><span class="sxs-lookup"><span data-stu-id="5ba8a-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="5ba8a-104">在本教學課程中，您會了解如何整合 Nexonia 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-104">In this tutorial, you learn how to integrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ba8a-105">Nexonia 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="5ba8a-105">Integrating Nexonia with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5ba8a-106">您可以在 Azure AD 中控制可存取 Nexonia 的人員</span><span class="sxs-lookup"><span data-stu-id="5ba8a-106">You can control in Azure AD who has access to Nexonia</span></span>
- <span data-ttu-id="5ba8a-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Nexonia (單一登入)</span><span class="sxs-lookup"><span data-stu-id="5ba8a-107">You can enable your users to automatically get signed-on to Nexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ba8a-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5ba8a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5ba8a-109">如果您想要知道與 Azure AD 整合的 SaaS 應用程式詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5ba8a-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="5ba8a-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ba8a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="5ba8a-111">Prerequisites</span></span>

<span data-ttu-id="5ba8a-112">若要設定與 Nexonia 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5ba8a-112">To configure Azure AD integration with Nexonia, you need the following items:</span></span>

- <span data-ttu-id="5ba8a-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5ba8a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="5ba8a-114">已啟用 Nexonia 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5ba8a-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ba8a-115">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ba8a-116">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5ba8a-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ba8a-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ba8a-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ba8a-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="5ba8a-119">Scenario description</span></span>
<span data-ttu-id="5ba8a-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ba8a-121">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5ba8a-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ba8a-122">從資源庫新增 Nexonia</span><span class="sxs-lookup"><span data-stu-id="5ba8a-122">Adding Nexonia from the gallery</span></span>
2. <span data-ttu-id="5ba8a-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5ba8a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-the-gallery"></a><span data-ttu-id="5ba8a-124">從資源庫新增 Nexonia</span><span class="sxs-lookup"><span data-stu-id="5ba8a-124">Adding Nexonia from the gallery</span></span>
<span data-ttu-id="5ba8a-125">若要設定 Nexonia 與 Azure AD 整合，您需要從資源庫將 Nexonia 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-125">To configure the integration of Nexonia into Azure AD, you need to add Nexonia from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5ba8a-126">**若要從資源庫新增 Nexonia，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5ba8a-126">**To add Nexonia from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5ba8a-127">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ba8a-129">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5ba8a-130">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-130">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5ba8a-132">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5ba8a-134">在搜尋方塊中，輸入 **Nexonia**。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-134">In the search box, type **Nexonia**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="5ba8a-136">在結果窗格中，選取 [Nexonia]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-136">In the results panel, select **Nexonia**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ba8a-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5ba8a-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ba8a-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Nexonia 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5ba8a-140">若要讓單一登入運作，Azure AD 必須知道 Nexonia 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Nexonia is to a user in Azure AD.</span></span> <span data-ttu-id="5ba8a-141">換句話說，必須建立 Azure AD 使用者和 Nexonia 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-141">In other words, a link relationship between an Azure AD user and the related user in Nexonia needs to be established.</span></span>

<span data-ttu-id="5ba8a-142">在 Nexonia 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-142">In Nexonia, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5ba8a-143">若要設定及測試與 Nexonia 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="5ba8a-143">To configure and test Azure AD single sign-on with Nexonia, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5ba8a-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5ba8a-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ba8a-146">**[建立 Nexonia 測試使用者](#creating-a-nexonia-test-user)** - 使 Nexonia 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - to have a counterpart of Britta Simon in Nexonia that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ba8a-147">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ba8a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ba8a-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5ba8a-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ba8a-150">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Nexonia 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="5ba8a-151">如果您在整合時遇到問題，請參閱此[連結](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting)以取得疑難排解指南。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-151">If you have issues in the integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="5ba8a-152">如果仍找不到解決方案，請從 Azure 入口網站提出支援要求。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-152">If you still have not found the solution, then raise the support request from Azure portal.</span></span>

<span data-ttu-id="5ba8a-153">**若要設定與 Nexonia 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5ba8a-153">**To configure Azure AD single sign-on with Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="5ba8a-154">在 Azure 入口網站的 [Nexonia] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-154">In the Azure portal, on the **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5ba8a-156">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-156">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="5ba8a-158">在 [Nexonia 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5ba8a-158">On the **Nexonia Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="5ba8a-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="5ba8a-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5ba8a-161">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-161">This value is not real.</span></span> <span data-ttu-id="5ba8a-162">請使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-162">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="5ba8a-163">請連絡 [Nexonia 支援小組](https://nexonia.zendesk.com/hc/requests/new)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to get this value.</span></span> 


4. <span data-ttu-id="5ba8a-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="5ba8a-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5ba8a-168">在 [Nexonia 組態] 區段上，按一下 [設定 Nexonia] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-168">On the **Nexonia Configuration** section, click **Configure Nexonia** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5ba8a-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="5ba8a-171">若要為您的應用程式設定 SSO，請連絡 [Nexonia 支援小組](https://nexonia.zendesk.com/hc/requests/new)，並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba8a-171">To get SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with the following:</span></span>

    <span data-ttu-id="5ba8a-172">• 下載的 **憑證**</span><span class="sxs-lookup"><span data-stu-id="5ba8a-172">• The downloaded **certificate**</span></span>

    <span data-ttu-id="5ba8a-173">• **SAML 實體識別碼**</span><span class="sxs-lookup"><span data-stu-id="5ba8a-173">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="5ba8a-174">• **SAML 單一登入服務 URL**</span><span class="sxs-lookup"><span data-stu-id="5ba8a-174">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="5ba8a-175">• **登出 URL**</span><span class="sxs-lookup"><span data-stu-id="5ba8a-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="5ba8a-176">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="5ba8a-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5ba8a-177">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5ba8a-178">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5ba8a-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ba8a-179">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5ba8a-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ba8a-180">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5ba8a-182">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5ba8a-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5ba8a-183">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ba8a-185">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ba8a-187">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ba8a-189">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5ba8a-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ba8a-191">a.</span><span class="sxs-lookup"><span data-stu-id="5ba8a-191">a.</span></span> <span data-ttu-id="5ba8a-192">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ba8a-193">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-193">b.</span></span> <span data-ttu-id="5ba8a-194">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ba8a-195">c.</span><span class="sxs-lookup"><span data-stu-id="5ba8a-195">c.</span></span> <span data-ttu-id="5ba8a-196">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5ba8a-197">d.</span><span class="sxs-lookup"><span data-stu-id="5ba8a-197">d.</span></span> <span data-ttu-id="5ba8a-198">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="5ba8a-199">建立 Nexonia 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5ba8a-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="5ba8a-200">在本節中，您要在 Nexonia 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="5ba8a-201">請與 [Nexonia 支援小組](https://nexonia.zendesk.com/hc/requests/new)合作，在 Nexonia 平台中加入使用者。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) to add the users in the Nexonia platform.</span></span> <span data-ttu-id="5ba8a-202">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5ba8a-203">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5ba8a-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5ba8a-204">在本節中，您會將 Nexonia 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Nexonia.</span></span>

![指派使用者][200] 

<span data-ttu-id="5ba8a-206">**若要將 Britta Simon 指派給 Nexonia，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5ba8a-206">**To assign Britta Simon to Nexonia, perform the following steps:**</span></span>

1. <span data-ttu-id="5ba8a-207">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5ba8a-209">在應用程式清單中，選取 [Nexonia]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-209">In the applications list, select **Nexonia**.</span></span>

    ![設定單一登入](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="5ba8a-211">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-211">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5ba8a-213">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-213">Click **Add** button.</span></span> <span data-ttu-id="5ba8a-214">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5ba8a-216">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5ba8a-217">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ba8a-218">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ba8a-219">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5ba8a-219">Testing single sign-on</span></span>

<span data-ttu-id="5ba8a-220">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5ba8a-221">當您在「存取面板」中按一下 Nexonia 圖格時，應該會自動登入您的 Nexonia 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-221">When you click the Nexonia tile in the Access Panel, you should get automatically signed-on to your Nexonia application.</span></span>
<span data-ttu-id="5ba8a-222">如需存取面板的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="5ba8a-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ba8a-223">其他資源</span><span class="sxs-lookup"><span data-stu-id="5ba8a-223">Additional resources</span></span>

* [<span data-ttu-id="5ba8a-224">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5ba8a-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ba8a-225">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5ba8a-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

