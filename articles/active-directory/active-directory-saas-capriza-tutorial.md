---
title: "教學課程：Azure Active Directory 與 Capriza Platform 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Capriza Platform 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 668c094d5330be1c5f71d51d2e76170dc69d1bce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="5689e-103">教學課程：Azure Active Directory 與 Capriza Platform 整合</span><span class="sxs-lookup"><span data-stu-id="5689e-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="5689e-104">在本教學課程中，您會了解如何將 Capriza Platform 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="5689e-104">In this tutorial, you learn how to integrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5689e-105">將 Capriza Platform 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="5689e-105">Integrating Capriza Platform with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5689e-106">您可以在 Azure AD 中控制可存取 Capriza Platform 的人員</span><span class="sxs-lookup"><span data-stu-id="5689e-106">You can control in Azure AD who has access to Capriza Platform</span></span>
- <span data-ttu-id="5689e-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Capriza Platform (單一登入)</span><span class="sxs-lookup"><span data-stu-id="5689e-107">You can enable your users to automatically get signed-on to Capriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5689e-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5689e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5689e-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5689e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5689e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5689e-110">Prerequisites</span></span>

<span data-ttu-id="5689e-111">若要設定 Azure AD 與 Capriza Platform 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5689e-111">To configure Azure AD integration with Capriza Platform, you need the following items:</span></span>

- <span data-ttu-id="5689e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5689e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5689e-113">已啟用 Capriza Platform 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5689e-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5689e-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5689e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5689e-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5689e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5689e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5689e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5689e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="5689e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5689e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5689e-118">Scenario description</span></span>
<span data-ttu-id="5689e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5689e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5689e-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5689e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5689e-121">從資源庫新增 Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="5689e-121">Adding Capriza Platform from the gallery</span></span>
2. <span data-ttu-id="5689e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5689e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-the-gallery"></a><span data-ttu-id="5689e-123">從資源庫新增 Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="5689e-123">Adding Capriza Platform from the gallery</span></span>
<span data-ttu-id="5689e-124">若要設定將 Capriza Platform 整合到 Azure AD 中，您需要從資源庫將 Capriza Platform 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="5689e-124">To configure the integration of Capriza Platform into Azure AD, you need to add Capriza Platform from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5689e-125">**若要從資源庫新增 Capriza Platform，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5689e-125">**To add Capriza Platform from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5689e-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5689e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5689e-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5689e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5689e-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5689e-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5689e-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5689e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5689e-133">在搜尋方塊中，輸入 **Capriza Platform**。</span><span class="sxs-lookup"><span data-stu-id="5689e-133">In the search box, type **Capriza Platform**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="5689e-135">在結果面板中，選取 [Capriza Platform]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="5689e-135">In the results panel, select **Capriza Platform**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5689e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5689e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5689e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Capriza Platform 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5689e-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5689e-139">若要讓單一登入能夠運作，Azure AD 必須知道 Capriza Platform 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="5689e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza Platform is to a user in Azure AD.</span></span> <span data-ttu-id="5689e-140">換句話說，必須在 Azure AD 使用者與 Capriza Platform 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5689e-140">In other words, a link relationship between an Azure AD user and the related user in Capriza Platform needs to be established.</span></span>

<span data-ttu-id="5689e-141">在 Capriza Platform 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5689e-141">In Capriza Platform, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5689e-142">若要設定及測試與 Capriza Platform 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="5689e-142">To configure and test Azure AD single sign-on with Capriza Platform, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5689e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5689e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5689e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5689e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5689e-145">**[建立 Capriza Platform 測試使用者](#creating-a-capriza-platform-test-user)** - 在 Capriza Platform 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="5689e-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - to have a counterpart of Britta Simon in Capriza Platform that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5689e-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5689e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5689e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5689e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5689e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5689e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5689e-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Capriza Platform 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5689e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="5689e-150">**若要設定與 Capriza Platform 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5689e-150">**To configure Azure AD single sign-on with Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="5689e-151">在 Azure 入口網站的 [Capriza Platform] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5689e-151">In the Azure portal, on the **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5689e-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5689e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="5689e-155">在 [Capriza Platform 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5689e-155">On the **Capriza Platform Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="5689e-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="5689e-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5689e-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="5689e-158">This value is not real.</span></span> <span data-ttu-id="5689e-159">使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="5689e-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="5689e-160">請連絡 [Capriza Platform 用戶端支援小組](mailTo:support@capriza.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="5689e-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) to get this value.</span></span> 

4. <span data-ttu-id="5689e-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="5689e-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="5689e-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5689e-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5689e-165">在 [Capriza Platform 組態] 區段上，按一下 [設定 Capriza Platform] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5689e-165">On the **Capriza Platform Configuration** section, click **Configure Capriza Platform** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5689e-166">從 [快速參考] 區段中複製「登出 URL」、「SAML 實體識別碼」及「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="5689e-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="5689e-168">若要在 **Capriza Platform** 端設定單一登入，您必須將已下載的「憑證」、「登出 URL」、「SAML 實體識別碼」及「SAML 單一登入服務 URL」傳送給 [Capriza Platform 支援小組](mailTo:support@capriza.com)。</span><span class="sxs-lookup"><span data-stu-id="5689e-168">To configure single sign-on on **Capriza Platform** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="5689e-169">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="5689e-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5689e-170">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="5689e-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5689e-171">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="5689e-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5689e-172">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5689e-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5689e-173">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5689e-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="5689e-174">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5689e-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5689e-176">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5689e-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5689e-177">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5689e-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5689e-179">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="5689e-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5689e-181">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5689e-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5689e-183">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5689e-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5689e-185">a.</span><span class="sxs-lookup"><span data-stu-id="5689e-185">a.</span></span> <span data-ttu-id="5689e-186">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5689e-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5689e-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5689e-187">b.</span></span> <span data-ttu-id="5689e-188">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="5689e-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5689e-189">c.</span><span class="sxs-lookup"><span data-stu-id="5689e-189">c.</span></span> <span data-ttu-id="5689e-190">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="5689e-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5689e-191">d.</span><span class="sxs-lookup"><span data-stu-id="5689e-191">d.</span></span> <span data-ttu-id="5689e-192">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5689e-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="5689e-193">建立 Capriza Platform 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5689e-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="5689e-194">本節的目標是要在 Capriza 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="5689e-194">The objective of this section is to create a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="5689e-195">Capriza 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="5689e-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="5689e-196">**請確定您已搭配 Capriza 來設定網域名稱，以便進行使用者佈建。之後，將只有 Just-In-Time 使用者佈建能夠運作。**</span><span class="sxs-lookup"><span data-stu-id="5689e-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only the just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="5689e-197">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="5689e-197">There is no action item for you in this section.</span></span> <span data-ttu-id="5689e-198">嘗試存取 Capriza 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="5689e-198">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5689e-199">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5689e-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5689e-200">在本節中，您會將 Capriza Platform 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5689e-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Capriza Platform.</span></span>

![指派使用者][200] 

<span data-ttu-id="5689e-202">**若要將 Britta Simon 指派給 Capriza Platform，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5689e-202">**To assign Britta Simon to Capriza Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="5689e-203">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5689e-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5689e-205">在應用程式清單中，選取 [Capriza Platform]。</span><span class="sxs-lookup"><span data-stu-id="5689e-205">In the applications list, select **Capriza Platform**.</span></span>

    ![設定單一登入](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="5689e-207">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5689e-207">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5689e-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5689e-209">Click **Add** button.</span></span> <span data-ttu-id="5689e-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5689e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5689e-212">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="5689e-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5689e-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5689e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5689e-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5689e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5689e-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5689e-215">Testing single sign-on</span></span>

<span data-ttu-id="5689e-216">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="5689e-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5689e-217">當您在「存取面板」中按一下 [Capriza Platform] 圖格時，應該會自動登入您的 Capriza Platform 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5689e-217">When you click the Capriza Platform tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span></span> <span data-ttu-id="5689e-218">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5689e-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5689e-219">其他資源</span><span class="sxs-lookup"><span data-stu-id="5689e-219">Additional resources</span></span>

* [<span data-ttu-id="5689e-220">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5689e-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5689e-221">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5689e-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

