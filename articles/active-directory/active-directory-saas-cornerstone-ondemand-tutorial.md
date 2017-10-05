---
title: "教學課程：Azure Active Directory 與 Cornerstone OnDemand 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Cornerstone OnDemand 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 8bb32588579a0d40b9ae7e0f823c6daab21c856e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="9cd63-103">教學課程：Azure Active Directory 與 Cornerstone OnDemand 整合</span><span class="sxs-lookup"><span data-stu-id="9cd63-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="9cd63-104">在本教學課程中，您將了解如何整合 Cornerstone OnDemand 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9cd63-104">In this tutorial, you learn how to integrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9cd63-105">Cornerstone OnDemand 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="9cd63-105">Integrating Cornerstone OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9cd63-106">您可以在 Azure AD 中控制可存取 Cornerstone OnDemand 的人員</span><span class="sxs-lookup"><span data-stu-id="9cd63-106">You can control in Azure AD who has access to Cornerstone OnDemand</span></span>
- <span data-ttu-id="9cd63-107">您可以讓使用者利用自己的 Azure AD 帳戶，來自動登入 Cornerstone OnDemand (單一登入)</span><span class="sxs-lookup"><span data-stu-id="9cd63-107">You can enable your users to automatically get signed-on to Cornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9cd63-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="9cd63-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9cd63-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9cd63-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cd63-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9cd63-110">Prerequisites</span></span>

<span data-ttu-id="9cd63-111">若要設定 Azure AD 與 Cornerstone OnDemand 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="9cd63-111">To configure Azure AD integration with Cornerstone OnDemand, you need the following items:</span></span>

- <span data-ttu-id="9cd63-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9cd63-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9cd63-113">已啟用 Cornerstone OnDemand 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9cd63-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9cd63-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9cd63-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9cd63-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9cd63-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9cd63-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9cd63-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9cd63-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="9cd63-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9cd63-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9cd63-118">Scenario description</span></span>
<span data-ttu-id="9cd63-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cd63-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9cd63-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="9cd63-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9cd63-121">從資源庫新增 Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="9cd63-121">Adding Cornerstone OnDemand from the gallery</span></span>
2. <span data-ttu-id="9cd63-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9cd63-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-the-gallery"></a><span data-ttu-id="9cd63-123">從資源庫新增 Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="9cd63-123">Adding Cornerstone OnDemand from the gallery</span></span>
<span data-ttu-id="9cd63-124">若要設定將 Cornerstone OnDemand 整合到 Azure AD 中，您需要從資源庫將 Cornerstone OnDemand 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="9cd63-124">To configure the integration of Cornerstone OnDemand into Azure AD, you need to add Cornerstone OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9cd63-125">**若要從資源庫新增 Cornerstone OnDemand，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9cd63-125">**To add Cornerstone OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9cd63-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9cd63-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9cd63-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9cd63-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="9cd63-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cd63-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="9cd63-133">在搜尋方塊中，輸入 **Cornerstone OnDemand**。</span><span class="sxs-lookup"><span data-stu-id="9cd63-133">In the search box, type **Cornerstone OnDemand**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="9cd63-135">在結果窗格中，選取 [Cornerstone OnDemand]，然後按一下 [新增] 按鈕來新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cd63-135">In the results panel, select **Cornerstone OnDemand**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9cd63-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9cd63-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9cd63-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Cornerstone OnDemand 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cd63-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9cd63-139">若要讓單一登入運作，Azure AD 必須知道 Cornerstone OnDemand 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="9cd63-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cornerstone OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="9cd63-140">換句話說，必須建立 Azure AD 使用者和 Cornerstone OnDemand 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9cd63-140">In other words, a link relationship between an Azure AD user and the related user in Cornerstone OnDemand needs to be established.</span></span>

<span data-ttu-id="9cd63-141">在 Cornerstone OnDemand 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9cd63-141">In Cornerstone OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9cd63-142">若要設定及測試與 Cornerstone OnDemand 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="9cd63-142">To configure and test Azure AD single sign-on with Cornerstone OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9cd63-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="9cd63-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9cd63-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cd63-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9cd63-145">**[建立 Cornerstone OnDemand 測試使用者](#creating-a-cornerstone-ondemand-test-user)** - 在 Cornerstone OnDemand 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="9cd63-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - to have a counterpart of Britta Simon in Cornerstone OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9cd63-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cd63-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9cd63-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="9cd63-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9cd63-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9cd63-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9cd63-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Cornerstone OnDemand 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cd63-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="9cd63-150">**若要使用 Cornerstone OnDemand 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9cd63-150">**To configure Azure AD single sign-on with Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="9cd63-151">在 Azure 入口網站的 [Cornerstone OnDemand] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-151">In the Azure portal, on the **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9cd63-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cd63-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="9cd63-155">在 [Cornerstone OnDemand 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9cd63-155">On the **Cornerstone OnDemand Domain and URLs** section, perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="9cd63-157">a.</span><span class="sxs-lookup"><span data-stu-id="9cd63-157">a.</span></span> <span data-ttu-id="9cd63-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="9cd63-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="9cd63-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cd63-159">b.</span></span> <span data-ttu-id="9cd63-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="9cd63-160">In **Identifier** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9cd63-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9cd63-161">These values are not real.</span></span> <span data-ttu-id="9cd63-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="9cd63-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9cd63-163">請連絡 [Cornerstone OnDemand 用戶端支援小組](mailTo:moreinfo@csod.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="9cd63-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) to get these values.</span></span> 
 
4. <span data-ttu-id="9cd63-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9cd63-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="9cd63-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cd63-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9cd63-168">在 [Cornerstone OnDemand 設定] 區段中，按一下 [設定 Cornerstone OnDemand] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9cd63-168">On the **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9cd63-169">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="9cd63-171">若要在 **Cornerstone OnDemand** 端設定單一登入，您必須將下載的 [憑證]、[登出 URL] 和 [SAML 單一登入服務 URL] 傳送至 [Cornerstone OnDemand 支援小組](mailTo:moreinfo@csod.com)。</span><span class="sxs-lookup"><span data-stu-id="9cd63-171">To configure single sign-on on **Cornerstone OnDemand** side, you need to send the downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  to [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="9cd63-172">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="9cd63-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9cd63-173">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="9cd63-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9cd63-174">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="9cd63-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9cd63-175">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9cd63-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9cd63-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9cd63-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="9cd63-177">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9cd63-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="9cd63-179">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9cd63-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9cd63-180">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9cd63-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9cd63-182">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9cd63-184">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9cd63-186">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9cd63-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9cd63-188">a.</span><span class="sxs-lookup"><span data-stu-id="9cd63-188">a.</span></span> <span data-ttu-id="9cd63-189">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9cd63-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9cd63-190">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cd63-190">b.</span></span> <span data-ttu-id="9cd63-191">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="9cd63-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9cd63-192">c.</span><span class="sxs-lookup"><span data-stu-id="9cd63-192">c.</span></span> <span data-ttu-id="9cd63-193">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="9cd63-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9cd63-194">d.</span><span class="sxs-lookup"><span data-stu-id="9cd63-194">d.</span></span> <span data-ttu-id="9cd63-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9cd63-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="9cd63-196">建立 Cornerstone OnDemand 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9cd63-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="9cd63-197">若要讓 Azure AD 使用者可以登入 Cornerstone OnDemand，則必須將他們佈建到 Cornerstone OnDemand。</span><span class="sxs-lookup"><span data-stu-id="9cd63-197">In order to enable Azure AD users to log into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="9cd63-198">Cornerstone OnDemand 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="9cd63-198">In the case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="9cd63-199">若要設定使用者佈建，請將您想要佈建的 Azure AD 使用者資訊 (例如姓名、電子郵件) 傳送給 [Cornerstone OnDemand 支援小組](mailTo:moreinfo@csod.com)。</span><span class="sxs-lookup"><span data-stu-id="9cd63-199">To configure user provisioning, send the information (e.g.: Name, Email) about the Azure AD user you want to provision to the [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="9cd63-200">您可以使用任何其他的 Cornerstone OnDemand 使用者帳戶建立工具或 Cornerstone OnDemand 所提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="9cd63-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9cd63-201">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9cd63-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9cd63-202">在本節中，您會將 Cornerstone OnDemand 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9cd63-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cornerstone OnDemand.</span></span>

![指派使用者][200] 

<span data-ttu-id="9cd63-204">**若要將 Britta Simon 指派給 Cornerstone OnDemand，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9cd63-204">**To assign Britta Simon to Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="9cd63-205">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9cd63-207">在應用程式清單中，選取 **Cornerstone OnDemand**。</span><span class="sxs-lookup"><span data-stu-id="9cd63-207">In the applications list, select **Cornerstone OnDemand**.</span></span>

    ![設定單一登入](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="9cd63-209">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-209">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="9cd63-211">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cd63-211">Click **Add** button.</span></span> <span data-ttu-id="9cd63-212">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="9cd63-214">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="9cd63-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9cd63-215">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cd63-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9cd63-216">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9cd63-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9cd63-217">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9cd63-217">Testing single sign-on</span></span>

<span data-ttu-id="9cd63-218">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="9cd63-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9cd63-219">當您在存取面板中按一下 [Cornerstone OnDemand] 圖格時，應該會自動登入您的 Cornerstone OnDemand 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9cd63-219">When you click the Cornerstone OnDemand tile in the Access Panel, you should get automatically signed-on to your Cornerstone OnDemand application.</span></span>
<span data-ttu-id="9cd63-220">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="9cd63-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9cd63-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="9cd63-221">Additional resources</span></span>

* [<span data-ttu-id="9cd63-222">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="9cd63-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9cd63-223">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9cd63-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png

