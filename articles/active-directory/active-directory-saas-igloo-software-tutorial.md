---
title: "教學課程：Azure Active Directory 與 Igloo Software 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Igloo Software 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="876fd-103">教學課程：Azure Active Directory 與 Igloo Software 整合</span><span class="sxs-lookup"><span data-stu-id="876fd-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="876fd-104">在此教學課程中，您將了解如何整合 Igloo Software 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="876fd-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="876fd-105">Igloo Software 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="876fd-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="876fd-106">您可以在 Azure AD 中控制可存取 Igloo Software 的人員。</span><span class="sxs-lookup"><span data-stu-id="876fd-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="876fd-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Igloo Software (單一登入)</span><span class="sxs-lookup"><span data-stu-id="876fd-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="876fd-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="876fd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="876fd-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="876fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="876fd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="876fd-110">Prerequisites</span></span>

<span data-ttu-id="876fd-111">若要設定 Azure AD 與 Igloo Software 整合，您需要以下項目：</span><span class="sxs-lookup"><span data-stu-id="876fd-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="876fd-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="876fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="876fd-113">已啟用 Igloo Software 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="876fd-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="876fd-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="876fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="876fd-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="876fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="876fd-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="876fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="876fd-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="876fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="876fd-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="876fd-118">Scenario description</span></span>
<span data-ttu-id="876fd-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="876fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="876fd-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="876fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="876fd-121">從資源庫新增 Igloo Software</span><span class="sxs-lookup"><span data-stu-id="876fd-121">Adding Igloo Software from the gallery</span></span>
2. <span data-ttu-id="876fd-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="876fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="876fd-123">從資源庫新增 Igloo Software</span><span class="sxs-lookup"><span data-stu-id="876fd-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="876fd-124">若要設定將 Igloo Software 整合到 Azure AD 中，您需要從資源庫將 Igloo Software 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="876fd-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="876fd-125">**若要從資源庫新增 Igloo Software，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="876fd-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="876fd-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="876fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="876fd-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="876fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="876fd-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="876fd-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="876fd-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="876fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="876fd-133">在搜尋方塊中，輸入 **Igloo Software**。</span><span class="sxs-lookup"><span data-stu-id="876fd-133">In the search box, type **Igloo Software**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="876fd-135">在結果窗格中，選取 [Igloo Software]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="876fd-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="876fd-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="876fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="876fd-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Igloo Software 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="876fd-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="876fd-139">單一登入若要運作，Azure AD 必須知道 Igloo Software 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="876fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="876fd-140">換句話說，Azure AD 使用者和 Igloo Software 中的相關使用者之間必須建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="876fd-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="876fd-141">在 Igloo Software 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="876fd-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="876fd-142">若要設定及測試與 Igloo Software 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="876fd-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="876fd-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="876fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="876fd-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="876fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="876fd-145">**[建立 Igloo Software 測試使用者](#creating-an-igloo-software-test-user)** - 在 Igloo Software 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="876fd-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="876fd-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="876fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="876fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="876fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="876fd-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="876fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="876fd-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Igloo Software 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="876fd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="876fd-150">**若要使用 Igloo Software 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="876fd-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="876fd-151">在 Azure 入口網站的 [Igloo Software] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="876fd-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="876fd-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="876fd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="876fd-155">在 [Igloo Software 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="876fd-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="876fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="876fd-157">a.</span></span> <span data-ttu-id="876fd-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="876fd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="876fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="876fd-159">b.</span></span> <span data-ttu-id="876fd-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="876fd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="876fd-161">c.</span><span class="sxs-lookup"><span data-stu-id="876fd-161">c.</span></span> <span data-ttu-id="876fd-162">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="876fd-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="876fd-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="876fd-163">These values are not real.</span></span> <span data-ttu-id="876fd-164">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="876fd-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="876fd-165">請連絡 [Igloo Software 用戶端支援小組](https://www.igloosoftware.com/services/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="876fd-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

4. <span data-ttu-id="876fd-166">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="876fd-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="876fd-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="876fd-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="876fd-170">在 [Igloo Software 組態] 區段上，按一下 [設定 Igloo Software] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="876fd-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="876fd-171">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="876fd-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="876fd-173">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Igloo Software 公司網站。</span><span class="sxs-lookup"><span data-stu-id="876fd-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="876fd-174">移至 [控制台] 。</span><span class="sxs-lookup"><span data-stu-id="876fd-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="876fd-175">![控制台](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "控制台")</span><span class="sxs-lookup"><span data-stu-id="876fd-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="876fd-176">在 [成員資格] 索引標籤中，按一下 [登入設定]。</span><span class="sxs-lookup"><span data-stu-id="876fd-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="876fd-177">![登入設定](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "登入設定")</span><span class="sxs-lookup"><span data-stu-id="876fd-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="876fd-178">在 [SAML 設定] 區段，按一下 [設定 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="876fd-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="876fd-179">![SAML 組態](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML 組態")</span><span class="sxs-lookup"><span data-stu-id="876fd-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="876fd-180">在 [一般設定]  區段，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="876fd-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="876fd-181">![一般組態](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "一般組態")</span><span class="sxs-lookup"><span data-stu-id="876fd-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="876fd-182">a.</span><span class="sxs-lookup"><span data-stu-id="876fd-182">a.</span></span> <span data-ttu-id="876fd-183">在 [連接名稱]  文字方塊中，輸入組態的自訂名稱。</span><span class="sxs-lookup"><span data-stu-id="876fd-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="876fd-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="876fd-184">b.</span></span> <span data-ttu-id="876fd-185">在 [IdP 登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="876fd-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="876fd-186">c.</span><span class="sxs-lookup"><span data-stu-id="876fd-186">c.</span></span> <span data-ttu-id="876fd-187">在 [IdP 登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="876fd-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="876fd-188">d.</span><span class="sxs-lookup"><span data-stu-id="876fd-188">d.</span></span> <span data-ttu-id="876fd-189">選取 [登出回應與要求 HTTP 類型] 作為 [POST]。</span><span class="sxs-lookup"><span data-stu-id="876fd-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="876fd-190">e.</span><span class="sxs-lookup"><span data-stu-id="876fd-190">e.</span></span> <span data-ttu-id="876fd-191">在從 Azure 入口網站下載的記事本檔案中開啟您的 **base-64** 編碼憑證，將憑證的內容複製到剪貼簿，再貼到 [公開憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="876fd-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="876fd-192">在 [回應與驗證設定] ，執行以下步驟：</span><span class="sxs-lookup"><span data-stu-id="876fd-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="876fd-193">![回應和驗證設定](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "回應和驗證設定")</span><span class="sxs-lookup"><span data-stu-id="876fd-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="876fd-194">a.</span><span class="sxs-lookup"><span data-stu-id="876fd-194">a.</span></span> <span data-ttu-id="876fd-195">在 [識別提供者]，選取 [Microsoft ADFS]。</span><span class="sxs-lookup"><span data-stu-id="876fd-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="876fd-196">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="876fd-196">b.</span></span> <span data-ttu-id="876fd-197">在 [識別元類型]，選取 [電子郵件地址]。</span><span class="sxs-lookup"><span data-stu-id="876fd-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="876fd-198">c.</span><span class="sxs-lookup"><span data-stu-id="876fd-198">c.</span></span> <span data-ttu-id="876fd-199">在 [電子郵件屬性] 文字方塊中，輸入**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="876fd-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="876fd-200">d.</span><span class="sxs-lookup"><span data-stu-id="876fd-200">d.</span></span> <span data-ttu-id="876fd-201">在 [名字屬性] 文字方塊中，輸入**名字**。</span><span class="sxs-lookup"><span data-stu-id="876fd-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="876fd-202">e.</span><span class="sxs-lookup"><span data-stu-id="876fd-202">e.</span></span> <span data-ttu-id="876fd-203">在 [姓氏屬性] 文字方塊中，輸入**姓氏**。</span><span class="sxs-lookup"><span data-stu-id="876fd-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="876fd-204">執行以下步驟來完成設定：</span><span class="sxs-lookup"><span data-stu-id="876fd-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="876fd-205">![登入時建立使用者](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "登入時建立使用者")</span><span class="sxs-lookup"><span data-stu-id="876fd-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="876fd-206">a.</span><span class="sxs-lookup"><span data-stu-id="876fd-206">a.</span></span> <span data-ttu-id="876fd-207">在 [登入時建立使用者]，選取 [使用者登入您的網站時建立新的使用者]。</span><span class="sxs-lookup"><span data-stu-id="876fd-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="876fd-208">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="876fd-208">b.</span></span> <span data-ttu-id="876fd-209">在 [登入設定]，選取 [在「登入」畫面使用 SAML 按鈕]。</span><span class="sxs-lookup"><span data-stu-id="876fd-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="876fd-210">c.</span><span class="sxs-lookup"><span data-stu-id="876fd-210">c.</span></span> <span data-ttu-id="876fd-211">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="876fd-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="876fd-212">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="876fd-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="876fd-213">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="876fd-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="876fd-214">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="876fd-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="876fd-215">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="876fd-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="876fd-216">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="876fd-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="876fd-218">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="876fd-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="876fd-219">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="876fd-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="876fd-221">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="876fd-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="876fd-223">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="876fd-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="876fd-225">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="876fd-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="876fd-227">a.</span><span class="sxs-lookup"><span data-stu-id="876fd-227">a.</span></span> <span data-ttu-id="876fd-228">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="876fd-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="876fd-229">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="876fd-229">b.</span></span> <span data-ttu-id="876fd-230">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="876fd-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="876fd-231">c.</span><span class="sxs-lookup"><span data-stu-id="876fd-231">c.</span></span> <span data-ttu-id="876fd-232">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="876fd-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="876fd-233">d.</span><span class="sxs-lookup"><span data-stu-id="876fd-233">d.</span></span> <span data-ttu-id="876fd-234">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="876fd-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="876fd-235">建立 Igloo Software 測試使用者</span><span class="sxs-lookup"><span data-stu-id="876fd-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="876fd-236">沒有動作項目可讓您設定  Igloo Software 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="876fd-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="876fd-237">當已指派的使用者透過存取面板嘗試登入 Igloo Software 時，Igloo Software 會檢查使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="876fd-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="876fd-238">如果尚無可用的使用者帳戶，Igloo Software 會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="876fd-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="876fd-239">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="876fd-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="876fd-240">在本節中，您會將 Igloo Software 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="876fd-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![指派使用者][200] 

<span data-ttu-id="876fd-242">**若要指派 Britta Simon 到 Igloo Software，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="876fd-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="876fd-243">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="876fd-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="876fd-245">在應用程式清單中，選取 [Igloo Software]。</span><span class="sxs-lookup"><span data-stu-id="876fd-245">In the applications list, select **Igloo Software**.</span></span>

    ![設定單一登入](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="876fd-247">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="876fd-247">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="876fd-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="876fd-249">Click **Add** button.</span></span> <span data-ttu-id="876fd-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="876fd-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="876fd-252">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="876fd-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="876fd-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="876fd-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="876fd-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="876fd-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="876fd-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="876fd-255">Testing single sign-on</span></span>

<span data-ttu-id="876fd-256">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="876fd-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="876fd-257">當您在 [存取面板] 中按一下 [Igloo Software] 圖格時，您應該會自動登入您的 Igloo Software 應用程式。</span><span class="sxs-lookup"><span data-stu-id="876fd-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="876fd-258">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="876fd-258">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="876fd-259">其他資源</span><span class="sxs-lookup"><span data-stu-id="876fd-259">Additional resources</span></span>

* [<span data-ttu-id="876fd-260">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="876fd-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="876fd-261">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="876fd-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

