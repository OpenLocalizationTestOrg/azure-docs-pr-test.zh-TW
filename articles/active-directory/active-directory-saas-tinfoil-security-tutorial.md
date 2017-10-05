---
title: "教學課程：Azure Active Directory 與 TINFOIL SECURITY 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 TINFOIL SECURITY 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 614e4de3335574f4b56c7d641af4fcfafdb17d12
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a><span data-ttu-id="5b0f7-103">教學課程：Azure Active Directory 與 TINFOIL SECURITY 整合</span><span class="sxs-lookup"><span data-stu-id="5b0f7-103">Tutorial: Azure Active Directory integration with TINFOIL SECURITY</span></span>

<span data-ttu-id="5b0f7-104">在本教學課程中，您會了解如何將 TINFOIL SECURITY 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-104">In this tutorial, you learn how to integrate TINFOIL SECURITY with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b0f7-105">將 TINFOIL SECURITY 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="5b0f7-105">Integrating TINFOIL SECURITY with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b0f7-106">您可以在 Azure AD 中控制可存取 TINFOIL SECURITY 的人員</span><span class="sxs-lookup"><span data-stu-id="5b0f7-106">You can control in Azure AD who has access to TINFOIL SECURITY</span></span>
- <span data-ttu-id="5b0f7-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 TINFOIL SECURITY (單一登入)</span><span class="sxs-lookup"><span data-stu-id="5b0f7-107">You can enable your users to automatically get signed-on to TINFOIL SECURITY (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b0f7-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="5b0f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5b0f7-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b0f7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5b0f7-110">Prerequisites</span></span>

<span data-ttu-id="5b0f7-111">若要設定 Azure AD 與 TINFOIL SECURITY 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5b0f7-111">To configure Azure AD integration with TINFOIL SECURITY, you need the following items:</span></span>

- <span data-ttu-id="5b0f7-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5b0f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b0f7-113">已啟用 TINFOIL SECURITY 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5b0f7-113">A TINFOIL SECURITY single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5b0f7-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5b0f7-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5b0f7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b0f7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5b0f7-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5b0f7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5b0f7-118">Scenario description</span></span>
<span data-ttu-id="5b0f7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b0f7-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="5b0f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b0f7-121">從資源庫新增 TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="5b0f7-121">Add TINFOIL SECURITY from the gallery</span></span>
2. <span data-ttu-id="5b0f7-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5b0f7-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tinfoil-security-from-the-gallery"></a><span data-ttu-id="5b0f7-123">從資源庫新增 TINFOIL SECURITY</span><span class="sxs-lookup"><span data-stu-id="5b0f7-123">Add TINFOIL SECURITY from the gallery</span></span>
<span data-ttu-id="5b0f7-124">如要設定將 TINFOIL SECURITY 整合到 Azure AD 中，您需要從資源庫將 TINFOIL SECURITY 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-124">To configure the integration of TINFOIL SECURITY into Azure AD, you need to add TINFOIL SECURITY from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b0f7-125">**若要從資源庫新增 TINFOIL SECURITY，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5b0f7-125">**To add TINFOIL SECURITY from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b0f7-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b0f7-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b0f7-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="5b0f7-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="5b0f7-133">在搜尋方塊中，輸入 **TINFOIL SECURITY**，從結果面板中選取 [TINFOIL SECURITY]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-133">In the search box, type **TINFOIL SECURITY**, select  **TINFOIL SECURITY** from result panel then click **Add** button to add the application.</span></span>

    ![來自資源庫的 TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5b0f7-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5b0f7-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="5b0f7-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 TINFOIL SECURITY 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-136">In this section, you configure and test Azure AD single sign-on with TINFOIL SECURITY based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b0f7-137">若要讓單一登入能夠運作，Azure AD 必須知道 TINFOIL SECURITY 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TINFOIL SECURITY is to a user in Azure AD.</span></span> <span data-ttu-id="5b0f7-138">換句話說，必須要建立某位 Azure AD 使用者與 TINFOIL SECURITY 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-138">In other words, a link relationship between an Azure AD user and the related user in TINFOIL SECURITY needs to be established.</span></span>

<span data-ttu-id="5b0f7-139">在 TINFOIL SECURITY 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-139">In TINFOIL SECURITY, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5b0f7-140">若要設定及測試與 TINFOIL SECURITY 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5b0f7-140">To configure and test Azure AD single sign-on with TINFOIL SECURITY, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b0f7-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5b0f7-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b0f7-143">**[建立 TINFOIL SECURITY 測試使用者](#create-a-tinfoil-security-test-user)** - 使 TINFOIL SECURITY 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-143">**[Create a TINFOIL SECURITY test user](#create-a-tinfoil-security-test-user)** - to have a counterpart of Britta Simon in TINFOIL SECURITY that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5b0f7-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b0f7-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5b0f7-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5b0f7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5b0f7-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 TINFOIL SECURITY 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TINFOIL SECURITY application.</span></span>

<span data-ttu-id="5b0f7-148">**若要使用 TINFOIL SECURITY 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5b0f7-148">**To configure Azure AD single sign-on with TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="5b0f7-149">在 Azure 入口網站的 [TINFOIL SECURITY] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-149">In the Azure portal, on the **TINFOIL SECURITY** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="5b0f7-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. <span data-ttu-id="5b0f7-153">在 [TINFOIL SECURITY 網域和 URL] 區段中，使用者不需要執行任何步驟，因為應用程式已預先與 Azure 整合。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-153">On the **TINFOIL SECURITY Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. <span data-ttu-id="5b0f7-155">在 [SAML 簽署憑證] 區段上，複製 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-155">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. <span data-ttu-id="5b0f7-157">若要加入必要的屬性對應，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b0f7-157">To add the required attribute mappings, perform the following steps:</span></span>
    
    <span data-ttu-id="5b0f7-158">![屬性](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="5b0f7-158">![Attributes](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Attributes")</span></span>
    
    | <span data-ttu-id="5b0f7-159">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="5b0f7-159">Attribute Name</span></span>    |   <span data-ttu-id="5b0f7-160">屬性值</span><span class="sxs-lookup"><span data-stu-id="5b0f7-160">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="5b0f7-161">accountid</span><span class="sxs-lookup"><span data-stu-id="5b0f7-161">accountid</span></span> | <span data-ttu-id="5b0f7-162">UXXXXXXXXXXXXX</span><span class="sxs-lookup"><span data-stu-id="5b0f7-162">UXXXXXXXXXXXXX</span></span> |
    
    <span data-ttu-id="5b0f7-163">a.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-163">a.</span></span> <span data-ttu-id="5b0f7-164">按一下 [加入使用者屬性] 。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-164">Click **add user attribute**.</span></span>
    
    <span data-ttu-id="5b0f7-165">![新增屬性](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="5b0f7-165">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Attributes")</span></span>
    
    <span data-ttu-id="5b0f7-166">![新增屬性](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="5b0f7-166">![ADD Attribute](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Attributes")</span></span>
    
    <span data-ttu-id="5b0f7-167">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-167">b.</span></span> <span data-ttu-id="5b0f7-168">在 [屬性名稱] 文字方塊中，輸入 **accountid**。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-168">In the **Attribute Name** textbox, type **accountid**.</span></span>
    
    <span data-ttu-id="5b0f7-169">c.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-169">c.</span></span> <span data-ttu-id="5b0f7-170">在 [屬性值] 文字方塊中，貼上您會在本教學課程稍後取得的帳戶識別碼值。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-170">In the **Attribute Value** textbox, paste the account ID value which you will get later on the tutorial.</span></span>
    
    <span data-ttu-id="5b0f7-171">d.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-171">d.</span></span> <span data-ttu-id="5b0f7-172">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-172">Click **Ok**.</span></span>    

6. <span data-ttu-id="5b0f7-173">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-173">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5b0f7-175">在 [TINFOIL SECURITY 組態] 區段上，按一下 [設定 TINFOIL SECURITY] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-175">On the **TINFOIL SECURITY Configuration** section, click **Configure TINFOIL SECURITY** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5b0f7-176">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TINFOIL SECURITY 組態](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. <span data-ttu-id="5b0f7-178">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 TINFOIL SECURITY 公司網站。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-178">In a different web browser window, log into your TINFOIL SECURITY company site as an administrator.</span></span>

9. <span data-ttu-id="5b0f7-179">在頂端工具列中，按一下 [我的帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-179">In the toolbar on the top, click **My Account**.</span></span>
   
    <span data-ttu-id="5b0f7-180">![儀表板](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "儀表板")</span><span class="sxs-lookup"><span data-stu-id="5b0f7-180">![Dashboard](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Dashboard")</span></span>

10. <span data-ttu-id="5b0f7-181">按一下 [安全性] 。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-181">Click **Security**.</span></span>
   
    <span data-ttu-id="5b0f7-182">![安全性](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="5b0f7-182">![Security](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Security")</span></span>

11. <span data-ttu-id="5b0f7-183">在 [單一登入]  組態頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b0f7-183">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="5b0f7-184">![單一登入](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="5b0f7-184">![Single Sign-On](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="5b0f7-185">a.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-185">a.</span></span> <span data-ttu-id="5b0f7-186">選取 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-186">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="5b0f7-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-187">b.</span></span> <span data-ttu-id="5b0f7-188">按一下 [手動設定] 。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-188">Click **Manual Configuration**.</span></span>
   
    <span data-ttu-id="5b0f7-189">c.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-189">c.</span></span> <span data-ttu-id="5b0f7-190">在 [SAML Post URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值</span><span class="sxs-lookup"><span data-stu-id="5b0f7-190">In **SAML Post URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal</span></span>
   
    <span data-ttu-id="5b0f7-191">d.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-191">d.</span></span> <span data-ttu-id="5b0f7-192">在 [SAML 憑證指紋] 文字方塊中，貼上您從 [SAML 簽署憑證] 區段複製的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-192">In **SAML Certificate Fingerprint** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span>
  
    <span data-ttu-id="5b0f7-193">e.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-193">e.</span></span> <span data-ttu-id="5b0f7-194">複製 [您的帳戶識別碼] 值，並將該值貼到 Azure 入口網站中 [新增屬性] 區段底下的 [屬性值] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-194">Copy **Your Account ID** value and paste the value in **Attribute Value** textbox under **Add Attribute** section in Azure portal.</span></span>
   
    <span data-ttu-id="5b0f7-195">f.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-195">f.</span></span> <span data-ttu-id="5b0f7-196">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-196">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5b0f7-197">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="5b0f7-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5b0f7-198">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5b0f7-199">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5b0f7-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5b0f7-200">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5b0f7-200">Create an Azure AD test user</span></span>
<span data-ttu-id="5b0f7-201">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="5b0f7-203">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5b0f7-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b0f7-204">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b0f7-206">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![<span data-ttu-id="5b0f7-207">[使用者和群組] -> [所有使用者]</span><span class="sxs-lookup"><span data-stu-id="5b0f7-207">Users and groups -> All users</span></span> ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b0f7-208">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![User](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b0f7-210">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5b0f7-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b0f7-212">a.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-212">a.</span></span> <span data-ttu-id="5b0f7-213">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b0f7-214">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-214">b.</span></span> <span data-ttu-id="5b0f7-215">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b0f7-216">c.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-216">c.</span></span> <span data-ttu-id="5b0f7-217">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5b0f7-218">d.</span><span class="sxs-lookup"><span data-stu-id="5b0f7-218">d.</span></span> <span data-ttu-id="5b0f7-219">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-219">Click **Create**.</span></span>
 
### <a name="create-a-tinfoil-security-test-user"></a><span data-ttu-id="5b0f7-220">建立 TINFOIL SECURITY 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5b0f7-220">Create a TINFOIL SECURITY test user</span></span>

<span data-ttu-id="5b0f7-221">若要讓 Azure AD 使用者可以登入 TINFOIL SECURITY，則必須將他們佈建到 TINFOIL SECURITY。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-221">In order to enable Azure AD users to log into TINFOIL SECURITY, they must be provisioned into TINFOIL SECURITY.</span></span> <span data-ttu-id="5b0f7-222">TINFOIL SECURITY 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-222">In the case of TINFOIL SECURITY, provisioning is a manual task.</span></span>

<span data-ttu-id="5b0f7-223">**若要佈建使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5b0f7-223">**To get a user provisioned, perform the following steps:**</span></span>

1. <span data-ttu-id="5b0f7-224">如果該使用者屬於企業帳戶，您需要[連絡 TINFOIL SECURITY 支援小組](https://www.tinfoilsecurity.com/contact)以建立使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-224">If the user is a part of an Enterprise account, you need to [contact the TINFOIL SECURITY support team](https://www.tinfoilsecurity.com/contact) to get the user account created.</span></span>

2. <span data-ttu-id="5b0f7-225">如果該使用者是一般的 TINFOIL SECURITY SaaS 使用者，則可以將合作者加入該使用者的任何網站。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-225">If the user is a regular TINFOIL SECURITY SaaS user, then the user can add a collaborator to any of the user’s sites.</span></span> <span data-ttu-id="5b0f7-226">這樣會觸發傳送邀請到指定電子郵件的程序，以建立新的 TINFOIL SECURITY 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-226">This triggers a process to send an invitation to the specified email to create a new TINFOIL SECURITY user account.</span></span>

> [!NOTE]
> <span data-ttu-id="5b0f7-227">您可以使用任何其他的 TINFOIL SECURITY 使用者帳戶建立工具或 TINFOIL SECURITY 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-227">You can use any other TINFOIL SECURITY user account creation tools or APIs provided by TINFOIL SECURITY to provision Azure AD user accounts.</span></span>
> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5b0f7-228">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5b0f7-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="5b0f7-229">在本節中，您會將 TINFOIL SECURITY 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TINFOIL SECURITY.</span></span>

![指派使用者][200] 

<span data-ttu-id="5b0f7-231">**若要將 Britta Simon 指派給 TINFOIL SECURITY，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5b0f7-231">**To assign Britta Simon to TINFOIL SECURITY, perform the following steps:**</span></span>

1. <span data-ttu-id="5b0f7-232">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5b0f7-234">在應用程式清單中，選取 [TINFOIL SECURITY]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-234">In the applications list, select **TINFOIL SECURITY**.</span></span>

    ![選取 TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. <span data-ttu-id="5b0f7-236">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-236">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="5b0f7-238">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-238">Click **Add** button.</span></span> <span data-ttu-id="5b0f7-239">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="5b0f7-241">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5b0f7-242">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b0f7-243">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5b0f7-244">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5b0f7-244">Test single sign-on</span></span>

<span data-ttu-id="5b0f7-245">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5b0f7-246">當您在存取面板中按一下 [TINFOIL SECURITY] 圖格時，應該會自動登入 TINFOIL SECURITY 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-246">When you click the TINFOIL SECURITY tile in the Access Panel, you should get automatically signed-on to your TINFOIL SECURITY application.</span></span> <span data-ttu-id="5b0f7-247">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5b0f7-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b0f7-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="5b0f7-248">Additional resources</span></span>

* [<span data-ttu-id="5b0f7-249">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="5b0f7-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b0f7-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5b0f7-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

