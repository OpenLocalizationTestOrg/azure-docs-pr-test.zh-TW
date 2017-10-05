---
title: "教學課程：Azure Active Directory 與 Image Relay 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Image Relay 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 0bfbbaee7a74df6508584b7c8846fd07c2dc15c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="259f6-103">教學課程：Azure Active Directory 與 Image Relay 整合</span><span class="sxs-lookup"><span data-stu-id="259f6-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="259f6-104">在本教學課程中，您將了解如何整合 Image Relay 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="259f6-104">In this tutorial, you learn how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="259f6-105">Image Relay 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="259f6-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="259f6-106">您可以在 Azure AD 中控制可存取 Image Relay 的人員</span><span class="sxs-lookup"><span data-stu-id="259f6-106">You can control in Azure AD who has access to Image Relay</span></span>
- <span data-ttu-id="259f6-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Image Relay (單一登入)</span><span class="sxs-lookup"><span data-stu-id="259f6-107">You can enable your users to automatically get signed-on to Image Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="259f6-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="259f6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="259f6-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="259f6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="259f6-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="259f6-110">Prerequisites</span></span>

<span data-ttu-id="259f6-111">若要設定 Azure AD 與 Image Relay 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="259f6-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

- <span data-ttu-id="259f6-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="259f6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="259f6-113">啟用 Image Relay 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="259f6-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="259f6-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="259f6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="259f6-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="259f6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="259f6-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="259f6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="259f6-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="259f6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="259f6-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="259f6-118">Scenario description</span></span>
<span data-ttu-id="259f6-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="259f6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="259f6-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="259f6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="259f6-121">從資源庫新增 Image Relay</span><span class="sxs-lookup"><span data-stu-id="259f6-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="259f6-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="259f6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="259f6-123">從資源庫新增 Image Relay</span><span class="sxs-lookup"><span data-stu-id="259f6-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="259f6-124">若要設定 Image Relay 與 Azure AD 整合，您需要從資源庫將 Image Relay 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="259f6-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="259f6-125">**若要從資源庫新增 Image Relay，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="259f6-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="259f6-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="259f6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="259f6-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="259f6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="259f6-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="259f6-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="259f6-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="259f6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="259f6-133">在搜尋方塊中，輸入 **Image Relay**。</span><span class="sxs-lookup"><span data-stu-id="259f6-133">In the search box, type **Image Relay**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="259f6-135">在結果窗格中，選取 [Image Relay]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="259f6-135">In the results panel, select **Image Relay**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="259f6-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="259f6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="259f6-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Image Relay 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="259f6-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="259f6-139">若要讓單一登入能夠運作，Azure AD 必須知道 Image Relay 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="259f6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Image Relay is to a user in Azure AD.</span></span> <span data-ttu-id="259f6-140">換句話說，必須在 Azure AD 使用者與 Image Relay 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="259f6-140">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>

<span data-ttu-id="259f6-141">在 Image Relay 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="259f6-141">In Image Relay, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="259f6-142">若要設定及測試與 Image Relay 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="259f6-142">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="259f6-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="259f6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="259f6-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="259f6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="259f6-145">**[建立 Image Relay 測試使用者](#creating-an-image-relay-test-user)** - 使 Image Relay 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="259f6-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="259f6-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="259f6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="259f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="259f6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="259f6-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="259f6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="259f6-149">在本節中，您會在 Azure 的入口網站中啟用 Azure AD 單一登入，然後在您的 Image Relay 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="259f6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="259f6-150">**若要使用 Image Relay 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="259f6-150">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="259f6-151">在 Azure 入口網站的 [Image Relay] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="259f6-151">In the Azure portal, on the **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="259f6-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="259f6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="259f6-155">在 [Image Relay 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="259f6-155">On the **Image Relay Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="259f6-157">a.</span><span class="sxs-lookup"><span data-stu-id="259f6-157">a.</span></span> <span data-ttu-id="259f6-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="259f6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="259f6-159">b.</span><span class="sxs-lookup"><span data-stu-id="259f6-159">b.</span></span> <span data-ttu-id="259f6-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="259f6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="259f6-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="259f6-161">These values are not real.</span></span> <span data-ttu-id="259f6-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="259f6-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="259f6-163">請連絡 [Image Relay 客戶支援小組](http://support.imagerelay.com/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="259f6-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="259f6-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="259f6-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="259f6-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="259f6-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="259f6-168">在 [Image Relay 組態] 區段上，按一下 [設定 Image Relay] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="259f6-168">On the **Image Relay Configuration** section, click **Configure Image Relay** to open **Configure sign-on** window.</span></span> <span data-ttu-id="259f6-169">從 [快速參考] 區段中複製 [登出服務 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="259f6-169">Copy the **Sign-Out Service URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="259f6-171">在另一個瀏覽器視窗中，以系統管理員身分登入您的 Image Relay 公司網站。</span><span class="sxs-lookup"><span data-stu-id="259f6-171">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="259f6-172">在頂端的工具列中按一下 [使用者和權限] 工作負載。</span><span class="sxs-lookup"><span data-stu-id="259f6-172">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="259f6-174">按一下 [建立新的權限] 。</span><span class="sxs-lookup"><span data-stu-id="259f6-174">Click **Create New Permission**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="259f6-176">在 [單一登入設定] 工作負載中，選取 [這個群組只能透過單一登入來登入] 核取方塊，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="259f6-176">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="259f6-178">移至 [帳戶設定] 。</span><span class="sxs-lookup"><span data-stu-id="259f6-178">Go to **Account Settings**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="259f6-180">移至 [單一登入設定]  工作負載。</span><span class="sxs-lookup"><span data-stu-id="259f6-180">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="259f6-182">在 [SAML設定]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="259f6-182">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="259f6-184">a.</span><span class="sxs-lookup"><span data-stu-id="259f6-184">a.</span></span> <span data-ttu-id="259f6-185">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [單一登入服務 URL] 的值。</span><span class="sxs-lookup"><span data-stu-id="259f6-185">In **Login URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="259f6-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="259f6-186">b.</span></span> <span data-ttu-id="259f6-187">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [單一登出服務 URL] 的值。</span><span class="sxs-lookup"><span data-stu-id="259f6-187">In **Logout URL**  textbox, paste the value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="259f6-188">c.</span><span class="sxs-lookup"><span data-stu-id="259f6-188">c.</span></span> <span data-ttu-id="259f6-189">選取 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** 做為 [名稱識別碼格式]。</span><span class="sxs-lookup"><span data-stu-id="259f6-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="259f6-190">d.</span><span class="sxs-lookup"><span data-stu-id="259f6-190">d.</span></span> <span data-ttu-id="259f6-191">選取 [POST 繫結] 做為 [服務提供者要求的繫結選項 (影像轉送)]。</span><span class="sxs-lookup"><span data-stu-id="259f6-191">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="259f6-192">e.</span><span class="sxs-lookup"><span data-stu-id="259f6-192">e.</span></span> <span data-ttu-id="259f6-193">在 [x.509 憑證] 下方，按一下 [更新憑證]。</span><span class="sxs-lookup"><span data-stu-id="259f6-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="259f6-195">f.</span><span class="sxs-lookup"><span data-stu-id="259f6-195">f.</span></span> <span data-ttu-id="259f6-196">在記事本中開啟下載的憑證，複製其內容，然後貼到 [x.509 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="259f6-196">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="259f6-198">g.</span><span class="sxs-lookup"><span data-stu-id="259f6-198">g.</span></span> <span data-ttu-id="259f6-199">在 [Just-In-Time 使用者佈建] 區段中，選取 [啟用 Just-In-Time 使用者佈建]。</span><span class="sxs-lookup"><span data-stu-id="259f6-199">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="259f6-201">h.</span><span class="sxs-lookup"><span data-stu-id="259f6-201">h.</span></span> <span data-ttu-id="259f6-202">選取只允許透過單一登入來登入的權限群組 (例如 [SSO 基本])。</span><span class="sxs-lookup"><span data-stu-id="259f6-202">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="259f6-204">i.</span><span class="sxs-lookup"><span data-stu-id="259f6-204">i.</span></span> <span data-ttu-id="259f6-205">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="259f6-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="259f6-206">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="259f6-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="259f6-207">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="259f6-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="259f6-208">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="259f6-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="259f6-209">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="259f6-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="259f6-210">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="259f6-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="259f6-212">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="259f6-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="259f6-213">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="259f6-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="259f6-215">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="259f6-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="259f6-217">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="259f6-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="259f6-219">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="259f6-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="259f6-221">a.</span><span class="sxs-lookup"><span data-stu-id="259f6-221">a.</span></span> <span data-ttu-id="259f6-222">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="259f6-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="259f6-223">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="259f6-223">b.</span></span> <span data-ttu-id="259f6-224">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="259f6-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="259f6-225">c.</span><span class="sxs-lookup"><span data-stu-id="259f6-225">c.</span></span> <span data-ttu-id="259f6-226">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="259f6-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="259f6-227">d.</span><span class="sxs-lookup"><span data-stu-id="259f6-227">d.</span></span> <span data-ttu-id="259f6-228">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="259f6-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="259f6-229">建立 Image Relay 測試使用者</span><span class="sxs-lookup"><span data-stu-id="259f6-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="259f6-230">本節目標是在 Image Relay 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="259f6-230">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="259f6-231">**若要在 Image Relay 中建立名為 Britta Simon 的使用者，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="259f6-231">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="259f6-232">以系統管理員身分登入您的 Image Relay 公司網站。</span><span class="sxs-lookup"><span data-stu-id="259f6-232">Sign-on to your Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="259f6-233">移至 [使用者和權限]，選取 [建立 SSO 使用者]。</span><span class="sxs-lookup"><span data-stu-id="259f6-233">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="259f6-235">輸入您要佈建的使用者的**電子郵件**、**名字**、**姓氏**和**公司**，選取只能透過單一登入來登入的權限群組 (例如 [SSO 基本])。</span><span class="sxs-lookup"><span data-stu-id="259f6-235">Enter the **Email**, **First Name**, **Last Name**, and **Company** of the user you want to provision and select the permission group (for example, SSO Basic) which is the group that can sign in only through single sign-on.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="259f6-237">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="259f6-237">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="259f6-238">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="259f6-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="259f6-239">在本節中，您會把 Image Relay 的存取權授予 Britta Simon，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="259f6-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Image Relay.</span></span>

![指派使用者][200] 

<span data-ttu-id="259f6-241">**若要將 Britta Simon 指派到 Image Relay，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="259f6-241">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="259f6-242">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="259f6-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="259f6-244">在應用程式清單中，選取 [Image Relay]。</span><span class="sxs-lookup"><span data-stu-id="259f6-244">In the applications list, select **Image Relay**.</span></span>

    ![設定單一登入](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="259f6-246">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="259f6-246">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="259f6-248">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="259f6-248">Click **Add** button.</span></span> <span data-ttu-id="259f6-249">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="259f6-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="259f6-251">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="259f6-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="259f6-252">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="259f6-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="259f6-253">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="259f6-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="259f6-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="259f6-254">Testing single sign-on</span></span>

<span data-ttu-id="259f6-255">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="259f6-255">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>    

<span data-ttu-id="259f6-256">當您在存取面板中按一下 [Image Relay] 圖格時，應該會自動登入您的 Image Relay 應用程式。</span><span class="sxs-lookup"><span data-stu-id="259f6-256">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="259f6-257">其他資源</span><span class="sxs-lookup"><span data-stu-id="259f6-257">Additional resources</span></span>

* [<span data-ttu-id="259f6-258">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="259f6-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="259f6-259">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="259f6-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

