---
title: "教學課程：Azure Active Directory 與 FM:Systems 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 FM:Systems 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3a597d228f6c9234ec2fd2644ec3ac50b98f3b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="6496e-103">教學課程：Azure Active Directory 與 FM:Systems 整合</span><span class="sxs-lookup"><span data-stu-id="6496e-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="6496e-104">在本教學課程中，您將了解如何整合 FM:Systems 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6496e-104">In this tutorial, you learn how to integrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6496e-105">FM:Systems 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="6496e-105">Integrating FM:Systems with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6496e-106">您可以在 Azure AD 中控制可存取 FM:Systems 的人員</span><span class="sxs-lookup"><span data-stu-id="6496e-106">You can control in Azure AD who has access to FM:Systems</span></span>
- <span data-ttu-id="6496e-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 FM:Systems (單一登入)</span><span class="sxs-lookup"><span data-stu-id="6496e-107">You can enable your users to automatically get signed-on to FM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6496e-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="6496e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6496e-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6496e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6496e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6496e-110">Prerequisites</span></span>

<span data-ttu-id="6496e-111">若要設定 Azure AD 與 FM:Systems 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6496e-111">To configure Azure AD integration with FM:Systems, you need the following items:</span></span>

- <span data-ttu-id="6496e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6496e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6496e-113">已啟用 FM: Systems 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6496e-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6496e-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6496e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6496e-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6496e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6496e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6496e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6496e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="6496e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6496e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6496e-118">Scenario description</span></span>
<span data-ttu-id="6496e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6496e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6496e-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="6496e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6496e-121">從資源庫新增 FM:Systems</span><span class="sxs-lookup"><span data-stu-id="6496e-121">Adding FM:Systems from the gallery</span></span>
2. <span data-ttu-id="6496e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6496e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-the-gallery"></a><span data-ttu-id="6496e-123">從資源庫新增 FM:Systems</span><span class="sxs-lookup"><span data-stu-id="6496e-123">Adding FM:Systems from the gallery</span></span>
<span data-ttu-id="6496e-124">若要設定將 FM:Systems 整合到 Azure AD 中，您需要從資源庫將 FM:Systems 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="6496e-124">To configure the integration of FM:Systems into Azure AD, you need to add FM:Systems from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6496e-125">**若要從資源庫新增 FM:Systems，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6496e-125">**To add FM:Systems from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6496e-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6496e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6496e-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6496e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6496e-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6496e-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6496e-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6496e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6496e-133">在搜尋方塊中，輸入 **FM:Systems**。</span><span class="sxs-lookup"><span data-stu-id="6496e-133">In the search box, type **FM:Systems**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="6496e-135">在結果窗格中，選取 [FM:Systems]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="6496e-135">In the results panel, select **FM:Systems**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6496e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6496e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6496e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FM:Systems 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6496e-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6496e-139">若要讓單一登入運作，Azure AD 必須知道 FM:Systems 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="6496e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FM:Systems is to a user in Azure AD.</span></span> <span data-ttu-id="6496e-140">換句話說，必須在 Azure AD 使用者與 FM:Systems 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6496e-140">In other words, a link relationship between an Azure AD user and the related user in FM:Systems needs to be established.</span></span>

<span data-ttu-id="6496e-141">在 FM:Systems 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6496e-141">In FM:Systems, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6496e-142">若要設定及測試與 FM:Systems 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="6496e-142">To configure and test Azure AD single sign-on with FM:Systems, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6496e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="6496e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6496e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6496e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6496e-145">**[建立 FM:Systems 測試使用者](#creating-an-fmsystems-test-user)** - 在 FM:Systems 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="6496e-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - to have a counterpart of Britta Simon in FM:Systems that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6496e-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6496e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6496e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="6496e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6496e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6496e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6496e-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 FM:Systems 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6496e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="6496e-150">**若要使用 FM:Systems 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6496e-150">**To configure Azure AD single sign-on with FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="6496e-151">在 Azure 入口網站的 [FM:Systems] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="6496e-151">In the Azure portal, on the **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6496e-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6496e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="6496e-155">在 [FM:Systems 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6496e-155">On the **FM:Systems Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="6496e-157">在 [回覆 URL] 文字方塊中，輸入 FM:Systems [回覆 URL]，使用下列模式輸入 URL：`https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span><span class="sxs-lookup"><span data-stu-id="6496e-157">In the **Reply URL** textbox, type your FM:Systems **Reply URL**, type the URL using the following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6496e-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="6496e-158">This value is not real.</span></span> <span data-ttu-id="6496e-159">請使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="6496e-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="6496e-160">請連絡 [FM:Systems 支援小組](https://fmsystems.com/ask-us/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="6496e-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) to get this value.</span></span>
 
4. <span data-ttu-id="6496e-161">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6496e-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="6496e-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6496e-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6496e-165">若要在 **FM:Systems** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [FM:Systems 支援小組](https://fmsystems.com/ask-us/)。</span><span class="sxs-lookup"><span data-stu-id="6496e-165">To configure single sign-on on **FM:Systems** side, you need to send the downloaded **Metadata XML** to [FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="6496e-166">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="6496e-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="6496e-167">當您的訂用帳戶啟用 SSO 之後，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="6496e-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="6496e-168">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="6496e-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6496e-169">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="6496e-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6496e-170">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6496e-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6496e-171">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6496e-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="6496e-172">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6496e-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6496e-174">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6496e-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6496e-175">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6496e-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6496e-177">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="6496e-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6496e-179">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6496e-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6496e-181">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6496e-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6496e-183">a.</span><span class="sxs-lookup"><span data-stu-id="6496e-183">a.</span></span> <span data-ttu-id="6496e-184">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6496e-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6496e-185">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6496e-185">b.</span></span> <span data-ttu-id="6496e-186">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="6496e-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6496e-187">c.</span><span class="sxs-lookup"><span data-stu-id="6496e-187">c.</span></span> <span data-ttu-id="6496e-188">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="6496e-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6496e-189">d.</span><span class="sxs-lookup"><span data-stu-id="6496e-189">d.</span></span> <span data-ttu-id="6496e-190">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6496e-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="6496e-191">建立 FM:Systems 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6496e-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="6496e-192">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 FM: Systems 公司網站。</span><span class="sxs-lookup"><span data-stu-id="6496e-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="6496e-193">移至 [系統管理]\>[管理安全性]\>[使用者]\>[使用者清單]。</span><span class="sxs-lookup"><span data-stu-id="6496e-193">Go to **System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="6496e-194">![系統管理](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "系統管理")</span><span class="sxs-lookup"><span data-stu-id="6496e-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="6496e-195">按一下 [建立新的使用者] 。</span><span class="sxs-lookup"><span data-stu-id="6496e-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="6496e-196">![建立新的使用者](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "建立新的使用者")</span><span class="sxs-lookup"><span data-stu-id="6496e-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="6496e-197">在 [建立使用者]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6496e-197">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6496e-198">![建立使用者](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="6496e-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="6496e-199">a.</span><span class="sxs-lookup"><span data-stu-id="6496e-199">a.</span></span> <span data-ttu-id="6496e-200">在相關的文字方塊中，輸入您想要佈建之有效 Azure Active Directory 帳戶的 [使用者名稱]、[密碼]、[確認密碼]、[電子郵件]、[員工識別碼]、[電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="6496e-200">Type the **UserName**, the **Password**, **Confirm Password**, **E-mail** and the **Employee ID** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="6496e-201">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6496e-201">b.</span></span> <span data-ttu-id="6496e-202">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6496e-202">Click **Next**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6496e-203">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6496e-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6496e-204">在本節中，您會將 FM:Systems 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6496e-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FM:Systems.</span></span>

![指派使用者][200] 

<span data-ttu-id="6496e-206">**若要將 Britta Simon 指派到 FM:Systems，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6496e-206">**To assign Britta Simon to FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="6496e-207">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6496e-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6496e-209">在應用程式清單中，選取 [FM:Systems]。</span><span class="sxs-lookup"><span data-stu-id="6496e-209">In the applications list, select **FM:Systems**.</span></span>

    ![設定單一登入](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="6496e-211">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6496e-211">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6496e-213">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6496e-213">Click **Add** button.</span></span> <span data-ttu-id="6496e-214">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6496e-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6496e-216">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="6496e-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6496e-217">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6496e-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6496e-218">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6496e-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6496e-219">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6496e-219">Testing single sign-on</span></span>

<span data-ttu-id="6496e-220">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="6496e-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6496e-221">當您在存取面板中按一下 [FM:Systems] 圖格時，應該會自動登入您的 FM:Systems 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6496e-221">When you click the FM:Systems tile in the Access Panel, you should get automatically signed-on to your FM:Systems application.</span></span>
<span data-ttu-id="6496e-222">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6496e-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6496e-223">其他資源</span><span class="sxs-lookup"><span data-stu-id="6496e-223">Additional resources</span></span>

* [<span data-ttu-id="6496e-224">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="6496e-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6496e-225">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6496e-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

