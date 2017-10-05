---
title: "教學課程：Azure Active Directory 與 Aha! | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Aha! 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7723864b2e1ab2d5b69d86f0fa18416b9d3f9aa3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="5f260-104">教學課程：Azure Active Directory 與 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="5f260-105">在本教學課程中，您會了解如何將 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="5f260-106">與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="5f260-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f260-107">將 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-107">Integrating Aha!</span></span> <span data-ttu-id="5f260-108">與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="5f260-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5f260-109">您可以在 Azure AD 中控制可存取 Aha! 的人員</span><span class="sxs-lookup"><span data-stu-id="5f260-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="5f260-110">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="5f260-111">(單一登入)</span><span class="sxs-lookup"><span data-stu-id="5f260-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5f260-112">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5f260-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5f260-113">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5f260-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f260-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="5f260-114">Prerequisites</span></span>

<span data-ttu-id="5f260-115">若要設定 Azure AD 與 Aha! 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5f260-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="5f260-116">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5f260-116">An Azure AD subscription</span></span>
- <span data-ttu-id="5f260-117">已啟用 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-117">An Aha!</span></span> <span data-ttu-id="5f260-118">單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5f260-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f260-119">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5f260-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f260-120">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5f260-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f260-121">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5f260-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f260-122">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5f260-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f260-123">案例描述</span><span class="sxs-lookup"><span data-stu-id="5f260-123">Scenario description</span></span>
<span data-ttu-id="5f260-124">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5f260-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f260-125">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5f260-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f260-126">新增 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-126">Adding Aha!</span></span> <span data-ttu-id="5f260-127">(從資源庫)</span><span class="sxs-lookup"><span data-stu-id="5f260-127">from the gallery</span></span>
2. <span data-ttu-id="5f260-128">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5f260-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="5f260-129">新增 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-129">Adding Aha!</span></span> <span data-ttu-id="5f260-130">(從資源庫)</span><span class="sxs-lookup"><span data-stu-id="5f260-130">from the gallery</span></span>
<span data-ttu-id="5f260-131">若要設定將 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-131">To configure the integration of Aha!</span></span> <span data-ttu-id="5f260-132">整合到 Azure AD 中，您需要從資源庫將 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="5f260-133">新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="5f260-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5f260-134">**若要從資源庫新增 Aha!，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5f260-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5f260-135">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5f260-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5f260-137">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5f260-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5f260-138">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5f260-138">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5f260-140">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5f260-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5f260-142">在搜尋方塊中，輸入 **Aha!**。</span><span class="sxs-lookup"><span data-stu-id="5f260-142">In the search box, type **Aha!**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="5f260-144">在結果面板中，選取 [Aha!]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f260-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5f260-146">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5f260-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5f260-147">在本節中，您會設定及測試與 Aha! 搭配運作的 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5f260-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="5f260-148">(以名為 "Britta Simon" 的測試使用者為基礎)。</span><span class="sxs-lookup"><span data-stu-id="5f260-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5f260-149">若要讓單一登入能夠運作，Azure AD 必須知道 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="5f260-150">與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="5f260-150">is to a user in Azure AD.</span></span> <span data-ttu-id="5f260-151">換句話說，必須在 Azure AD 使用者與 Aha! 中的相關使用者之間</span><span class="sxs-lookup"><span data-stu-id="5f260-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="5f260-152">建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5f260-152">needs to be established.</span></span>

<span data-ttu-id="5f260-153">在 Aha! 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5f260-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5f260-154">若要設定及測試與 Aha! 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="5f260-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5f260-155">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5f260-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5f260-156">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5f260-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f260-157">**[建立 Aha! 測試使用者](#creating-an-aha-test-user)** - 在 Aha! 中建立一個與 Azure AD 中代表 Britta Simon 之項目</span><span class="sxs-lookup"><span data-stu-id="5f260-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="5f260-158">連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="5f260-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f260-159">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5f260-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f260-160">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5f260-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5f260-161">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5f260-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5f260-162">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="5f260-163">應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5f260-163">application.</span></span>

<span data-ttu-id="5f260-164">**若要設定與 Aha! 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5f260-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="5f260-165">在 Azure 入口網站的 [Aha!]</span><span class="sxs-lookup"><span data-stu-id="5f260-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="5f260-166">應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5f260-166">application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5f260-168">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5f260-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="5f260-170">在 [Aha!網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5f260-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="5f260-172">a.</span><span class="sxs-lookup"><span data-stu-id="5f260-172">a.</span></span> <span data-ttu-id="5f260-173">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="5f260-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="5f260-174">b.</span><span class="sxs-lookup"><span data-stu-id="5f260-174">b.</span></span> <span data-ttu-id="5f260-175">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="5f260-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5f260-176">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="5f260-176">These values are not real.</span></span> <span data-ttu-id="5f260-177">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="5f260-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5f260-178">請連絡 [Aha!用戶端支援小組](https://www.aha.io/company/contact)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="5f260-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="5f260-179">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5f260-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="5f260-181">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5f260-181">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5f260-183">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="5f260-184">公司網站。</span><span class="sxs-lookup"><span data-stu-id="5f260-184">company site as an administrator.</span></span>

7. <span data-ttu-id="5f260-185">在頂端的功能表中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="5f260-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="5f260-186">![設定](./media/active-directory-saas-aha-tutorial/IC798950.png "設定")</span><span class="sxs-lookup"><span data-stu-id="5f260-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="5f260-187">按一下 [帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="5f260-187">Click **Account**.</span></span>
   
    <span data-ttu-id="5f260-188">![設定檔](./media/active-directory-saas-aha-tutorial/IC798951.png "設定檔")</span><span class="sxs-lookup"><span data-stu-id="5f260-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="5f260-189">按一下 [安全性和單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="5f260-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="5f260-190">![安全性和單一登入](./media/active-directory-saas-aha-tutorial/IC798952.png "安全性和單一登入")</span><span class="sxs-lookup"><span data-stu-id="5f260-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="5f260-191">在 [單一登入] 區段中，針對 [識別提供者] 選取 [SAML2.0]。</span><span class="sxs-lookup"><span data-stu-id="5f260-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="5f260-192">![安全性和單一登入](./media/active-directory-saas-aha-tutorial/IC798953.png "安全性和單一登入")</span><span class="sxs-lookup"><span data-stu-id="5f260-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="5f260-193">在 [單一登入]  組態頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5f260-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="5f260-194">![單一登入](./media/active-directory-saas-aha-tutorial/IC798954.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="5f260-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="5f260-195">a.</span><span class="sxs-lookup"><span data-stu-id="5f260-195">a.</span></span> <span data-ttu-id="5f260-196">在 [名稱]  文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="5f260-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="5f260-197">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f260-197">b.</span></span> <span data-ttu-id="5f260-198">針對 [設定使用]，選取 [中繼資料檔]。</span><span class="sxs-lookup"><span data-stu-id="5f260-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="5f260-199">c.</span><span class="sxs-lookup"><span data-stu-id="5f260-199">c.</span></span> <span data-ttu-id="5f260-200">若要上傳您下載的中繼資料檔，請按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="5f260-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="5f260-201">d.</span><span class="sxs-lookup"><span data-stu-id="5f260-201">d.</span></span> <span data-ttu-id="5f260-202">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="5f260-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="5f260-203">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="5f260-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5f260-204">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="5f260-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5f260-205">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5f260-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5f260-206">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5f260-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="5f260-207">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5f260-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5f260-209">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5f260-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5f260-210">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5f260-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5f260-212">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="5f260-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5f260-214">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5f260-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5f260-216">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5f260-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5f260-218">a.</span><span class="sxs-lookup"><span data-stu-id="5f260-218">a.</span></span> <span data-ttu-id="5f260-219">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5f260-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f260-220">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f260-220">b.</span></span> <span data-ttu-id="5f260-221">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="5f260-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5f260-222">c.</span><span class="sxs-lookup"><span data-stu-id="5f260-222">c.</span></span> <span data-ttu-id="5f260-223">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="5f260-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5f260-224">d.</span><span class="sxs-lookup"><span data-stu-id="5f260-224">d.</span></span> <span data-ttu-id="5f260-225">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5f260-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="5f260-226">建立 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-226">Creating an Aha!</span></span> <span data-ttu-id="5f260-227">測試使用者</span><span class="sxs-lookup"><span data-stu-id="5f260-227">test user</span></span>

<span data-ttu-id="5f260-228">若要讓 Azure AD 使用者能夠登入 Aha!，必須將他們佈建到 Aha!。</span><span class="sxs-lookup"><span data-stu-id="5f260-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="5f260-229">Aha! 的佈建是自動化工作。</span><span class="sxs-lookup"><span data-stu-id="5f260-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="5f260-230">沒有您適用的動作項目。</span><span class="sxs-lookup"><span data-stu-id="5f260-230">There is no action item for you.</span></span>

<span data-ttu-id="5f260-231">第一次嘗試單一登入時，會視需要自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="5f260-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="5f260-232">您可以使用任何其他的 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-232">You can use any other Aha!</span></span> <span data-ttu-id="5f260-233">使用者帳戶建立工具或 Aha!</span><span class="sxs-lookup"><span data-stu-id="5f260-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="5f260-234">提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f260-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5f260-235">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5f260-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5f260-236">在本節中，您會將 Aha! 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5f260-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![指派使用者][200] 

<span data-ttu-id="5f260-238">**若要將 Britta Simon 指派給 Aha!，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5f260-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="5f260-239">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5f260-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5f260-241">在應用程式清單中，選取 [Aha!]。</span><span class="sxs-lookup"><span data-stu-id="5f260-241">In the applications list, select **Aha!**.</span></span>

    ![設定單一登入](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="5f260-243">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5f260-243">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5f260-245">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5f260-245">Click **Add** button.</span></span> <span data-ttu-id="5f260-246">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5f260-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5f260-248">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="5f260-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5f260-249">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5f260-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f260-250">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5f260-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5f260-251">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5f260-251">Testing single sign-on</span></span>

<span data-ttu-id="5f260-252">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="5f260-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5f260-253">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5f260-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f260-254">其他資源</span><span class="sxs-lookup"><span data-stu-id="5f260-254">Additional resources</span></span>

* [<span data-ttu-id="5f260-255">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5f260-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f260-256">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5f260-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

