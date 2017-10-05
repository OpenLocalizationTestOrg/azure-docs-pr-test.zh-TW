---
title: "教學課程：Azure Active Directory 與 Adaptive Suite 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Adaptive Suite 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 5d7ba2f4c7d814e3aaa1bf804ddc5030380ccb2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a><span data-ttu-id="7d6be-103">教學課程：Azure Active Directory 與 Adaptive Suite 整合</span><span class="sxs-lookup"><span data-stu-id="7d6be-103">Tutorial: Azure Active Directory integration with Adaptive Suite</span></span>

<span data-ttu-id="7d6be-104">在本教學課程中，您將了解如何整合 Adaptive Suite 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7d6be-104">In this tutorial, you learn how to integrate Adaptive Suite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d6be-105">Adaptive Suite 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7d6be-105">Integrating Adaptive Suite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7d6be-106">您可以在 Azure AD 中控制可存取 Adaptive Suite 的人員</span><span class="sxs-lookup"><span data-stu-id="7d6be-106">You can control in Azure AD who has access to Adaptive Suite</span></span>
- <span data-ttu-id="7d6be-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Adaptive Suite (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7d6be-107">You can enable your users to automatically get signed-on to Adaptive Suite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d6be-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7d6be-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7d6be-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7d6be-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d6be-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7d6be-110">Prerequisites</span></span>

<span data-ttu-id="7d6be-111">若要設定 Azure AD 與 Adaptive Suite 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7d6be-111">To configure Azure AD integration with Adaptive Suite, you need the following items:</span></span>

- <span data-ttu-id="7d6be-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7d6be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d6be-113">啟用 Adaptive Suite 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7d6be-113">An Adaptive Suite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d6be-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7d6be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d6be-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7d6be-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d6be-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7d6be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d6be-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="7d6be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d6be-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7d6be-118">Scenario description</span></span>
<span data-ttu-id="7d6be-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d6be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d6be-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7d6be-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d6be-121">從資源庫新增 Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="7d6be-121">Adding Adaptive Suite from the gallery</span></span>
2. <span data-ttu-id="7d6be-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7d6be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adaptive-suite-from-the-gallery"></a><span data-ttu-id="7d6be-123">從資源庫新增 Adaptive Suite</span><span class="sxs-lookup"><span data-stu-id="7d6be-123">Adding Adaptive Suite from the gallery</span></span>
<span data-ttu-id="7d6be-124">若要設定 Adaptive Suite 與 Azure AD 整合，您需要從資源庫將 Adaptive Suite 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7d6be-124">To configure the integration of Adaptive Suite into Azure AD, you need to add Adaptive Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7d6be-125">**若要從資源庫新增 Adaptive Suite，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d6be-125">**To add Adaptive Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7d6be-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7d6be-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d6be-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7d6be-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="7d6be-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d6be-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="7d6be-133">在搜尋方塊中，鍵入 **Adaptive Suite**。</span><span class="sxs-lookup"><span data-stu-id="7d6be-133">In the search box, type **Adaptive Suite**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. <span data-ttu-id="7d6be-135">在結果窗格中，選取 [Adaptive Suite]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d6be-135">In the results panel, select **Adaptive Suite**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d6be-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7d6be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d6be-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Adaptive Suite 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d6be-138">In this section, you configure and test Azure AD single sign-on with Adaptive Suite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7d6be-139">若要讓單一登入運作，Azure AD 必須知道 Adaptive Suite 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7d6be-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adaptive Suite is to a user in Azure AD.</span></span> <span data-ttu-id="7d6be-140">換句話說，必須在 Azure AD 使用者和 Adaptive Suite 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7d6be-140">In other words, a link relationship between an Azure AD user and the related user in Adaptive Suite needs to be established.</span></span>

<span data-ttu-id="7d6be-141">在 Adaptive Suite 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7d6be-141">In Adaptive Suite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7d6be-142">若要設定及測試與 Adaptive Suite 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="7d6be-142">To configure and test Azure AD single sign-on with Adaptive Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7d6be-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7d6be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7d6be-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d6be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d6be-145">**[建立 Adaptive Suite 測試使用者](#creating-an-adaptive-suite-test-user)** - 在 Adaptive Suite 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="7d6be-145">**[Creating an Adaptive Suite test user](#creating-an-adaptive-suite-test-user)** - to have a counterpart of Britta Simon in Adaptive Suite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d6be-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d6be-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d6be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7d6be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d6be-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7d6be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d6be-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Adaptive Suite 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d6be-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adaptive Suite application.</span></span>

<span data-ttu-id="7d6be-150">**若要設定與 Adaptive Suite 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d6be-150">**To configure Azure AD single sign-on with Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7d6be-151">在 Azure 入口網站的 [Adaptive Suite] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-151">In the Azure portal, on the **Adaptive Suite** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7d6be-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d6be-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. <span data-ttu-id="7d6be-155">在 [Adaptive Suite 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d6be-155">On the **Adaptive Suite Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    <span data-ttu-id="7d6be-157">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span><span class="sxs-lookup"><span data-stu-id="7d6be-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://login.adaptiveinsights.com:443/samlsso/<unique-id>`</span></span>

    >[!NOTE]
    > <span data-ttu-id="7d6be-158">您可以從 Adaptive Suite 的 [SAML SSO 設定] 頁面取得這個值。</span><span class="sxs-lookup"><span data-stu-id="7d6be-158">You can get this value from the Adaptive Suite’s **SAML SSO Settings** page.</span></span>
    >  

4. <span data-ttu-id="7d6be-159">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="7d6be-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. <span data-ttu-id="7d6be-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d6be-161">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7d6be-163">在 [Adaptive Suite 設定] 區段上，按一下 [設定 Adaptive Suite] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="7d6be-163">On the **Adaptive Suite Configuration** section, click **Configure Adaptive Suite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7d6be-164">從 [快速參考] 區段中複製 [SAML 實體識別碼] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. <span data-ttu-id="7d6be-166">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Adaptive Suite 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7d6be-166">In a different web browser window, log in to your Adaptive Suite company site as an administrator.</span></span>

8. <span data-ttu-id="7d6be-167">移至 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="7d6be-167">Go to **Admin**.</span></span>
   
    <span data-ttu-id="7d6be-168">![管理](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "管理")</span><span class="sxs-lookup"><span data-stu-id="7d6be-168">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>

9. <span data-ttu-id="7d6be-169">在 [使用者和角色] 區段中，按一下 [管理 SAML SSO 設定]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-169">In the **Users and Roles** section, click **Manage SAML SSO Settings**.</span></span>
   
    <span data-ttu-id="7d6be-170">![管理 SAML SSO 設定](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "管理 SAML SSO 設定")</span><span class="sxs-lookup"><span data-stu-id="7d6be-170">![Manage SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Manage SAML SSO Settings")</span></span>

10. <span data-ttu-id="7d6be-171">在 [SAML SSO 設定]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d6be-171">On the **SAML SSO Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="7d6be-172">![SAML SSO 設定](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO 設定")</span><span class="sxs-lookup"><span data-stu-id="7d6be-172">![SAML SSO Settings](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "SAML SSO Settings")</span></span>

    <span data-ttu-id="7d6be-173">a.</span><span class="sxs-lookup"><span data-stu-id="7d6be-173">a.</span></span> <span data-ttu-id="7d6be-174">在 [識別提供者名稱]  文字方塊中，輸入您組態的名稱。</span><span class="sxs-lookup"><span data-stu-id="7d6be-174">In the **Identity provider name** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="7d6be-175">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d6be-175">b.</span></span> <span data-ttu-id="7d6be-176">將從 Azure 入口網站複製的 [SAML 實體識別碼] 值貼到 [識別提供者實體識別碼] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7d6be-176">Paste the **SAML Entity ID** value copied from Azure portal into the **Identity provider Entity ID** textbox.</span></span>
  
    <span data-ttu-id="7d6be-177">c.</span><span class="sxs-lookup"><span data-stu-id="7d6be-177">c.</span></span> <span data-ttu-id="7d6be-178">將從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值貼到 [識別提供者 SSO URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7d6be-178">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Identity provider SSO URL** textbox.</span></span>
  
    <span data-ttu-id="7d6be-179">d.</span><span class="sxs-lookup"><span data-stu-id="7d6be-179">d.</span></span> <span data-ttu-id="7d6be-180">將從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值貼到 [自訂登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7d6be-180">Paste the **SAML Single Sign-On Service URL** value copied from Azure portal into the **Custom logout URL** textbox.</span></span>
  
    <span data-ttu-id="7d6be-181">e.</span><span class="sxs-lookup"><span data-stu-id="7d6be-181">e.</span></span> <span data-ttu-id="7d6be-182">若要上傳您下載的憑證，請按一下 [選擇檔案] 。</span><span class="sxs-lookup"><span data-stu-id="7d6be-182">To upload your downloaded certificate, click **Choose file**.</span></span>
  
    <span data-ttu-id="7d6be-183">f.</span><span class="sxs-lookup"><span data-stu-id="7d6be-183">f.</span></span> <span data-ttu-id="7d6be-184">選取下列選項：</span><span class="sxs-lookup"><span data-stu-id="7d6be-184">Select the following, for:</span></span>
    * <span data-ttu-id="7d6be-185">針對 [SAML 使用者識別碼]，選取 [使用者的 Adaptive Insights 使用者名稱]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-185">**SAML user id**, select **User’s Adaptive Insights user name**.</span></span>
    * <span data-ttu-id="7d6be-186">針對 [SAML 使用者識別碼位置]，選取 [主旨 NameID 中的使用者識別碼]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-186">**SAML user id location**, select **User id in NameID of Subject**.</span></span>
    * <span data-ttu-id="7d6be-187">針對 [SAML NameID 格式]，選取 [電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-187">**SAML NameID format**, select **Email address**.</span></span>
    * <span data-ttu-id="7d6be-188">針對 [啟用 SAML]，選取 [允許 SAML SSO 和直接 Adaptive Insights 登入]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-188">**Enable SAML**, select **Allow SAML SSO and direct Adaptive Insights login**.</span></span>
    
    <span data-ttu-id="7d6be-189">g.</span><span class="sxs-lookup"><span data-stu-id="7d6be-189">g.</span></span> <span data-ttu-id="7d6be-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7d6be-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7d6be-191">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7d6be-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7d6be-192">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7d6be-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7d6be-193">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d6be-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d6be-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7d6be-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d6be-195">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7d6be-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="7d6be-197">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d6be-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7d6be-198">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7d6be-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d6be-200">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d6be-202">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d6be-204">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d6be-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d6be-206">a.</span><span class="sxs-lookup"><span data-stu-id="7d6be-206">a.</span></span> <span data-ttu-id="7d6be-207">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7d6be-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d6be-208">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d6be-208">b.</span></span> <span data-ttu-id="7d6be-209">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7d6be-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d6be-210">c.</span><span class="sxs-lookup"><span data-stu-id="7d6be-210">c.</span></span> <span data-ttu-id="7d6be-211">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7d6be-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7d6be-212">d.</span><span class="sxs-lookup"><span data-stu-id="7d6be-212">d.</span></span> <span data-ttu-id="7d6be-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7d6be-213">Click **Create**.</span></span>
 
### <a name="creating-an-adaptive-suite-test-user"></a><span data-ttu-id="7d6be-214">建立 Adaptive Suite 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7d6be-214">Creating an Adaptive Suite test user</span></span>

<span data-ttu-id="7d6be-215">若要讓 Azure AD 使用者能夠登入 Adaptive Suite，必須將他們佈建到 Adaptive Suite。</span><span class="sxs-lookup"><span data-stu-id="7d6be-215">To enable Azure AD users to log in to Adaptive Suite, they must be provisioned into Adaptive Suite.</span></span>  

* <span data-ttu-id="7d6be-216">Adaptive Suite 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="7d6be-216">In the case of Adaptive Suite, provisioning is a manual task.</span></span>

<span data-ttu-id="7d6be-217">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d6be-217">**To configure user provisioning, perform the following steps:**</span></span> 

1. <span data-ttu-id="7d6be-218">以系統管理員身分登入您的 **Adaptive Suite** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7d6be-218">Log in to your **Adaptive Suite** company site as an administrator.</span></span>
2. <span data-ttu-id="7d6be-219">移至 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="7d6be-219">Go to **Admin**.</span></span>
   
   <span data-ttu-id="7d6be-220">![管理](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "管理")</span><span class="sxs-lookup"><span data-stu-id="7d6be-220">![Admin](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Admin")</span></span>
3. <span data-ttu-id="7d6be-221">在 [使用者和角色] 區段中，按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-221">In the **Users and Roles** section, click **Add User**.</span></span>
   
   <span data-ttu-id="7d6be-222">![新增使用者](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="7d6be-222">![Add User](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Add User")</span></span>
4. <span data-ttu-id="7d6be-223">在 [新增使用者]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7d6be-223">In the **New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="7d6be-224">![提交](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "提交")</span><span class="sxs-lookup"><span data-stu-id="7d6be-224">![Submit](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Submit")</span></span>   

   <span data-ttu-id="7d6be-225">a.</span><span class="sxs-lookup"><span data-stu-id="7d6be-225">a.</span></span> <span data-ttu-id="7d6be-226">在相關的文字方塊中，輸入您想要佈建之有效 Azure Active Directory 使用者的 [名稱]、[登入]、[電子郵件]、[密碼]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-226">Type the **Name**, **Login**, **Email**, **Password** of a valid Azure Active Directory user you want to provision into the related textboxes.</span></span>
  
   <span data-ttu-id="7d6be-227">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d6be-227">b.</span></span> <span data-ttu-id="7d6be-228">選取 [角色] 。</span><span class="sxs-lookup"><span data-stu-id="7d6be-228">Select a **Role**.</span></span>
  
   <span data-ttu-id="7d6be-229">c.</span><span class="sxs-lookup"><span data-stu-id="7d6be-229">c.</span></span> <span data-ttu-id="7d6be-230">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="7d6be-230">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="7d6be-231">您可以使用任何其他的 Adaptive Suite 使用者帳戶建立工具或 Adaptive Suite 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7d6be-231">You can use any other Adaptive Suite user account creation tools or APIs provided by Adaptive Suite to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7d6be-232">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7d6be-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7d6be-233">在本節中，您會將 Adaptive Suite 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7d6be-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adaptive Suite.</span></span>

![指派使用者][200] 

<span data-ttu-id="7d6be-235">**若要將 Britta Simon 指派給 Adaptive Suite，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7d6be-235">**To assign Britta Simon to Adaptive Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="7d6be-236">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7d6be-238">在應用程式清單中，選取 [Adaptive Suite]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-238">In the applications list, select **Adaptive Suite**.</span></span>

    ![設定單一登入](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. <span data-ttu-id="7d6be-240">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-240">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="7d6be-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d6be-242">Click **Add** button.</span></span> <span data-ttu-id="7d6be-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="7d6be-245">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7d6be-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7d6be-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d6be-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d6be-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7d6be-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7d6be-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7d6be-248">Testing single sign-on</span></span>

<span data-ttu-id="7d6be-249">本節的目標是要使用「存取面板」來測試您的 Microsoft Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="7d6be-249">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="7d6be-250">當您在存取面板中按一下 [Adaptive Suite] 磚時，應該會自動登入您的 Adaptive Suite 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d6be-250">When you click the Adaptive Suite tile in the Access Panel, you should get automatically signed-on to your Adaptive Suite application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7d6be-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="7d6be-251">Additional resources</span></span>

* [<span data-ttu-id="7d6be-252">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7d6be-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d6be-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7d6be-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png
