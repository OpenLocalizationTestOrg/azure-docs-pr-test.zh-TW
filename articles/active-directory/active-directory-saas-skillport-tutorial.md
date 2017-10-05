---
title: "教學課程：Azure Active Directory 與 Skillport 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Skillport 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 668fc5ae4f964bd776904c3a9dbc2b203689d50c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="7146d-103">教學課程：Azure Active Directory 與 Skillport 整合</span><span class="sxs-lookup"><span data-stu-id="7146d-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="7146d-104">在本教學課程中，您會了解如何整合 Skillport 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7146d-104">In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7146d-105">Skillport 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7146d-105">Integrating Skillport with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7146d-106">您可以在 Azure AD 中控制可存取 Skillport 的人員</span><span class="sxs-lookup"><span data-stu-id="7146d-106">You can control in Azure AD who has access to Skillport</span></span>
- <span data-ttu-id="7146d-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Skillport (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7146d-107">You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7146d-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7146d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7146d-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7146d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7146d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7146d-110">Prerequisites</span></span>

<span data-ttu-id="7146d-111">若要設定 Azure AD 與 Skillport 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7146d-111">To configure Azure AD integration with Skillport, you need the following items:</span></span>

- <span data-ttu-id="7146d-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7146d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7146d-113">已啟用 Skillport 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7146d-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7146d-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7146d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7146d-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7146d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7146d-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7146d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7146d-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7146d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7146d-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7146d-118">Scenario description</span></span>
<span data-ttu-id="7146d-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7146d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7146d-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7146d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7146d-121">從資源庫新增 Skillport</span><span class="sxs-lookup"><span data-stu-id="7146d-121">Adding Skillport from the gallery</span></span>
2. <span data-ttu-id="7146d-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7146d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-the-gallery"></a><span data-ttu-id="7146d-123">從資源庫新增 Skillport</span><span class="sxs-lookup"><span data-stu-id="7146d-123">Adding Skillport from the gallery</span></span>
<span data-ttu-id="7146d-124">若要設定 Skillport 與 Azure AD 的整合作業，您必須從資源庫將 Skillport 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7146d-124">To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7146d-125">**若要從資源庫新增 Skillport，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7146d-125">**To add Skillport from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7146d-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7146d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7146d-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7146d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7146d-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7146d-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7146d-131">按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7146d-131">Click **New Application** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7146d-133">在搜尋方塊中，輸入 **Skillport**。</span><span class="sxs-lookup"><span data-stu-id="7146d-133">In the search box, type **Skillport**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="7146d-135">在結果窗格中，選取 [Skillport]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7146d-135">In the results panel, select **Skillport**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7146d-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7146d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7146d-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Skillport 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7146d-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7146d-139">若要讓單一登入能夠運作，Azure AD 必須知道 Skillport 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7146d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD.</span></span> <span data-ttu-id="7146d-140">換句話說，必須在 Azure AD 使用者和 Skillport 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7146d-140">In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.</span></span>

<span data-ttu-id="7146d-141">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 Skillport 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="7146d-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.</span></span>

<span data-ttu-id="7146d-142">若要設定及測試與 Skillport 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7146d-142">To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7146d-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7146d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7146d-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7146d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7146d-145">**[建立 Skillport 測試使用者](#creating-a-skillport-test-user)** - 使 Skillport 中 Britta Simon 的對應身分連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="7146d-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7146d-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7146d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7146d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7146d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7146d-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7146d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7146d-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Skillport 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7146d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="7146d-150">**若要使用 Skillport 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7146d-150">**To configure Azure AD single sign-on with Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="7146d-151">在 Azure 入口網站的 [Skillport] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7146d-151">In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7146d-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7146d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="7146d-155">在 [Skillport 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7146d-155">On the **Skillport Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="7146d-157">a.</span><span class="sxs-lookup"><span data-stu-id="7146d-157">a.</span></span> <span data-ttu-id="7146d-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰</span><span class="sxs-lookup"><span data-stu-id="7146d-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      
      <span data-ttu-id="7146d-159">EU 資料中心：`https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="7146d-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="7146d-160">US 資料中心：`https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="7146d-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="7146d-161">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7146d-161">b.</span></span> <span data-ttu-id="7146d-162">在 [回覆 URL] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="7146d-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    
      <span data-ttu-id="7146d-163">EU 資料中心：`https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="7146d-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="7146d-164">US 資料中心：`https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="7146d-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7146d-165">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7146d-165">These values are not the real.</span></span> <span data-ttu-id="7146d-166">使用實際的回覆 URL 與登入 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="7146d-166">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="7146d-167">請連絡 [Skillport 用戶端支援小組](https://www.skillsoft.com/contact.asp)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="7146d-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) to get these values.</span></span>
 
4. <span data-ttu-id="7146d-168">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7146d-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="7146d-170">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7146d-170">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7146d-172">若要在 **Skillport** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Skillport 支援小組](https://www.skillsoft.com/contact.asp)。</span><span class="sxs-lookup"><span data-stu-id="7146d-172">To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="7146d-173">他們將進行設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="7146d-173">They will set it up to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7146d-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7146d-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="7146d-175">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7146d-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7146d-177">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7146d-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7146d-178">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7146d-178">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7146d-180">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="7146d-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7146d-182">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7146d-182">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7146d-184">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7146d-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7146d-186">a.</span><span class="sxs-lookup"><span data-stu-id="7146d-186">a.</span></span> <span data-ttu-id="7146d-187">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7146d-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7146d-188">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7146d-188">b.</span></span> <span data-ttu-id="7146d-189">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7146d-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7146d-190">c.</span><span class="sxs-lookup"><span data-stu-id="7146d-190">c.</span></span> <span data-ttu-id="7146d-191">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7146d-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7146d-192">d.</span><span class="sxs-lookup"><span data-stu-id="7146d-192">d.</span></span> <span data-ttu-id="7146d-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7146d-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="7146d-194">建立 Skillport 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7146d-194">Creating a Skillport test user</span></span>

<span data-ttu-id="7146d-195">若要建立 Skillport 測試使用者，您需要連絡 [Skillport 支援小組](https://www.skillsoft.com/contact.asp)，因為他們可根據終端使用者的需求，提供多種商務案例。</span><span class="sxs-lookup"><span data-stu-id="7146d-195">In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user.</span></span> <span data-ttu-id="7146d-196">他們會在與使用者討論之後進行設定。</span><span class="sxs-lookup"><span data-stu-id="7146d-196">They will configure it after discussion with the users.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7146d-197">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7146d-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7146d-198">在本節中，您會將 Skillport 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7146d-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.</span></span>

![指派使用者][200] 

<span data-ttu-id="7146d-200">**若要將 Britta Simon 指派給 Skillport，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7146d-200">**To assign Britta Simon to Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="7146d-201">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7146d-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7146d-203">在應用程式清單中，選取 [Skillport]。</span><span class="sxs-lookup"><span data-stu-id="7146d-203">In the applications list, select **Skillport**.</span></span>

    ![設定單一登入](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="7146d-205">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7146d-205">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7146d-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7146d-207">Click **Add** button.</span></span> <span data-ttu-id="7146d-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7146d-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7146d-210">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7146d-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7146d-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7146d-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7146d-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7146d-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7146d-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7146d-213">Testing single sign-on</span></span>

<span data-ttu-id="7146d-214">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="7146d-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7146d-215">當您在 [存取面板] 中按一下 [Skillport] 圖格時，應該會自動登入您的 Skillport 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7146d-215">When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.</span></span>
<span data-ttu-id="7146d-216">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="7146d-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7146d-217">其他資源</span><span class="sxs-lookup"><span data-stu-id="7146d-217">Additional resources</span></span>

* [<span data-ttu-id="7146d-218">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7146d-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7146d-219">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7146d-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

