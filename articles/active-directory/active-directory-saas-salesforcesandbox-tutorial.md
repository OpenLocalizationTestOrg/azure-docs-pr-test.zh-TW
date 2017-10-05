---
title: "教學課程：Azure Active Directory 與 Salesforce 沙箱整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Salesforce Sandbox 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a><span data-ttu-id="7b9f6-103">教學課程：Azure Active Directory 與 Salesforce 沙箱整合</span><span class="sxs-lookup"><span data-stu-id="7b9f6-103">Tutorial: Azure Active Directory integration with Salesforce Sandbox</span></span>

<span data-ttu-id="7b9f6-104">在本教學課程中，您會了解如何整合 Salesforce Sandbox 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-104">In this tutorial, you learn how to integrate Salesforce Sandbox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b9f6-105">Salesforce Sandbox 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7b9f6-105">Integrating Salesforce Sandbox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7b9f6-106">您可以在 Azure AD 中控制可存取 Salesforce Sandbox 的人員</span><span class="sxs-lookup"><span data-stu-id="7b9f6-106">You can control in Azure AD who has access to Salesforce Sandbox</span></span>
- <span data-ttu-id="7b9f6-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Salesforce Sandbox (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7b9f6-107">You can enable your users to automatically get signed-on to Salesforce Sandbox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b9f6-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7b9f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7b9f6-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b9f6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b9f6-110">Prerequisites</span></span>

<span data-ttu-id="7b9f6-111">若要設定 Azure AD 與 Salesforce Sandbox 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7b9f6-111">To configure Azure AD integration with Salesforce Sandbox, you need the following items:</span></span>

- <span data-ttu-id="7b9f6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7b9f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b9f6-113">啟用 Salesforce Sandbox 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7b9f6-113">A Salesforce Sandbox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b9f6-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b9f6-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7b9f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b9f6-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b9f6-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b9f6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7b9f6-118">Scenario description</span></span>
<span data-ttu-id="7b9f6-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b9f6-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7b9f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b9f6-121">從資源庫新增 Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="7b9f6-121">Adding Salesforce Sandbox from the gallery</span></span>
2. <span data-ttu-id="7b9f6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7b9f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-sandbox-from-the-gallery"></a><span data-ttu-id="7b9f6-123">從資源庫新增 Salesforce Sandbox</span><span class="sxs-lookup"><span data-stu-id="7b9f6-123">Adding Salesforce Sandbox from the gallery</span></span>
<span data-ttu-id="7b9f6-124">若要設定將 Salesforce Sandbox 整合到 Azure AD 中，您需要從資源庫將 Salesforce Sandbox 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-124">To configure the integration of Salesforce Sandbox into Azure AD, you need to add Salesforce Sandbox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7b9f6-125">**若要從資源庫新增 Salesforce Sandbox，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7b9f6-125">**To add Salesforce Sandbox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7b9f6-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7b9f6-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7b9f6-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7b9f6-131">按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-131">Click **New application** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7b9f6-133">在搜尋方塊中，輸入 **Salesforce Sandbox**。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-133">In the search box, type **Salesforce Sandbox**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. <span data-ttu-id="7b9f6-135">在結果面板中，選取 [Salesforce Sandbox]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-135">In the results panel, select **Salesforce Sandbox**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b9f6-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7b9f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b9f6-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Salesforce Sandbox 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-138">In this section, you configure and test Azure AD single sign-on with Salesforce Sandbox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7b9f6-139">若要讓單一登入運作，Azure AD 必須知道 Salesforce Sandbox 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce Sandbox is to a user in Azure AD.</span></span> <span data-ttu-id="7b9f6-140">換句話說，必須在 Azure AD 使用者和 Salesforce Sandbox 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce Sandbox needs to be established.</span></span>

<span data-ttu-id="7b9f6-141">建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 Salesforce Sandbox 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce Sandbox.</span></span>

<span data-ttu-id="7b9f6-142">若要設定及測試與 Salesforce Sandbox 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7b9f6-142">To configure and test Azure AD single sign-on with Salesforce Sandbox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7b9f6-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7b9f6-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b9f6-145">**[建立 Salesforce Sandbox 測試使用者](#creating-a-salesforce-sandbox-test-user)** - 使 Salesforce Sandbox 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-145">**[Creating a Salesforce Sandbox test user](#creating-a-salesforce-sandbox-test-user)** - to have a counterpart of Britta Simon in Salesforce Sandbox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b9f6-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b9f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b9f6-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7b9f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b9f6-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Salesforce Sandbox 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce Sandbox application.</span></span>

<span data-ttu-id="7b9f6-150">**若要與 Salesforce Sandbox 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7b9f6-150">**To configure Azure AD single sign-on with Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="7b9f6-151">在 Azure 入口網站的 [Salesforce Sandbox] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-151">In the Azure portal, on the **Salesforce Sandbox** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7b9f6-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. <span data-ttu-id="7b9f6-155">在 [Salesforce Sandbox 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7b9f6-155">On the **Salesforce Sandbox Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     <span data-ttu-id="7b9f6-157">在 [登入 URL] 文字方塊中，以下列模式輸入值：`https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7b9f6-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<subdomain>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7b9f6-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-158">This value is not the real.</span></span> <span data-ttu-id="7b9f6-159">請使用實際的登入 URL 來更新此值。請連絡 [Salesforce Sandbox 客戶支援小組](https://help.salesforce.com/support)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-159">Update this value with the actual Sign-on URL.Contact [Salesforce Sandbox Client support team](https://help.salesforce.com/support) to get this value.</span></span>


4. <span data-ttu-id="7b9f6-160">如果您已為目錄中的另一個 Salesforce 沙箱執行個體設定單一登入，則也須將**識別碼**設定為具有與**登入 URL** 相同的值。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-160">If you have already configured single sign-on for another Salesforce Sandbox instance in your directory, then you must also configure the **Identifier** to have the same value as the **Sign on URL**.</span></span> 
    
    >[!Note]
    ><span data-ttu-id="7b9f6-161">您可以在對話方塊的 [設定應用程式 URL] 頁面上，勾選 [顯示進階設定] 核取方塊，就會出現 [識別碼] 欄位。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-161">The **Identifier** field can be found by checking the **Show advanced settings** checkbox on the **Configure App URL** page of the dialog</span></span> 


5. <span data-ttu-id="7b9f6-162">在 [SAML 簽署憑證] 區段上，按一下 [憑證]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-162">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. <span data-ttu-id="7b9f6-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-164">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="7b9f6-166">在 [Salesforce Sandbox 組態] 區段上，按一下 [設定 Salesforce Sandbox] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-166">On the **Salesforce Sandbox Configuration** section, click **Configure Salesforce Sandbox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7b9f6-167">從 [快速參考] 區段中複製 [SAML 實體 ID 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-167">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="7b9f6-168">![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="7b9f6-168">![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS></span></span>
8. <span data-ttu-id="7b9f6-169">在瀏覽器中開啟新索引標籤，登入您的 Salesforce Sandbox 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-169">Open a new tab in your browser and log in to your Salesforce Sandbox administrator account.</span></span>

9. <span data-ttu-id="7b9f6-170">在頂端的功能表中，按一下 [安裝] 。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-170">In the menu on the top, click **Setup**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. <span data-ttu-id="7b9f6-172">在左側的導覽窗格中，按一下 [安全性控制項]，然後按一下 [單一登入設定]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-172">In the navigation pane on the left, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. <span data-ttu-id="7b9f6-174">在 [單一登入設定] 區段中，執行下列步驟：![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span><span class="sxs-lookup"><span data-stu-id="7b9f6-174">On the Single Sign-On Settings section, perform the following steps:  ![Configure Single Sign-On](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)</span></span>
     
     <span data-ttu-id="7b9f6-175">a.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-175">a.</span></span>  <span data-ttu-id="7b9f6-176">選取 [已啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-176">Select **SAML Enabled**.</span></span> 

     <span data-ttu-id="7b9f6-177">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-177">b.</span></span>  <span data-ttu-id="7b9f6-178">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-178">Click **New**.</span></span>

12. <span data-ttu-id="7b9f6-179">在 [SAML 單一登入設定] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7b9f6-179">On the SAML Single Sign-On Settings section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    <span data-ttu-id="7b9f6-181">a.在 [名稱] 文字方塊中，輸入組態的名稱 (例如：*SPSSOWAAD\_Test*)。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-181">a.In the Name textbox, type the name of the configuration (e.g.: *SPSSOWAAD\_Test*).</span></span> 

    <span data-ttu-id="7b9f6-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-182">b.</span></span> <span data-ttu-id="7b9f6-183">將 [SMAL 實體識別碼] 值貼到 [簽發者] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-183">Paste **SMAL Entity ID** value into the **Issuer** textbox.</span></span>

    <span data-ttu-id="7b9f6-184">c.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-184">c.</span></span> <span data-ttu-id="7b9f6-185">如果這是您要新增至目錄的第一個 Salesforce Sandbox 執行個體，請在 [實體識別碼] 文字方塊中，輸入 **https://test.salesforce.com**。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-185">In the **Entity Id** textbox, type **https://test.salesforce.com** if it is the first Salesforce Sandbox instance that you are adding to your directory.</span></span> <span data-ttu-id="7b9f6-186">如果您已新增 Salesforce 沙箱的執行個體，請對 [實體識別碼] 輸入**登入 URL**，其格式如下：`http://company.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="7b9f6-186">If you have already added an instance of Salesforce Sandbox, then for the **Entity ID** type in the **Sign On URL**, which should be in this format: `http://company.my.salesforce.com`</span></span>  
 
    <span data-ttu-id="7b9f6-187">d.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-187">d.</span></span> <span data-ttu-id="7b9f6-188">按一下 [瀏覽] 來上傳已下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-188">Click **Browse** to upload the downloaded certificate.</span></span>  

    <span data-ttu-id="7b9f6-189">e.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-189">e.</span></span> <span data-ttu-id="7b9f6-190">對於 [SAML 身分識別類型]，選取 [判斷提示包含來自使用者物件的同盟識別碼]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-190">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
 
    <span data-ttu-id="7b9f6-191">f.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-191">f.</span></span> <span data-ttu-id="7b9f6-192">對於 [SAML 身分識別位置]，選取 [身分識別位於 Subject 陳述式的 NameIdentifier 元素中]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-192">As **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**.</span></span>

    <span data-ttu-id="7b9f6-193">g.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-193">g.</span></span> <span data-ttu-id="7b9f6-194">將 [單一登入服務 URL] 貼到 [識別提供者登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-194">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** textbox.</span></span> 

    <span data-ttu-id="7b9f6-195">h.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-195">h.</span></span> <span data-ttu-id="7b9f6-196">SFDC 不支援 SAML 登出。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-196">SFDC does not support SAML logout.</span></span>  <span data-ttu-id="7b9f6-197">解決方法是在 [識別提供者登出 URL] 文字方塊中貼上 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0'。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-197">As a workaround, paste 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' it into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="7b9f6-198">i.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-198">i.</span></span> <span data-ttu-id="7b9f6-199">在 [服務提供者起始的要求繫結]，選取 [HTTP POST]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-199">As **Service Provider Initiated Request Binding**, select **HTTP POST**.</span></span> 

    <span data-ttu-id="7b9f6-200">j.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-200">j.</span></span> <span data-ttu-id="7b9f6-201">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-201">Click **Save**.</span></span>

### <a name="enable-your-domain"></a><span data-ttu-id="7b9f6-202">啟用網域</span><span class="sxs-lookup"><span data-stu-id="7b9f6-202">Enable your domain</span></span>
<span data-ttu-id="7b9f6-203">本節假設您已經建立了一個網域。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-203">This section assumes that you already have created a domain.</span></span>  <span data-ttu-id="7b9f6-204">如需詳細資訊，請參閱[定義您的網域名稱](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-204">For more information, see [Defining Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).</span></span>

<span data-ttu-id="7b9f6-205">**若要啟用您的網域，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7b9f6-205">**To enable your domain, perform the following steps:**</span></span>

1. <span data-ttu-id="7b9f6-206">在左邊的導覽窗格中按一下 [網域管理]，然後按一下 [我的網域]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-206">In the left navigation pane, click **Domain Management**, and then click **My Domain.**</span></span>
   
     ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   ><span data-ttu-id="7b9f6-208">請確定您的網域已正確設定。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-208">Please make sure that your domain has been configured correctly.</span></span> 

2. <span data-ttu-id="7b9f6-209">在 [登入頁面設定] 區段中，按一下 [編輯]，然後對於 [驗證服務]，選取來自前一區段 SAML 單一登入設定的名稱，最後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-209">In the **Login Page Settings** section, click **Edit**, then, as **Authentication Service**, select the name of the SAML Single Sign-On Setting from the previous section, and finally click **Save**.</span></span>
   
   ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

<span data-ttu-id="7b9f6-211">一旦您設定了網域，您的使用者便應使用該網域 URL 登入至 Salesforce 沙箱。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-211">As soon as you have a domain configured, your users should use the domain URL to login to the Salesforce sandbox.</span></span>  

<span data-ttu-id="7b9f6-212">若要取得 URL 的值，請按一下您在上一區段中所建立的 SSO 設定檔。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-212">To get the value of the URL, click the SSO profile you have created in the previous section.</span></span>    

> [!TIP]
> <span data-ttu-id="7b9f6-213">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7b9f6-213">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7b9f6-214">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-214">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7b9f6-215">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b9f6-215">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b9f6-216">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7b9f6-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b9f6-217">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7b9f6-219">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7b9f6-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7b9f6-220">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b9f6-222">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-222">to display the list of users go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b9f6-224">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-224">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b9f6-226">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7b9f6-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b9f6-228">a.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-228">a.</span></span> <span data-ttu-id="7b9f6-229">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b9f6-230">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-230">b.</span></span> <span data-ttu-id="7b9f6-231">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7b9f6-232">c.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-232">c.</span></span> <span data-ttu-id="7b9f6-233">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7b9f6-234">d.</span><span class="sxs-lookup"><span data-stu-id="7b9f6-234">d.</span></span> <span data-ttu-id="7b9f6-235">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-235">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-sandbox-test-user"></a><span data-ttu-id="7b9f6-236">建立 Salesforce Sandbox 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7b9f6-236">Creating a Salesforce Sandbox test user</span></span>

<span data-ttu-id="7b9f6-237">本節會在 Salesforce Sandbox 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-237">In this section, a user called Britta Simon is created in Salesforce Sandbox.</span></span> <span data-ttu-id="7b9f6-238">Salesforce Sandbox 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-238">Salesforce Sandbox supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="7b9f6-239">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-239">There is no action item for you in this section.</span></span> <span data-ttu-id="7b9f6-240">如果 Salesforce Sandbox 中還沒有使用者，當您嘗試存取 Salesforce Sandbox 時，就會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-240">If a user doesn't already exist in Salesforce Sandbox, a new one is created when you attempt to access Salesforce Sandbox.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7b9f6-241">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7b9f6-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7b9f6-242">在本節中，您會將 Salesforce Sandbox 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce Sandbox.</span></span>

![指派使用者][200] 

<span data-ttu-id="7b9f6-244">**若要將 Britta Simon 指派給 Salesforce Sandbox，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7b9f6-244">**To assign Britta Simon to Salesforce Sandbox, perform the following steps:**</span></span>

1. <span data-ttu-id="7b9f6-245">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7b9f6-247">在應用程式清單中，選取 [Salesforce Sandbox]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-247">In the applications list, select **Salesforce Sandbox**.</span></span>

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. <span data-ttu-id="7b9f6-249">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-249">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7b9f6-251">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-251">Click **Add** button.</span></span> <span data-ttu-id="7b9f6-252">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7b9f6-254">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7b9f6-255">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b9f6-256">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b9f6-257">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7b9f6-257">Testing single sign-on</span></span>

<span data-ttu-id="7b9f6-258">如果要測試您的 SSO 設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-258">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="7b9f6-259">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7b9f6-259">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b9f6-260">其他資源</span><span class="sxs-lookup"><span data-stu-id="7b9f6-260">Additional resources</span></span>

* [<span data-ttu-id="7b9f6-261">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7b9f6-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b9f6-262">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7b9f6-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="7b9f6-263">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="7b9f6-263">Configure User Provisioning</span></span>](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

