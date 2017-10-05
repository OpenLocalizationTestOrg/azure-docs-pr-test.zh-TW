---
title: "教學課程：Azure Active Directory 與 Canvas LMS 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Canvas LMS 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 2212b7a81b66d1afd1aa78d1487b07b6d7b84129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="14003-103">教學課程：Azure Active Directory 與 Canvas LMS 整合</span><span class="sxs-lookup"><span data-stu-id="14003-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="14003-104">在本教學課程中，您會了解如何將 Canvas 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="14003-104">In this tutorial, you learn how to integrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="14003-105">將 Canvas 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="14003-105">Integrating Canvas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="14003-106">您可以在 Azure AD 中控制可存取 Canvas 的人員</span><span class="sxs-lookup"><span data-stu-id="14003-106">You can control in Azure AD who has access to Canvas</span></span>
- <span data-ttu-id="14003-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Canvas (單一登入)</span><span class="sxs-lookup"><span data-stu-id="14003-107">You can enable your users to automatically get signed-on to Canvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="14003-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="14003-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="14003-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="14003-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14003-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="14003-110">Prerequisites</span></span>

<span data-ttu-id="14003-111">若要設定 Azure AD 與 Canvas 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="14003-111">To configure Azure AD integration with Canvas, you need the following items:</span></span>

- <span data-ttu-id="14003-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="14003-112">An Azure AD subscription</span></span>
- <span data-ttu-id="14003-113">已啟用 Canvas 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="14003-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="14003-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="14003-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="14003-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="14003-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="14003-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="14003-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="14003-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="14003-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="14003-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="14003-118">Scenario description</span></span>
<span data-ttu-id="14003-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="14003-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="14003-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="14003-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="14003-121">從資源庫新增 Canvas</span><span class="sxs-lookup"><span data-stu-id="14003-121">Adding Canvas from the gallery</span></span>
2. <span data-ttu-id="14003-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="14003-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-the-gallery"></a><span data-ttu-id="14003-123">從資源庫新增 Canvas</span><span class="sxs-lookup"><span data-stu-id="14003-123">Adding Canvas from the gallery</span></span>
<span data-ttu-id="14003-124">若要設定將 Canvas 整合到 Azure AD 中，您需要從資源庫將 Canvas 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="14003-124">To configure the integration of Canvas into Azure AD, you need to add Canvas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="14003-125">**若要從資源庫新增 Canvas，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="14003-125">**To add Canvas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="14003-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="14003-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="14003-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="14003-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="14003-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="14003-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="14003-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="14003-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="14003-133">在搜尋方塊中，輸入 **Canvas**。</span><span class="sxs-lookup"><span data-stu-id="14003-133">In the search box, type **Canvas**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="14003-135">在結果面板中，選取 [Canvas]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="14003-135">In the results panel, select **Canvas**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="14003-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="14003-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="14003-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Canvas 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="14003-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="14003-139">若要讓單一登入能夠運作，Azure AD 必須知道 Canvas 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="14003-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Canvas is to a user in Azure AD.</span></span> <span data-ttu-id="14003-140">換句話說，必須在 Azure AD 使用者與 Canvas 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="14003-140">In other words, a link relationship between an Azure AD user and the related user in Canvas needs to be established.</span></span>

<span data-ttu-id="14003-141">在 Canvas 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="14003-141">In Canvas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="14003-142">若要設定及測試與 Canvas 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="14003-142">To configure and test Azure AD single sign-on with Canvas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="14003-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="14003-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="14003-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="14003-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="14003-145">**[建立 Canvas 測試使用者](#creating-a-canvas-test-user)** - 在 Canvas 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="14003-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - to have a counterpart of Britta Simon in Canvas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="14003-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="14003-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="14003-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="14003-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="14003-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="14003-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="14003-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Canvas 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="14003-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="14003-150">**若要設定與 Canvas 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="14003-150">**To configure Azure AD single sign-on with Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="14003-151">在 Azure 入口網站的 [Canvas] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="14003-151">In the Azure portal, on the **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="14003-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="14003-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="14003-155">在 [Canvas 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="14003-155">On the **Canvas Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="14003-157">a.</span><span class="sxs-lookup"><span data-stu-id="14003-157">a.</span></span> <span data-ttu-id="14003-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="14003-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="14003-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="14003-159">b.</span></span> <span data-ttu-id="14003-160">在 [識別碼] 文字方塊中，使用下列模式將值輸入：`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="14003-160">In the **Identifier** textbox, type the value using the following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="14003-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="14003-161">These values are not real.</span></span> <span data-ttu-id="14003-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="14003-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="14003-163">請連絡 [Canvas 用戶端支援小組](https://community.canvaslms.com/community/help)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="14003-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="14003-164">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="14003-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="14003-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="14003-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="14003-168">在 [Canvas 組態] 區段上，按一下 [設定 Canvas] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="14003-168">On the **Canvas Configuration** section, click **Configure Canvas** to open **Configure sign-on** window.</span></span> <span data-ttu-id="14003-169">從 [快速參考] 區段中複製「變更密碼 URL」、「登出 URL」、「SAML 實體識別碼」及「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="14003-169">Copy the **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="14003-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Canvas 公司網站。</span><span class="sxs-lookup"><span data-stu-id="14003-171">In a different web browser window, log in to your Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="14003-172">移至 [課程] \> [受管理帳戶] \> [Microsoft]。</span><span class="sxs-lookup"><span data-stu-id="14003-172">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="14003-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="14003-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="14003-174">在左側瀏覽窗格中，選取 [驗證]，然後按一下 [加入新的 SAML 設定]。</span><span class="sxs-lookup"><span data-stu-id="14003-174">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="14003-175">![驗證](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "驗證")</span><span class="sxs-lookup"><span data-stu-id="14003-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="14003-176">在 [目前的整合] 頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="14003-176">On the Current Integration page, perform the following steps:</span></span>
   
    <span data-ttu-id="14003-177">![目前的整合](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "目前的整合")</span><span class="sxs-lookup"><span data-stu-id="14003-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="14003-178">a.</span><span class="sxs-lookup"><span data-stu-id="14003-178">a.</span></span> <span data-ttu-id="14003-179">在 [IdP 實體識別碼] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="14003-179">In **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="14003-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="14003-180">b.</span></span> <span data-ttu-id="14003-181">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="14003-181">In **Log On URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="14003-182">c.</span><span class="sxs-lookup"><span data-stu-id="14003-182">c.</span></span> <span data-ttu-id="14003-183">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="14003-183">In **Log Out URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="14003-184">d.</span><span class="sxs-lookup"><span data-stu-id="14003-184">d.</span></span> <span data-ttu-id="14003-185">在 [變更密碼連結] 文字方塊中，貼上您從 Azure 入口網站複製的 [變更密碼 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="14003-185">In **Change Password Link** textbox, paste the value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="14003-186">e.</span><span class="sxs-lookup"><span data-stu-id="14003-186">e.</span></span> <span data-ttu-id="14003-187">在 [憑證指紋] 文字方塊中，貼上您從 Azure 入口網站複製的憑證 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="14003-187">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="14003-188">f.</span><span class="sxs-lookup"><span data-stu-id="14003-188">f.</span></span> <span data-ttu-id="14003-189">從 [登入屬性] 清單中選取 [NameID]。</span><span class="sxs-lookup"><span data-stu-id="14003-189">From the **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="14003-190">g.</span><span class="sxs-lookup"><span data-stu-id="14003-190">g.</span></span> <span data-ttu-id="14003-191">從 [識別碼格式] 清單中選取 [emailAddress]。</span><span class="sxs-lookup"><span data-stu-id="14003-191">From the **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="14003-192">h.</span><span class="sxs-lookup"><span data-stu-id="14003-192">h.</span></span> <span data-ttu-id="14003-193">按一下 [儲存驗證設定] 。</span><span class="sxs-lookup"><span data-stu-id="14003-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="14003-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="14003-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="14003-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="14003-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="14003-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="14003-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="14003-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="14003-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="14003-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="14003-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="14003-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="14003-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="14003-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="14003-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="14003-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="14003-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="14003-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="14003-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="14003-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="14003-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="14003-209">a.</span><span class="sxs-lookup"><span data-stu-id="14003-209">a.</span></span> <span data-ttu-id="14003-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="14003-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="14003-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="14003-211">b.</span></span> <span data-ttu-id="14003-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="14003-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="14003-213">c.</span><span class="sxs-lookup"><span data-stu-id="14003-213">c.</span></span> <span data-ttu-id="14003-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="14003-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="14003-215">d.</span><span class="sxs-lookup"><span data-stu-id="14003-215">d.</span></span> <span data-ttu-id="14003-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="14003-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="14003-217">建立 Canvas 測試使用者</span><span class="sxs-lookup"><span data-stu-id="14003-217">Creating a Canvas test user</span></span>

<span data-ttu-id="14003-218">若要讓 Azure AD 使用者能夠登入 Canvas，必須將他們佈建到 Canvas。</span><span class="sxs-lookup"><span data-stu-id="14003-218">To enable Azure AD users to log in to Canvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="14003-219">就 Canvas 而言，需以手動方式佈建使用者。</span><span class="sxs-lookup"><span data-stu-id="14003-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="14003-220">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="14003-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="14003-221">登入您的 **Canvas** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="14003-221">Log in to your **Canvas** tenant.</span></span>

2. <span data-ttu-id="14003-222">移至 [課程] \> [受管理帳戶] \> [Microsoft]。</span><span class="sxs-lookup"><span data-stu-id="14003-222">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="14003-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="14003-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="14003-224">按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="14003-224">Click **Users**.</span></span>
   
   <span data-ttu-id="14003-225">![使用者](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="14003-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="14003-226">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="14003-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="14003-227">![使用者](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="14003-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="14003-228">在 [新增使用者] 對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="14003-228">On the Add a New User dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="14003-229">![新增使用者](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="14003-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="14003-230">a.</span><span class="sxs-lookup"><span data-stu-id="14003-230">a.</span></span> <span data-ttu-id="14003-231">在 [全名] 文字方塊中，輸入使用者的名稱，例如 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="14003-231">In the **Full Name** textbox, enter the name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="14003-232">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="14003-232">b.</span></span> <span data-ttu-id="14003-233">在 [電子郵件] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="14003-233">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="14003-234">c.</span><span class="sxs-lookup"><span data-stu-id="14003-234">c.</span></span> <span data-ttu-id="14003-235">在 [登入] 文字方塊中，輸入使用者的 Azure AD 電子郵件地址，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="14003-235">In the **Login** textbox, enter the user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="14003-236">d.</span><span class="sxs-lookup"><span data-stu-id="14003-236">d.</span></span> <span data-ttu-id="14003-237">選取 [以電子郵件通知使用者有關這個帳戶的建立] 。</span><span class="sxs-lookup"><span data-stu-id="14003-237">Select **Email the user about this account creation**.</span></span>

   <span data-ttu-id="14003-238">e.</span><span class="sxs-lookup"><span data-stu-id="14003-238">e.</span></span> <span data-ttu-id="14003-239">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="14003-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="14003-240">您可以使用任何其他的 Canvas 使用者帳戶建立工具或 Canvas 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="14003-240">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="14003-241">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="14003-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="14003-242">在本節中，您會將 Canvas 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="14003-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Canvas.</span></span>

![指派使用者][200] 

<span data-ttu-id="14003-244">**若要將 Britta Simon 指派給 Canvas，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="14003-244">**To assign Britta Simon to Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="14003-245">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="14003-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="14003-247">在應用程式清單中，選取 [Canvas]。</span><span class="sxs-lookup"><span data-stu-id="14003-247">In the applications list, select **Canvas**.</span></span>

    ![設定單一登入](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="14003-249">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="14003-249">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="14003-251">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="14003-251">Click **Add** button.</span></span> <span data-ttu-id="14003-252">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="14003-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="14003-254">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="14003-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="14003-255">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="14003-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="14003-256">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="14003-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="14003-257">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="14003-257">Testing single sign-on</span></span>

<span data-ttu-id="14003-258">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="14003-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="14003-259">當您在「存取面板」中按一下 [Canvas] 圖格時，應該會自動登入您的 Canvas 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14003-259">When you click the Canvas tile in the Access Panel, you should get automatically signed-on to your Canvas application.</span></span>
<span data-ttu-id="14003-260">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="14003-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="14003-261">其他資源</span><span class="sxs-lookup"><span data-stu-id="14003-261">Additional resources</span></span>

* [<span data-ttu-id="14003-262">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="14003-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="14003-263">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="14003-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

