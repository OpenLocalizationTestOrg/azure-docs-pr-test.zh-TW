---
title: "教學課程：Azure Active Directory 與 Humanity 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Humanity 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="5c292-103">教學課程：Azure Active Directory 與 Humanity 整合</span><span class="sxs-lookup"><span data-stu-id="5c292-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="5c292-104">在本教學課程中，您將了解如何整合 Humanity 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5c292-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c292-105">將 Humanity 與 Azure AD 整合有下列優點：</span><span class="sxs-lookup"><span data-stu-id="5c292-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c292-106">您可以在 Azure AD 中控制可存取 Humanity 的人員</span><span class="sxs-lookup"><span data-stu-id="5c292-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="5c292-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 Humanity (單一登入)</span><span class="sxs-lookup"><span data-stu-id="5c292-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c292-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5c292-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c292-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5c292-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c292-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c292-110">Prerequisites</span></span>

<span data-ttu-id="5c292-111">若要進行 Azure AD 與 Humanity 整合的設定，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5c292-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="5c292-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5c292-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c292-113">已啟用 Humanity 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5c292-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c292-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5c292-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c292-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5c292-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c292-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5c292-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c292-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5c292-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c292-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5c292-118">Scenario description</span></span>
<span data-ttu-id="5c292-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c292-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c292-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5c292-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c292-121">從資源庫新增 Humanity</span><span class="sxs-lookup"><span data-stu-id="5c292-121">Adding Humanity from the gallery</span></span>
2. <span data-ttu-id="5c292-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5c292-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="5c292-123">從資源庫新增 Humanity</span><span class="sxs-lookup"><span data-stu-id="5c292-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="5c292-124">若要進行 Humanity 與 Azure AD 整合的設定，您需要從資源庫將 Humanity 新增到受管理 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="5c292-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c292-125">**若要從資源庫新增 Humanity，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5c292-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c292-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5c292-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c292-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5c292-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c292-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5c292-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5c292-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c292-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5c292-133">在搜尋方塊中，輸入 **Humanity**。</span><span class="sxs-lookup"><span data-stu-id="5c292-133">In the search box, type **Humanity**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="5c292-135">在結果面板中，選取 [Humanity]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c292-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c292-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5c292-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c292-138">在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Humanity 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c292-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c292-139">為了讓單一登入正常運作，Azure AD 必須知道 Azure AD 使用者在 Humanity 中的對應使用者是誰。</span><span class="sxs-lookup"><span data-stu-id="5c292-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="5c292-140">換句話說，必須在 Azure AD 使用者與 Humanity 的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5c292-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="5c292-141">在 Humanity 中，將 Azure AD 中 [使用者名稱]的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5c292-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c292-142">若要設定及測試與 Humanity 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5c292-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c292-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5c292-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c292-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c292-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c292-145">**[建立 Humanity 測試使用者](#creating-a-humanity-test-user)** - 使 Humanity 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="5c292-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c292-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c292-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c292-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5c292-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c292-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5c292-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c292-149">在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Humanity 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c292-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="5c292-150">**若要設定 Humanity 的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5c292-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="5c292-151">在 Azure 入口網站的 [Humanity] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5c292-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5c292-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c292-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="5c292-155">在 [Humanity 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5c292-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="5c292-157">a.</span><span class="sxs-lookup"><span data-stu-id="5c292-157">a.</span></span> <span data-ttu-id="5c292-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="5c292-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="5c292-159">b.</span><span class="sxs-lookup"><span data-stu-id="5c292-159">b.</span></span> <span data-ttu-id="5c292-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="5c292-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c292-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="5c292-161">These values are not real.</span></span> <span data-ttu-id="5c292-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="5c292-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5c292-163">請連絡 [Humanity 用戶端支援小組](https://www.humanity.com/support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="5c292-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="5c292-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5c292-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="5c292-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c292-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c292-168">在 [Humanity 設定] 區段中，按一下 [設定 Humanity] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5c292-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5c292-169">複製 [快速參考] 區段中的 **SAML 單一登入服務 URL 和登出 URL**。</span><span class="sxs-lookup"><span data-stu-id="5c292-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="5c292-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **Humanity** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="5c292-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="5c292-172">在頂端的功能表中，按一下 [系統管理員] 。</span><span class="sxs-lookup"><span data-stu-id="5c292-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="5c292-173">![管理](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "管理")</span><span class="sxs-lookup"><span data-stu-id="5c292-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="5c292-174">在 [整合] 下方，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5c292-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="5c292-175">![單一登入](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="5c292-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="5c292-176">在 [單一登入]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5c292-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5c292-177">![單一登入](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="5c292-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="5c292-178">a.</span><span class="sxs-lookup"><span data-stu-id="5c292-178">a.</span></span> <span data-ttu-id="5c292-179">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="5c292-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="5c292-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c292-180">b.</span></span> <span data-ttu-id="5c292-181">選取 [允許密碼登入]。</span><span class="sxs-lookup"><span data-stu-id="5c292-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="5c292-182">c.</span><span class="sxs-lookup"><span data-stu-id="5c292-182">c.</span></span> <span data-ttu-id="5c292-183">將 [SAML 單一登入服務 URL] 的值貼到 [SAML 簽發者 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5c292-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="5c292-184">d.</span><span class="sxs-lookup"><span data-stu-id="5c292-184">d.</span></span> <span data-ttu-id="5c292-185">將 [登出 URL] 的值貼到 [遠端登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5c292-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="5c292-186">e.</span><span class="sxs-lookup"><span data-stu-id="5c292-186">e.</span></span> <span data-ttu-id="5c292-187">在記事本中開啟您的 base-64 編碼的憑證，將它的內容複製到您的剪貼簿，然後貼到 [X.509 憑證]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5c292-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="5c292-188">按一下 [儲存設定] 。</span><span class="sxs-lookup"><span data-stu-id="5c292-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="5c292-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="5c292-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c292-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="5c292-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c292-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c292-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c292-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5c292-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c292-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5c292-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5c292-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5c292-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c292-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5c292-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c292-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="5c292-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c292-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5c292-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c292-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5c292-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c292-204">a.</span><span class="sxs-lookup"><span data-stu-id="5c292-204">a.</span></span> <span data-ttu-id="5c292-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5c292-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c292-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c292-206">b.</span></span> <span data-ttu-id="5c292-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="5c292-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c292-208">c.</span><span class="sxs-lookup"><span data-stu-id="5c292-208">c.</span></span> <span data-ttu-id="5c292-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="5c292-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c292-210">d.</span><span class="sxs-lookup"><span data-stu-id="5c292-210">d.</span></span> <span data-ttu-id="5c292-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5c292-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="5c292-212">建立 Humanity 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5c292-212">Creating a Humanity test user</span></span>

<span data-ttu-id="5c292-213">若要讓 Azure AD 使用者能夠登入 Humanity，您必須將他們佈建至 Humanity。</span><span class="sxs-lookup"><span data-stu-id="5c292-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="5c292-214">在 Humanity 中，必須以手動方式進行佈建。</span><span class="sxs-lookup"><span data-stu-id="5c292-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="5c292-215">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5c292-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5c292-216">以系統管理員身分登入您的 **Humanity** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="5c292-216">Log in to your **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="5c292-217">按一下 Admin 。</span><span class="sxs-lookup"><span data-stu-id="5c292-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="5c292-218">![管理](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "管理")</span><span class="sxs-lookup"><span data-stu-id="5c292-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="5c292-219">按一下 [職員] 。</span><span class="sxs-lookup"><span data-stu-id="5c292-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="5c292-220">![職員](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "職員")</span><span class="sxs-lookup"><span data-stu-id="5c292-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="5c292-221">在 [動作] 下方，按一下 [新增員工]。</span><span class="sxs-lookup"><span data-stu-id="5c292-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="5c292-222">![新增員工](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "新增員工")</span><span class="sxs-lookup"><span data-stu-id="5c292-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="5c292-223">在 [新增員工]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5c292-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5c292-224">![儲存員工](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "儲存員工")</span><span class="sxs-lookup"><span data-stu-id="5c292-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="5c292-225">a.</span><span class="sxs-lookup"><span data-stu-id="5c292-225">a.</span></span> <span data-ttu-id="5c292-226">在相關的文字方塊中，輸入您想要佈建之有效 AAD 帳戶的 [名字]、[姓氏] 和 [電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="5c292-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="5c292-227">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c292-227">b.</span></span> <span data-ttu-id="5c292-228">按一下 [儲存員工] 。</span><span class="sxs-lookup"><span data-stu-id="5c292-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="5c292-229">您可以使用任何其他的 Humanity 使用者帳戶建立工具或 Humanity 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5c292-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c292-230">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5c292-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c292-231">在本節中，您將把 Humanity 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5c292-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![指派使用者][200] 

<span data-ttu-id="5c292-233">**若要將 Britta Simon 指派到 Humanity，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5c292-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="5c292-234">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5c292-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5c292-236">在應用程式清單中，選取 [Humanity]。</span><span class="sxs-lookup"><span data-stu-id="5c292-236">In the applications list, select **Humanity**.</span></span>

    ![設定單一登入](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="5c292-238">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5c292-238">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5c292-240">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c292-240">Click **Add** button.</span></span> <span data-ttu-id="5c292-241">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5c292-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5c292-243">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="5c292-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c292-244">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c292-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c292-245">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c292-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c292-246">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5c292-246">Testing single sign-on</span></span>

<span data-ttu-id="5c292-247">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="5c292-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c292-248">按一下存取面板中的 [Humanity] 圖格，應會自動登入您的 Humanity 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c292-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="5c292-249">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5c292-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c292-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="5c292-250">Additional resources</span></span>

* [<span data-ttu-id="5c292-251">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5c292-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c292-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5c292-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

