---
title: "教學課程：將 Azure Active Directory 與 Namely 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Namely 之間的單一登入功能。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 1d7e8fbcfc757853ab909bbb05522f3dc387715d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="4b036-103">教學課程：將 Azure Active Directory 與 Namely 整合</span><span class="sxs-lookup"><span data-stu-id="4b036-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="4b036-104">在本教學課程中，您將了解如何整合 Namely 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4b036-104">In this tutorial, you learn how to integrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b036-105">將 Namely 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="4b036-105">Integrating Namely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b036-106">您可以在 Azure AD 中控制可存取 Namely 的人員</span><span class="sxs-lookup"><span data-stu-id="4b036-106">You can control in Azure AD who has access to Namely</span></span>
- <span data-ttu-id="4b036-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Namely (單一登入)</span><span class="sxs-lookup"><span data-stu-id="4b036-107">You can enable your users to automatically get signed-on to Namely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b036-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="4b036-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4b036-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4b036-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b036-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4b036-110">Prerequisites</span></span>

<span data-ttu-id="4b036-111">若要設定 Namely 與 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="4b036-111">To configure Azure AD integration with Namely, you need the following items:</span></span>

- <span data-ttu-id="4b036-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4b036-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b036-113">已啟用 Namely 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4b036-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b036-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4b036-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b036-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4b036-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b036-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4b036-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b036-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="4b036-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b036-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4b036-118">Scenario description</span></span>
<span data-ttu-id="4b036-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b036-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b036-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="4b036-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b036-121">從資源庫新增 Namely</span><span class="sxs-lookup"><span data-stu-id="4b036-121">Adding Namely from the gallery</span></span>
2. <span data-ttu-id="4b036-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b036-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-the-gallery"></a><span data-ttu-id="4b036-123">從資源庫新增 Namely</span><span class="sxs-lookup"><span data-stu-id="4b036-123">Adding Namely from the gallery</span></span>
<span data-ttu-id="4b036-124">若要設定將 Namely 整合到 Azure AD 中，您需要從資源庫將 Namely 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="4b036-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b036-125">**若要從資源庫新增 Namely，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4b036-125">**To add Namely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b036-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4b036-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b036-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4b036-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b036-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4b036-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="4b036-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b036-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="4b036-133">在搜尋方塊中，輸入 **Namely**。</span><span class="sxs-lookup"><span data-stu-id="4b036-133">In the search box, type **Namely**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="4b036-135">在結果窗格中，選取 [Namely]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b036-135">In the results panel, select **Namely**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b036-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b036-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b036-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Namely 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b036-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b036-139">若要讓單一登入運作，Azure AD 必須知道 Namely 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="4b036-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Namely is to a user in Azure AD.</span></span> <span data-ttu-id="4b036-140">換句話說，必須在 Azure AD 使用者與 Namely 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4b036-140">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span></span>

<span data-ttu-id="4b036-141">在 Namely 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4b036-141">In Namely, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4b036-142">若要設定及測試與 Namely 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="4b036-142">To configure and test Azure AD single sign-on with Namely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b036-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="4b036-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4b036-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b036-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b036-145">**[建立 Namely 測試使用者](#creating-a-namely-test-user)** - 使 Namely 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="4b036-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b036-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b036-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b036-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="4b036-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b036-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b036-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b036-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Namely 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b036-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="4b036-150">**若要設定與 Namely 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4b036-150">**To configure Azure AD single sign-on with Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="4b036-151">在 Azure 入口網站的 [Namely] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="4b036-151">In the Azure portal, on the **Namely** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="4b036-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b036-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="4b036-155">在 [Namely 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b036-155">On the **Namely Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="4b036-157">a.</span><span class="sxs-lookup"><span data-stu-id="4b036-157">a.</span></span> <span data-ttu-id="4b036-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="4b036-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="4b036-159">b.</span><span class="sxs-lookup"><span data-stu-id="4b036-159">b.</span></span> <span data-ttu-id="4b036-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="4b036-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b036-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="4b036-161">These values are not real.</span></span> <span data-ttu-id="4b036-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="4b036-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4b036-163">請連絡 [Namely 客戶支援小組](https://www.namely.com/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="4b036-163">Contact [Namely Client support team](https://www.namely.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="4b036-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4b036-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="4b036-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b036-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b036-168">在 [Namely 組態] 區段上，按一下 [設定 Namely] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="4b036-168">On the **Namely Configuration** section, click **Configure Namely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4b036-169">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="4b036-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="4b036-171">在另一個瀏覽器視窗中，以系統管理員身分登入您的 Namely 公司網站。</span><span class="sxs-lookup"><span data-stu-id="4b036-171">In another browser window, sign on to your Namely company site as an administrator.</span></span>

8. <span data-ttu-id="4b036-172">在頂端的工具列中，按一下 [公司] 。</span><span class="sxs-lookup"><span data-stu-id="4b036-172">In the toolbar on the top, click **Company**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="4b036-174">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4b036-174">Click the **Settings** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="4b036-176">按一下 [SAML] 。</span><span class="sxs-lookup"><span data-stu-id="4b036-176">Click **SAML**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="4b036-178">在 [SAML設定]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b036-178">On the **SAML Settings** page, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="4b036-180">a.</span><span class="sxs-lookup"><span data-stu-id="4b036-180">a.</span></span> <span data-ttu-id="4b036-181">按一下 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="4b036-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="4b036-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b036-182">b.</span></span> <span data-ttu-id="4b036-183">在 [識別提供者 SSO URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="4b036-183">In the **Identity provider SSO url** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4b036-184">c.</span><span class="sxs-lookup"><span data-stu-id="4b036-184">c.</span></span> <span data-ttu-id="4b036-185">在記事本中開啟下載的憑證，複製其內容，然後貼到 [識別提供者憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="4b036-185">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="4b036-186">d.</span><span class="sxs-lookup"><span data-stu-id="4b036-186">d.</span></span> <span data-ttu-id="4b036-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="4b036-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4b036-188">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="4b036-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4b036-189">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="4b036-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b036-190">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b036-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b036-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b036-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b036-192">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4b036-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="4b036-194">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4b036-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b036-195">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4b036-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b036-197">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4b036-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b036-199">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4b036-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b036-201">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b036-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b036-203">a.</span><span class="sxs-lookup"><span data-stu-id="4b036-203">a.</span></span> <span data-ttu-id="4b036-204">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4b036-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b036-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b036-205">b.</span></span> <span data-ttu-id="4b036-206">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="4b036-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b036-207">c.</span><span class="sxs-lookup"><span data-stu-id="4b036-207">c.</span></span> <span data-ttu-id="4b036-208">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="4b036-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4b036-209">d.</span><span class="sxs-lookup"><span data-stu-id="4b036-209">d.</span></span> <span data-ttu-id="4b036-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4b036-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="4b036-211">建立 Namely 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b036-211">Creating a Namely test user</span></span>

<span data-ttu-id="4b036-212">本節的目標是要在 Namely 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4b036-212">The objective of this section is to create a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="4b036-213">**若要在 Namely 中建立名為 Britta Simon 的使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4b036-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="4b036-214">以管理員身分登入您的 Namely 公司網站。</span><span class="sxs-lookup"><span data-stu-id="4b036-214">Sign-on to your Namely company site as an administrator.</span></span>

2. <span data-ttu-id="4b036-215">在頂端工具列中，按一下 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="4b036-215">In the toolbar on the top, click **People**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="4b036-217">按一下 [目錄]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4b036-217">Click the **Directory** tab.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="4b036-219">按一下 [ **新增人員**]。</span><span class="sxs-lookup"><span data-stu-id="4b036-219">Click **Add New Person**.</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="4b036-221">在 [ **新增人員** ] 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b036-221">On the **Add New Person** dialog, perform the following steps:</span></span>

    <span data-ttu-id="4b036-222">a.</span><span class="sxs-lookup"><span data-stu-id="4b036-222">a.</span></span> <span data-ttu-id="4b036-223">在 [名字] 文字方塊中，輸入 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="4b036-223">In the **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="4b036-224">b.</span><span class="sxs-lookup"><span data-stu-id="4b036-224">b.</span></span> <span data-ttu-id="4b036-225">在 [姓氏] 文字方塊中，輸入 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="4b036-225">In the **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="4b036-226">c.</span><span class="sxs-lookup"><span data-stu-id="4b036-226">c.</span></span> <span data-ttu-id="4b036-227">在 [電子郵件] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="4b036-227">In the **Email** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b036-228">d.</span><span class="sxs-lookup"><span data-stu-id="4b036-228">d.</span></span> <span data-ttu-id="4b036-229">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="4b036-229">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4b036-230">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b036-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4b036-231">在本節中，您會將 Namely 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b036-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Namely.</span></span>

![指派使用者][200] 

<span data-ttu-id="4b036-233">**若要將 Britta Simon 指派給 Namely，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4b036-233">**To assign Britta Simon to Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="4b036-234">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4b036-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4b036-236">在應用程式清單中，選取 [Namely] 。</span><span class="sxs-lookup"><span data-stu-id="4b036-236">In the applications list, select **Namely**.</span></span>

    ![設定單一登入](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="4b036-238">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4b036-238">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="4b036-240">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b036-240">Click **Add** button.</span></span> <span data-ttu-id="4b036-241">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4b036-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="4b036-243">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="4b036-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4b036-244">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b036-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b036-245">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b036-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b036-246">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4b036-246">Testing single sign-on</span></span>

<span data-ttu-id="4b036-247">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="4b036-247">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4b036-248">當您在存取面板中按一下 Namely 圖示時，應該會自動登入 Namely 應用程式</span><span class="sxs-lookup"><span data-stu-id="4b036-248">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b036-249">其他資源</span><span class="sxs-lookup"><span data-stu-id="4b036-249">Additional resources</span></span>

* [<span data-ttu-id="4b036-250">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="4b036-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b036-251">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4b036-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png
