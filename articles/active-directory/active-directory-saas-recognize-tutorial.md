---
title: "教學課程：Azure Active Directory 與 Recognize 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Recognize 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 97d85183d0307c41a3b879d440d87a6fb0c53190
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="898b4-103">教學課程：Azure Active Directory 與 Recognize 整合</span><span class="sxs-lookup"><span data-stu-id="898b4-103">Tutorial: Azure Active Directory integration with Recognize</span></span>

<span data-ttu-id="898b4-104">在本教學課程中，您會了解如何整合 Recognize 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="898b4-104">In this tutorial, you learn how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="898b4-105">將 Recognize 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="898b4-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="898b4-106">您可以在 Azure AD 中控制誰能夠存取 Recognize</span><span class="sxs-lookup"><span data-stu-id="898b4-106">You can control in Azure AD who has access to Recognize</span></span>
- <span data-ttu-id="898b4-107">您可以讓您的使用者使用其 Azure AD 帳戶自動登入 Recognize (單一登入)</span><span class="sxs-lookup"><span data-stu-id="898b4-107">You can enable your users to automatically get signed-on to Recognize (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="898b4-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="898b4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="898b4-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="898b4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="898b4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="898b4-110">Prerequisites</span></span>

<span data-ttu-id="898b4-111">若要設定 Azure AD 與 Recognize 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="898b4-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

- <span data-ttu-id="898b4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="898b4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="898b4-113">啟用 Recognize 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="898b4-113">A Recognize single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="898b4-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="898b4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="898b4-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="898b4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="898b4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="898b4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="898b4-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="898b4-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="898b4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="898b4-118">Scenario description</span></span>
<span data-ttu-id="898b4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="898b4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="898b4-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="898b4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="898b4-121">從資源庫新增 Recognize</span><span class="sxs-lookup"><span data-stu-id="898b4-121">Adding Recognize from the gallery</span></span>
2. <span data-ttu-id="898b4-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="898b4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="898b4-123">從資源庫新增 Recognize</span><span class="sxs-lookup"><span data-stu-id="898b4-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="898b4-124">若要設定將 Recognize 整合至 Azure AD，您必須將資源庫中的 Recognize 新增至您的受管理 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="898b4-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="898b4-125">**若要從資源庫新增 Recognize，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="898b4-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="898b4-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="898b4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="898b4-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="898b4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="898b4-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="898b4-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="898b4-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="898b4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="898b4-133">在搜尋方塊中輸入 **Recognize**。</span><span class="sxs-lookup"><span data-stu-id="898b4-133">In the search box, type **Recognize**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. <span data-ttu-id="898b4-135">在結果面板中，選取 [Recognize]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="898b4-135">In the results panel, select **Recognize**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="898b4-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="898b4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="898b4-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Recognize 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="898b4-138">In this section, you configure and test Azure AD single sign-on with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="898b4-139">若要讓單一登入運作，Azure AD 必須知道 Recognize 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="898b4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Recognize is to a user in Azure AD.</span></span> <span data-ttu-id="898b4-140">換句話說，必須在 Azure AD 使用者和 Recognize 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="898b4-140">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="898b4-141">在 Recognize 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="898b4-141">In Recognize, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="898b4-142">若要使用 Recognize 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="898b4-142">To configure and test Azure AD single sign-on with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="898b4-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="898b4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="898b4-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="898b4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="898b4-145">**[建立 Recognize 測試使用者](#creating-a-recognize-test-user)** - 使 Recognize 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="898b4-145">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="898b4-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="898b4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="898b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="898b4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="898b4-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="898b4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="898b4-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Recognize 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="898b4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Recognize application.</span></span>

<span data-ttu-id="898b4-150">**若要使用 Recognize 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="898b4-150">**To configure Azure AD single sign-on with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="898b4-151">在 Azure 入口網站的 [Recognize] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="898b4-151">In the Azure portal, on the **Recognize** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="898b4-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="898b4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. <span data-ttu-id="898b4-155">在 [Recognize 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="898b4-155">On the **Recognize Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    <span data-ttu-id="898b4-157">a.</span><span class="sxs-lookup"><span data-stu-id="898b4-157">a.</span></span> <span data-ttu-id="898b4-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://recognizeapp.com/<your-domain>/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="898b4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`</span></span>

    <span data-ttu-id="898b4-159">b.</span><span class="sxs-lookup"><span data-stu-id="898b4-159">b.</span></span> <span data-ttu-id="898b4-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://recognizeapp.com/<your-domain>`</span><span class="sxs-lookup"><span data-stu-id="898b4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="898b4-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="898b4-161">These values are not real.</span></span> <span data-ttu-id="898b4-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="898b4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="898b4-163">請連絡 [Recognize 客戶支援小組](mailto:support@recognizeapp.com)以取得登入 URL，而且您可以從 [SSO 設定] 區段 (本教學課程稍後會說明) 中開啟 [服務提供者中繼資料 URL] 以取得識別碼值。</span><span class="sxs-lookup"><span data-stu-id="898b4-163">Contact [Recognize Client support team](mailto:support@recognizeapp.com) to get Sign-On URL and you can get Identifier value by opening the Service Provider Metadata URL from the SSO Settings section that is explained later in the tutorial.</span></span> <span data-ttu-id="898b4-164">。</span><span class="sxs-lookup"><span data-stu-id="898b4-164">.</span></span> 
 
4. <span data-ttu-id="898b4-165">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="898b4-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. <span data-ttu-id="898b4-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="898b4-167">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="898b4-169">在 [Recognize 組態] 區段上，按一下 [設定 Recognize] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="898b4-169">On the **Recognize Configuration** section, click **Configure Recognize** to open **Configure sign-on** window.</span></span> <span data-ttu-id="898b4-170">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="898b4-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. <span data-ttu-id="898b4-172">在不同的網頁瀏覽器視窗中，以管理員身分登入您的 Recognize 租用戶。</span><span class="sxs-lookup"><span data-stu-id="898b4-172">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>

8. <span data-ttu-id="898b4-173">按一下右上角的 [功能表]。</span><span class="sxs-lookup"><span data-stu-id="898b4-173">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="898b4-174">移至 [Company Admin] \(公司管理員)。</span><span class="sxs-lookup"><span data-stu-id="898b4-174">Go to **Company Admin**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. <span data-ttu-id="898b4-176">在左側的導覽窗格上，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="898b4-176">On the left navigation pane, click **Settings**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. <span data-ttu-id="898b4-178">在 [SSO Settings] \(SSO 設定) 區段下執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="898b4-178">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    <span data-ttu-id="898b4-180">a.</span><span class="sxs-lookup"><span data-stu-id="898b4-180">a.</span></span> <span data-ttu-id="898b4-181">將 **[啟用 SSO]** 選取為 **ON**。</span><span class="sxs-lookup"><span data-stu-id="898b4-181">As **Enable SSO**, select **ON**.</span></span>

    <span data-ttu-id="898b4-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="898b4-182">b.</span></span> <span data-ttu-id="898b4-183">在 [IDP 實體識別碼] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="898b4-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="898b4-184">c.</span><span class="sxs-lookup"><span data-stu-id="898b4-184">c.</span></span> <span data-ttu-id="898b4-185">在 [Sso 目標 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="898b4-185">In the **Sso target url** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="898b4-186">d.</span><span class="sxs-lookup"><span data-stu-id="898b4-186">d.</span></span> <span data-ttu-id="898b4-187">在 [Slo 目標 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="898b4-187">In the **Slo target url** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span> 
    
    <span data-ttu-id="898b4-188">e.</span><span class="sxs-lookup"><span data-stu-id="898b4-188">e.</span></span> <span data-ttu-id="898b4-189">在記事本中開啟您下載的**憑證 (Base64)** 檔案，將其內容複製到剪貼簿，然後貼到 [憑證] 文字方塊中</span><span class="sxs-lookup"><span data-stu-id="898b4-189">Open your downloaded **Certificate (Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="898b4-190">f.</span><span class="sxs-lookup"><span data-stu-id="898b4-190">f.</span></span> <span data-ttu-id="898b4-191">按一下 [儲存設定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="898b4-191">Click the **Save settings** button.</span></span> 

11. <span data-ttu-id="898b4-192">在 [SSO Settings] 區段中，複製 [Service Provider Metadata url] 下方的 URL。</span><span class="sxs-lookup"><span data-stu-id="898b4-192">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. <span data-ttu-id="898b4-194">在空白瀏覽器下方開啟**中繼資料 URL 連結**，以下載中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="898b4-194">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="898b4-195">然後，從檔案中複製 EntityDescriptor 值 (entityID) 值，然後貼到 Azure 入口網站中 [Recognize 網域及 URL] 區段的 [識別碼] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="898b4-195">Then copy the EntityDescriptor value(entityID) from the file and paste it in **Identifier** textbox in **Recognize Domain and URLs section** on Azure portal.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> <span data-ttu-id="898b4-197">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="898b4-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="898b4-198">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="898b4-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="898b4-199">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="898b4-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="898b4-200">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="898b4-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="898b4-201">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="898b4-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="898b4-203">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="898b4-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="898b4-204">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="898b4-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="898b4-206">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="898b4-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="898b4-208">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="898b4-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="898b4-210">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="898b4-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="898b4-212">a.</span><span class="sxs-lookup"><span data-stu-id="898b4-212">a.</span></span> <span data-ttu-id="898b4-213">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="898b4-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="898b4-214">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="898b4-214">b.</span></span> <span data-ttu-id="898b4-215">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="898b4-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="898b4-216">c.</span><span class="sxs-lookup"><span data-stu-id="898b4-216">c.</span></span> <span data-ttu-id="898b4-217">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="898b4-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="898b4-218">d.</span><span class="sxs-lookup"><span data-stu-id="898b4-218">d.</span></span> <span data-ttu-id="898b4-219">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="898b4-219">Click **Create**.</span></span>
 
### <a name="creating-a-recognize-test-user"></a><span data-ttu-id="898b4-220">建立 Recognize 測試使用者</span><span class="sxs-lookup"><span data-stu-id="898b4-220">Creating a Recognize test user</span></span>

<span data-ttu-id="898b4-221">若要讓 Azure AD 使用者能夠登入 Recognize，必須將他們佈建到 Recognize。</span><span class="sxs-lookup"><span data-stu-id="898b4-221">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="898b4-222">在 Recognize 的情況下，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="898b4-222">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="898b4-223">此應用程式不支援 SCIM 佈建，但有能夠佈建使用者的替代使用者同步處理作業。</span><span class="sxs-lookup"><span data-stu-id="898b4-223">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="898b4-224">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="898b4-224">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="898b4-225">以管理員身分登入您的 Recognize 公司網站。</span><span class="sxs-lookup"><span data-stu-id="898b4-225">Log into your Recognize company site as an administrator.</span></span>

2. <span data-ttu-id="898b4-226">按一下右上角的 [功能表]。</span><span class="sxs-lookup"><span data-stu-id="898b4-226">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="898b4-227">移至 [Company Admin] \(公司管理員)。</span><span class="sxs-lookup"><span data-stu-id="898b4-227">Go to **Company Admin**.</span></span>

3. <span data-ttu-id="898b4-228">在左側的導覽窗格上，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="898b4-228">On the left navigation pane, click **Settings**.</span></span>

4. <span data-ttu-id="898b4-229">在 [使用者同步處理] 區段中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="898b4-229">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="898b4-230">![新增使用者](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="898b4-230">![New User](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>
   
   <span data-ttu-id="898b4-231">a.</span><span class="sxs-lookup"><span data-stu-id="898b4-231">a.</span></span> <span data-ttu-id="898b4-232">對於 [已啟用同步處理] 選取 **ON**。</span><span class="sxs-lookup"><span data-stu-id="898b4-232">As **Sync Enabled**, select **ON**.</span></span>
   
   <span data-ttu-id="898b4-233">b.</span><span class="sxs-lookup"><span data-stu-id="898b4-233">b.</span></span> <span data-ttu-id="898b4-234">對於 [Choose sync provider] (選擇同步處理提供者)，選取 [Microsoft / Office 365]。</span><span class="sxs-lookup"><span data-stu-id="898b4-234">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span>
   
   <span data-ttu-id="898b4-235">c.</span><span class="sxs-lookup"><span data-stu-id="898b4-235">c.</span></span> <span data-ttu-id="898b4-236">按一下 [Run User Sync] \(執行使用者同步處理)。</span><span class="sxs-lookup"><span data-stu-id="898b4-236">Click **Run User Sync**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="898b4-237">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="898b4-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="898b4-238">在本節中，您會將 Recognize 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="898b4-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Recognize.</span></span>

![指派使用者][200] 

<span data-ttu-id="898b4-240">**若要將 Britta Simon 指派給 Recognize，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="898b4-240">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="898b4-241">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="898b4-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="898b4-243">在應用程式清單中，選取 [Recognize] 。</span><span class="sxs-lookup"><span data-stu-id="898b4-243">In the applications list, select **Recognize**.</span></span>

    ![設定單一登入](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. <span data-ttu-id="898b4-245">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="898b4-245">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="898b4-247">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="898b4-247">Click **Add** button.</span></span> <span data-ttu-id="898b4-248">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="898b4-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="898b4-250">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="898b4-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="898b4-251">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="898b4-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="898b4-252">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="898b4-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="898b4-253">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="898b4-253">Testing single sign-on</span></span>

<span data-ttu-id="898b4-254">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="898b4-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="898b4-255">當您在 [存取面板] 中按一下 [Recognize] 圖格時，應該會自動登入您的 Recognize 應用程式。</span><span class="sxs-lookup"><span data-stu-id="898b4-255">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span> <span data-ttu-id="898b4-256">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="898b4-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="898b4-257">其他資源</span><span class="sxs-lookup"><span data-stu-id="898b4-257">Additional resources</span></span>

* [<span data-ttu-id="898b4-258">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="898b4-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="898b4-259">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="898b4-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

