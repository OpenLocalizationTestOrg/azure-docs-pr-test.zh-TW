---
title: "教學課程：Azure Active Directory 與 MobileXpense 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 MobileXpense 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: 030a1fc9f36d6fcfa607552d85ce232e36eaa64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="4892e-103">教學課程：Azure Active Directory 與 MobileXpense 整合</span><span class="sxs-lookup"><span data-stu-id="4892e-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="4892e-104">在本教學課程中，您將了解如何將 MobileXpense 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="4892e-104">In this tutorial, you learn how to integrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4892e-105">將 MobileXpense 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="4892e-105">Integrating MobileXpense with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4892e-106">您可以在 Azure AD 中控制可存取 MobileXpense 的人員</span><span class="sxs-lookup"><span data-stu-id="4892e-106">You can control in Azure AD who has access to MobileXpense</span></span>
- <span data-ttu-id="4892e-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 MobileXpense (單一登入)</span><span class="sxs-lookup"><span data-stu-id="4892e-107">You can enable your users to automatically get signed-on to MobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4892e-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="4892e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4892e-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4892e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4892e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4892e-110">Prerequisites</span></span>

<span data-ttu-id="4892e-111">若要設定 Azure AD 與 MobileXpense 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="4892e-111">To configure Azure AD integration with MobileXpense, you need the following items:</span></span>

- <span data-ttu-id="4892e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4892e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4892e-113">已啟用 MobileXpense 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4892e-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4892e-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4892e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4892e-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4892e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4892e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4892e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4892e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="4892e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4892e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4892e-118">Scenario description</span></span>
<span data-ttu-id="4892e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4892e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4892e-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="4892e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4892e-121">從資源庫新增 MobileXpense</span><span class="sxs-lookup"><span data-stu-id="4892e-121">Adding MobileXpense from the gallery</span></span>
2. <span data-ttu-id="4892e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4892e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-the-gallery"></a><span data-ttu-id="4892e-123">從資源庫新增 MobileXpense</span><span class="sxs-lookup"><span data-stu-id="4892e-123">Adding MobileXpense from the gallery</span></span>
<span data-ttu-id="4892e-124">若要設定將 MobileXpense 整合到 Azure AD 中，您需要從資源庫將 MobileXpense 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="4892e-124">To configure the integration of MobileXpense into Azure AD, you need to add MobileXpense from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4892e-125">**若要從資源庫新增 MobileXpense，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4892e-125">**To add MobileXpense from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4892e-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4892e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4892e-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4892e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4892e-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4892e-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="4892e-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4892e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="4892e-133">在搜尋方塊中輸入 **MobileXpense**。</span><span class="sxs-lookup"><span data-stu-id="4892e-133">In the search box, type **MobileXpense**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="4892e-135">在結果窗格中，選取 [MobileXpense]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="4892e-135">In the results panel, select **MobileXpense**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4892e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4892e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4892e-138">在本節中，您會以測試使用者 "Britta Simon" 的身分，設定及測試 Azure AD 與 MobileXpense 的單一登入。</span><span class="sxs-lookup"><span data-stu-id="4892e-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4892e-139">若要讓單一登入能夠運作，Azure AD 必須知道 MobileXpense 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="4892e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MobileXpense is to a user in Azure AD.</span></span> <span data-ttu-id="4892e-140">換句話說，必須建立 Azure AD 使用者和 MobileXpense 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4892e-140">In other words, a link relationship between an Azure AD user and the related user in MobileXpense needs to be established.</span></span>

<span data-ttu-id="4892e-141">在 MobileXpense 中，將**使用者名稱**的值指派為 Azure AD 中**使用者名稱**的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4892e-141">In MobileXpense, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4892e-142">為了設定及測試 Azure AD 與 MobileXpense 的單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="4892e-142">To configure and test Azure AD single sign-on with MobileXpense, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4892e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="4892e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4892e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4892e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4892e-145">**[建立 MobileXpense 測試使用者](#creating-a-mobilexpense-test-user)** - 使 MobileXpense 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="4892e-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - to have a counterpart of Britta Simon in MobileXpense that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4892e-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4892e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4892e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="4892e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4892e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4892e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4892e-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 MobileXpense 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="4892e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="4892e-150">**若要設定 Azure AD 與 MobileXpense 的單一登入，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4892e-150">**To configure Azure AD single sign-on with MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="4892e-151">在 Azure 入口網站的 [MobileXpense] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="4892e-151">In the Azure portal, on the **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="4892e-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="4892e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="4892e-155">如果您想要以 **IDP 起始模式**設定應用程式，請在 [MobileXpense 網域和 URL] 區段執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4892e-155">On the **MobileXpense Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="4892e-157">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="4892e-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="4892e-158">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]：</span><span class="sxs-lookup"><span data-stu-id="4892e-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="4892e-160">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="4892e-160">In the **Sign-on URL** textbox, type a URL using the following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="4892e-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="4892e-161">These values are not real.</span></span> <span data-ttu-id="4892e-162">使用實際的回覆 URL 與登入 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="4892e-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="4892e-163">請連絡 [MobileXpense 客戶支援小組](http://www.mobilexpense.net/contact)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="4892e-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) to get these values.</span></span> 

5. <span data-ttu-id="4892e-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4892e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="4892e-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4892e-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4892e-168">若要在 **MobileXpense** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [MobileXpense 支援小組](http://www.mobilexpense.net/contact)。</span><span class="sxs-lookup"><span data-stu-id="4892e-168">To configure single sign-on on **MobileXpense** side, you need to send the downloaded **Metadata XML** to [MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="4892e-169">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="4892e-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4892e-170">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="4892e-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4892e-171">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4892e-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4892e-172">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4892e-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="4892e-173">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4892e-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="4892e-175">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4892e-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4892e-176">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4892e-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4892e-178">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4892e-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4892e-180">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4892e-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4892e-182">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4892e-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4892e-184">a.</span><span class="sxs-lookup"><span data-stu-id="4892e-184">a.</span></span> <span data-ttu-id="4892e-185">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4892e-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4892e-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="4892e-186">b.</span></span> <span data-ttu-id="4892e-187">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="4892e-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4892e-188">c.</span><span class="sxs-lookup"><span data-stu-id="4892e-188">c.</span></span> <span data-ttu-id="4892e-189">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="4892e-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4892e-190">d.</span><span class="sxs-lookup"><span data-stu-id="4892e-190">d.</span></span> <span data-ttu-id="4892e-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4892e-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="4892e-192">建立 MobileXpense 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4892e-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="4892e-193">在本節中，您要在 MobileXpense 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4892e-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="4892e-194">與 [MobileXpense 支援小組](http://www.mobilexpense.net/contact) 合作，在 MobileXpense 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="4892e-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add the users in the MobileXpense platform.</span></span> <span data-ttu-id="4892e-195">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="4892e-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4892e-196">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4892e-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4892e-197">在本節中，您會將 MobileXpense 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4892e-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MobileXpense.</span></span>

![指派使用者][200] 

<span data-ttu-id="4892e-199">**若要將 Britta Simon 指派給 MobileXpense，執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4892e-199">**To assign Britta Simon to MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="4892e-200">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4892e-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4892e-202">在應用程式清單中，選取 [MobileXpense]。</span><span class="sxs-lookup"><span data-stu-id="4892e-202">In the applications list, select **MobileXpense**.</span></span>

    ![設定單一登入](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="4892e-204">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4892e-204">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="4892e-206">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4892e-206">Click **Add** button.</span></span> <span data-ttu-id="4892e-207">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4892e-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="4892e-209">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="4892e-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4892e-210">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4892e-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4892e-211">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4892e-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4892e-212">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4892e-212">Testing single sign-on</span></span>

<span data-ttu-id="4892e-213">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="4892e-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4892e-214">當您在存取面板中按一下 [MobileXpense] 圖格時，應該會自動登入您的 MobileXpense 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4892e-214">When you click the MobileXpense tile in the Access Panel, you should get automatically signed-on to your MobileXpense application.</span></span>
<span data-ttu-id="4892e-215">如需存取面板的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="4892e-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4892e-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="4892e-216">Additional resources</span></span>

* [<span data-ttu-id="4892e-217">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="4892e-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4892e-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4892e-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png
