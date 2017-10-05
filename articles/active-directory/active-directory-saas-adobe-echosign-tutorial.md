---
title: "教學課程：Azure Active Directory 與 Adobe Sign 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Adobe Sign 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b413772de1af1fbb128d29b81e5831cfd6a39ab4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="f6775-103">教學課程：Azure Active Directory 與 Adobe Sign 整合</span><span class="sxs-lookup"><span data-stu-id="f6775-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="f6775-104">在本教學課程中，您會了解如何將 Adobe Sign 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="f6775-104">In this tutorial, you learn how to integrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6775-105">將 Adobe Sign 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f6775-105">Integrating Adobe Sign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f6775-106">您可以在 Azure AD 中控制可存取 Adobe Sign 的人員</span><span class="sxs-lookup"><span data-stu-id="f6775-106">You can control in Azure AD who has access to Adobe Sign</span></span>
- <span data-ttu-id="f6775-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Adobe Sign (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f6775-107">You can enable your users to automatically get signed-on to Adobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f6775-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f6775-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f6775-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f6775-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6775-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f6775-110">Prerequisites</span></span>

<span data-ttu-id="f6775-111">若要設定 Azure AD 與 Adobe Sign 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f6775-111">To configure Azure AD integration with Adobe Sign, you need the following items:</span></span>

- <span data-ttu-id="f6775-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f6775-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6775-113">已啟用 Adobe Sign 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f6775-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f6775-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f6775-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f6775-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f6775-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f6775-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f6775-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f6775-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f6775-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6775-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f6775-118">Scenario description</span></span>
<span data-ttu-id="f6775-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f6775-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f6775-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f6775-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6775-121">從資源庫新增 Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="f6775-121">Adding Adobe Sign from the gallery</span></span>
2. <span data-ttu-id="f6775-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f6775-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-the-gallery"></a><span data-ttu-id="f6775-123">從資源庫新增 Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="f6775-123">Adding Adobe Sign from the gallery</span></span>
<span data-ttu-id="f6775-124">若要設定將 Adobe Sign 整合到 Azure AD 中，您需要從資源庫將 Adobe Sign 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="f6775-124">To configure the integration of Adobe Sign into Azure AD, you need to add Adobe Sign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f6775-125">**若要從資源庫新增 Adobe Sign，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f6775-125">**To add Adobe Sign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f6775-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f6775-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f6775-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f6775-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f6775-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f6775-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f6775-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6775-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f6775-133">在搜尋方塊中，輸入 **Adobe Sign**。</span><span class="sxs-lookup"><span data-stu-id="f6775-133">In the search box, type **Adobe Sign**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="f6775-135">在結果面板中，選取 [Adobe Sign]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6775-135">In the results panel, select **Adobe Sign**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f6775-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f6775-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f6775-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Adobe Sign 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f6775-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f6775-139">若要讓單一登入能夠運作，Azure AD 必須知道 Adobe Sign 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f6775-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Sign is to a user in Azure AD.</span></span> <span data-ttu-id="f6775-140">換句話說，必須在 Azure AD 使用者與 Adobe Sign 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f6775-140">In other words, a link relationship between an Azure AD user and the related user in Adobe Sign needs to be established.</span></span>

<span data-ttu-id="f6775-141">在 Adobe Sign 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f6775-141">In Adobe Sign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f6775-142">若要設定及測試與 Adobe Sign 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="f6775-142">To configure and test Azure AD single sign-on with Adobe Sign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f6775-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f6775-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f6775-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f6775-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f6775-145">**[建立 Adobe Sign 測試使用者](#creating-an-adobe-sign-test-user)** - 在 Adobe Sign 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="f6775-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - to have a counterpart of Britta Simon in Adobe Sign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f6775-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f6775-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6775-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f6775-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f6775-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f6775-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f6775-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Adobe Sign 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f6775-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="f6775-150">**若要設定與 Adobe Sign 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f6775-150">**To configure Azure AD single sign-on with Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="f6775-151">在 Azure 入口網站的 [Adobe Sign] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f6775-151">In the Azure portal, on the **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f6775-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f6775-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="f6775-155">在 [Adobe Sign 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f6775-155">On the **Adobe Sign Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="f6775-157">a.</span><span class="sxs-lookup"><span data-stu-id="f6775-157">a.</span></span> <span data-ttu-id="f6775-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="f6775-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="f6775-159">b.</span><span class="sxs-lookup"><span data-stu-id="f6775-159">b.</span></span> <span data-ttu-id="f6775-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="f6775-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f6775-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f6775-161">These values are not real.</span></span> <span data-ttu-id="f6775-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="f6775-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f6775-163">請連絡 [Adobe Sign 用戶端支援小組](https://helpx.adobe.com/in/contact/support.html)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="f6775-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="f6775-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f6775-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="f6775-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6775-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f6775-168">在 [Adobe Sign 組態] 區段上，按一下 [設定 Adobe Sign] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f6775-168">On the **Adobe Sign Configuration** section, click **Configure Adobe Sign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f6775-169">從 [快速參考] 區段中複製「登出 URL」、「SAML 實體識別碼」及「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="f6775-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="f6775-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Adobe Sign 公司網站。</span><span class="sxs-lookup"><span data-stu-id="f6775-171">In a different web browser window, log in to your Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="f6775-172">在頂端的功能表中，按一下 [帳戶]，然後在左側瀏覽窗格中，按一下 [帳戶設定] 下的 [SAML 設定]。</span><span class="sxs-lookup"><span data-stu-id="f6775-172">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="f6775-173">![帳戶](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "帳戶")</span><span class="sxs-lookup"><span data-stu-id="f6775-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="f6775-174">在 [SAML 設定] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f6775-174">In the SAML Settings section, perform the following steps:</span></span>
   
   <span data-ttu-id="f6775-175">![SAML 設定](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="f6775-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="f6775-176">a.</span><span class="sxs-lookup"><span data-stu-id="f6775-176">a.</span></span> <span data-ttu-id="f6775-177">針對 [SAML 模式]，選取 [SAML 強制]。</span><span class="sxs-lookup"><span data-stu-id="f6775-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="f6775-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6775-178">b.</span></span> <span data-ttu-id="f6775-179">選取 [允許 EchoSign 帳戶管理員使用其 EchoSign 認證登入] 。</span><span class="sxs-lookup"><span data-stu-id="f6775-179">Select **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="f6775-180">c.</span><span class="sxs-lookup"><span data-stu-id="f6775-180">c.</span></span> <span data-ttu-id="f6775-181">針對 [使用者建立]，選取 [透過 SAML 自動新增已驗證的使用者]。</span><span class="sxs-lookup"><span data-stu-id="f6775-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="f6775-182">繼續執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f6775-182">Move on, performing the following steps:</span></span>

       <span data-ttu-id="f6775-183">![SAML 設定](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="f6775-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="f6775-184">a.</span><span class="sxs-lookup"><span data-stu-id="f6775-184">a.</span></span> <span data-ttu-id="f6775-185">將您從 Azure 入口網站複製的「SAML 實體識別碼」貼到 [IdP 實體識別碼] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="f6775-185">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="f6775-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6775-186">b.</span></span> <span data-ttu-id="f6775-187">將您從 Azure 入口網站複製的「SAML 單一登入服務 URL」貼到 [IdP 登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="f6775-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into the **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="f6775-188">c.</span><span class="sxs-lookup"><span data-stu-id="f6775-188">c.</span></span> <span data-ttu-id="f6775-189">將您從 Azure 入口網站複製的「登出 URL」貼到 [IdP 登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="f6775-189">Paste **Sign-Out URL**, which you have copied from Azure portal into the **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="f6775-190">d.</span><span class="sxs-lookup"><span data-stu-id="f6775-190">d.</span></span> <span data-ttu-id="f6775-191">在記事本中開啟下載的「憑證 (Base64)」檔案，將其內容複製到剪貼簿，然後貼到 [IdP 憑證] 文字方塊中</span><span class="sxs-lookup"><span data-stu-id="f6775-191">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Certificate** textbox</span></span>

    <span data-ttu-id="f6775-192">e.</span><span class="sxs-lookup"><span data-stu-id="f6775-192">e.</span></span> <span data-ttu-id="f6775-193">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="f6775-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f6775-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="f6775-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f6775-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="f6775-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f6775-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f6775-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f6775-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f6775-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f6775-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f6775-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f6775-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f6775-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f6775-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f6775-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6775-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="f6775-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6775-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f6775-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6775-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f6775-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f6775-209">a.</span><span class="sxs-lookup"><span data-stu-id="f6775-209">a.</span></span> <span data-ttu-id="f6775-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f6775-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f6775-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6775-211">b.</span></span> <span data-ttu-id="f6775-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f6775-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f6775-213">c.</span><span class="sxs-lookup"><span data-stu-id="f6775-213">c.</span></span> <span data-ttu-id="f6775-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f6775-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f6775-215">d.</span><span class="sxs-lookup"><span data-stu-id="f6775-215">d.</span></span> <span data-ttu-id="f6775-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f6775-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="f6775-217">建立 Adobe Sign 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f6775-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="f6775-218">若要讓 Azure AD 使用者能夠登入 Adobe Sign，必須將他們佈建到 Adobe Sign。</span><span class="sxs-lookup"><span data-stu-id="f6775-218">To enable Azure AD users to log in to Adobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="f6775-219">就 Adobe Sign 而言，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="f6775-219">In the case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="f6775-220">您可以使用任何其他的 Adobe Sign 使用者帳戶建立工具或 Adobe Sign 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f6775-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign to provision AAD user accounts.</span></span> 

<span data-ttu-id="f6775-221">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f6775-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f6775-222">以系統管理員身分登入您的 **Adobe Sign** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="f6775-222">Log in to your **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="f6775-223">在頂端的功能表中，按一下 [帳戶]，然後在左側瀏覽窗格中，按一下 [使用者和群組]，接著按一下 [建立新的使用者]。</span><span class="sxs-lookup"><span data-stu-id="f6775-223">In the menu on the top, click **Account**, and then, in the navigation pane on the left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="f6775-224">![帳戶](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "帳戶")</span><span class="sxs-lookup"><span data-stu-id="f6775-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="f6775-225">在 [建立新的使用者] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f6775-225">In the **Create New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="f6775-226">![建立使用者](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="f6775-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="f6775-227">a.</span><span class="sxs-lookup"><span data-stu-id="f6775-227">a.</span></span> <span data-ttu-id="f6775-228">在相關的文字方塊中，輸入您想要佈建之有效 AAD 帳戶的 [電子郵件地址]、[名字] 和 [姓氏]。</span><span class="sxs-lookup"><span data-stu-id="f6775-228">Type the **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="f6775-229">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6775-229">b.</span></span> <span data-ttu-id="f6775-230">按一下 [建立使用者] 。</span><span class="sxs-lookup"><span data-stu-id="f6775-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="f6775-231">Azure Active Directory 帳戶持有者會收到一封電子郵件，其中包含一個用來確認帳戶以使其生效的連結。</span><span class="sxs-lookup"><span data-stu-id="f6775-231">The Azure Active Directory account holder receives an email that includes a link to confirm the account before it becomes active.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f6775-232">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f6775-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f6775-233">在本節中，您會將 Adobe Sign 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f6775-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Sign.</span></span>

![指派使用者][200] 

<span data-ttu-id="f6775-235">**若要將 Britta Simon 指派給 Adobe Sign，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="f6775-235">**To assign Britta Simon to Adobe Sign, perform the following steps:**</span></span>

1. <span data-ttu-id="f6775-236">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f6775-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f6775-238">在應用程式清單中，選取 [Adobe Sign]。</span><span class="sxs-lookup"><span data-stu-id="f6775-238">In the applications list, select **Adobe Sign**.</span></span>

    ![設定單一登入](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="f6775-240">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f6775-240">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f6775-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6775-242">Click **Add** button.</span></span> <span data-ttu-id="f6775-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f6775-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f6775-245">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f6775-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f6775-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6775-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f6775-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6775-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f6775-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f6775-248">Testing single sign-on</span></span>

<span data-ttu-id="f6775-249">當您在「存取面板」中按一下 [Adobe Sign] 圖格時，應該會自動登入您的 Adobe Sign 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6775-249">When you click the Adobe Sign tile in the Access Panel, you should get automatically signed-on to your Adobe Sign application.</span></span>
<span data-ttu-id="f6775-250">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="f6775-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6775-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="f6775-251">Additional resources</span></span>

* [<span data-ttu-id="f6775-252">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f6775-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6775-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f6775-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

