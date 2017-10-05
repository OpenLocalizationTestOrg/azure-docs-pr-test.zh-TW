---
title: "教學課程：Azure Active Directory 與 Mimecast Admin Console 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Mimecast Admin Console 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: f401f592d79ad954aa466de74d3e3fbb18aa9a5b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="29d39-103">教學課程：Azure Active Directory 與 Mimecast Admin Console 整合</span><span class="sxs-lookup"><span data-stu-id="29d39-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="29d39-104">在本教學課程中，您會了解如何整合 Mimecast Admin Console 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="29d39-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29d39-105">Mimecast Admin Console 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="29d39-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29d39-106">您可以在 Azure AD 中控制可存取 Mimecast Admin Console 的人員。</span><span class="sxs-lookup"><span data-stu-id="29d39-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="29d39-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Mimecast Admin Console (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="29d39-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="29d39-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="29d39-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="29d39-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="29d39-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29d39-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="29d39-110">Prerequisites</span></span>

<span data-ttu-id="29d39-111">若要設定 Azure AD 與 Mimecast Admin Console 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="29d39-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="29d39-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="29d39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29d39-113">啟用 Mimecast Admin Console 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="29d39-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29d39-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="29d39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29d39-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="29d39-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29d39-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="29d39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29d39-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="29d39-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29d39-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="29d39-118">Scenario description</span></span>
<span data-ttu-id="29d39-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29d39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29d39-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="29d39-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29d39-121">從資源庫新增 Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="29d39-121">Adding Mimecast Admin Console from the gallery</span></span>
2. <span data-ttu-id="29d39-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="29d39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="29d39-123">從資源庫新增 Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="29d39-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="29d39-124">若要設定將 Mimecast Admin Console 整合到 Azure AD 中，您需要從資源庫將 Mimecast Admin Console 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="29d39-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29d39-125">**若要從資源庫新增 Mimecast Admin Console，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="29d39-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29d39-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="29d39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="29d39-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="29d39-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="29d39-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="29d39-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="29d39-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="29d39-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="29d39-133">在搜尋方塊中，輸入 **Mimecast Admin Console**，從結果面板中選取 **Mimecast Admin Console**，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="29d39-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29d39-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="29d39-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="29d39-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Mimecast Admin Console 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29d39-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29d39-137">若要讓單一登入運作，Azure AD 必須知道 Mimecast Admin Console 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="29d39-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="29d39-138">換句話說，必須在 Azure AD 使用者和 Mimecast Admin Console 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="29d39-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="29d39-139">在 Mimecast Admin Console 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="29d39-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="29d39-140">若要設定及測試與 Mimecast Admin Console 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="29d39-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29d39-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="29d39-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29d39-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29d39-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29d39-143">**[建立 Mimecast Admin Console 測試使用者](#create-a-mimecast-admin-console-test-user)** - 使 Mimecast Admin Console 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="29d39-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="29d39-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29d39-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29d39-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="29d39-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29d39-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="29d39-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="29d39-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Mimecast Admin Console 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="29d39-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="29d39-148">**若要設定與 Mimecast Admin Console 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="29d39-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="29d39-149">在 Azure 入口網站的 [Mimecast Admin Console] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="29d39-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="29d39-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="29d39-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="29d39-153">在 [Mimecast Admin Console 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="29d39-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Mimecast Admin Console 網域與 URL 單一登入資訊](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="29d39-155">在 [登入 URL] 文字方塊中，輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="29d39-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="29d39-156">登入 URL 是地區特定的 URL。</span><span class="sxs-lookup"><span data-stu-id="29d39-156">The sign on URL is region specific.</span></span>

4. <span data-ttu-id="29d39-157">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="29d39-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="29d39-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="29d39-159">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="29d39-161">在 [Mimecast Admin Console 設定] 區段上，按一下 [設定 Mimecast Admin Console 入口網站] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="29d39-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="29d39-162">從 [快速參考] 區段中複製 [SAML 實體識別碼] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="29d39-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Mimecast Admin Console 設定](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="29d39-164">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Mimecast Admin Console 公司網站。</span><span class="sxs-lookup"><span data-stu-id="29d39-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="29d39-165">移至 [服務 \> 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="29d39-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="29d39-166">![服務](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "服務")</span><span class="sxs-lookup"><span data-stu-id="29d39-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="29d39-167">按一下 [驗證設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="29d39-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="29d39-168">![驗證設定檔](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="29d39-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="29d39-169">按一下 [新驗證設定檔] 。</span><span class="sxs-lookup"><span data-stu-id="29d39-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="29d39-170">![新驗證設定檔](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "新驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="29d39-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="29d39-171">在 [驗證設定檔]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="29d39-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="29d39-172">![驗證設定檔](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "驗證設定檔")</span><span class="sxs-lookup"><span data-stu-id="29d39-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="29d39-173">a.</span><span class="sxs-lookup"><span data-stu-id="29d39-173">a.</span></span> <span data-ttu-id="29d39-174">在 [描述]  文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="29d39-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="29d39-175">b.</span><span class="sxs-lookup"><span data-stu-id="29d39-175">b.</span></span> <span data-ttu-id="29d39-176">選取 [強制執行 Mimecast Admin Console 的 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="29d39-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="29d39-177">c.</span><span class="sxs-lookup"><span data-stu-id="29d39-177">c.</span></span> <span data-ttu-id="29d39-178">在 [提供者] 中選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="29d39-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="29d39-179">d.</span><span class="sxs-lookup"><span data-stu-id="29d39-179">d.</span></span> <span data-ttu-id="29d39-180">將您從 Azure 入口網站複製的 **SAML 實體識別碼**貼到 [簽發者 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="29d39-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="29d39-181">e.</span><span class="sxs-lookup"><span data-stu-id="29d39-181">e.</span></span> <span data-ttu-id="29d39-182">將您從 Azure 入口網站複製的 **SAML 單一登入服務 URL** 貼到 [登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="29d39-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="29d39-183">f.</span><span class="sxs-lookup"><span data-stu-id="29d39-183">f.</span></span> <span data-ttu-id="29d39-184">將您從 Azure 入口網站複製的 **SAML 單一登入服務 URL** 貼到 [登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="29d39-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="29d39-185">Mimecast Admin Console 的登入 URL 值與登出 URL 值是相同的。</span><span class="sxs-lookup"><span data-stu-id="29d39-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="29d39-186">g.</span><span class="sxs-lookup"><span data-stu-id="29d39-186">g.</span></span> <span data-ttu-id="29d39-187">在記事本中開啟您從 Azure 入口網站下載的 base-64 憑證，移除第一行 (“*--*“) 與最後一行 (“*--*“)，將它的其餘內容複製到您的剪貼簿，然後貼到 [識別提供者憑證 (中繼資料)] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="29d39-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="29d39-188">h.</span><span class="sxs-lookup"><span data-stu-id="29d39-188">h.</span></span> <span data-ttu-id="29d39-189">選取 [允許單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="29d39-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="29d39-190">i.</span><span class="sxs-lookup"><span data-stu-id="29d39-190">i.</span></span> <span data-ttu-id="29d39-191">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="29d39-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="29d39-192">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="29d39-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="29d39-193">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="29d39-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="29d39-194">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29d39-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29d39-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="29d39-195">Create an Azure AD test user</span></span>

<span data-ttu-id="29d39-196">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="29d39-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="29d39-198">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="29d39-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29d39-199">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="29d39-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="29d39-201">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="29d39-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="29d39-203">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="29d39-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="29d39-205">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="29d39-205">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="29d39-207">a.</span><span class="sxs-lookup"><span data-stu-id="29d39-207">a.</span></span> <span data-ttu-id="29d39-208">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="29d39-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29d39-209">b.</span><span class="sxs-lookup"><span data-stu-id="29d39-209">b.</span></span> <span data-ttu-id="29d39-210">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="29d39-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="29d39-211">c.</span><span class="sxs-lookup"><span data-stu-id="29d39-211">c.</span></span> <span data-ttu-id="29d39-212">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="29d39-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="29d39-213">d.</span><span class="sxs-lookup"><span data-stu-id="29d39-213">d.</span></span> <span data-ttu-id="29d39-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="29d39-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="29d39-215">建立 Mimecast Admin Console 測試使用者</span><span class="sxs-lookup"><span data-stu-id="29d39-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="29d39-216">若要讓 Azure AD 使用者能夠登入 Mimecast Admin Console，必須將它們佈建到 Mimecast Admin Console。</span><span class="sxs-lookup"><span data-stu-id="29d39-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="29d39-217">Mimecast Admin Consol 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="29d39-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="29d39-218">您需要先註冊網域才能建立使用者。</span><span class="sxs-lookup"><span data-stu-id="29d39-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="29d39-219">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="29d39-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="29d39-220">以系統管理員身份登入您的 **Mimecast Admin Console** 。</span><span class="sxs-lookup"><span data-stu-id="29d39-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="29d39-221">移至 [目錄 \> 內部]。</span><span class="sxs-lookup"><span data-stu-id="29d39-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="29d39-222">![目錄](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "目錄")</span><span class="sxs-lookup"><span data-stu-id="29d39-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="29d39-223">按一下 [註冊新網域] 。</span><span class="sxs-lookup"><span data-stu-id="29d39-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="29d39-224">![註冊新網域](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "註冊新網域")</span><span class="sxs-lookup"><span data-stu-id="29d39-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="29d39-225">在您建立好新網域之後，，按一下 [新位址] 。</span><span class="sxs-lookup"><span data-stu-id="29d39-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="29d39-226">![新位址](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "新位址")</span><span class="sxs-lookup"><span data-stu-id="29d39-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="29d39-227">在 [新位址] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="29d39-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="29d39-228">![儲存](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "儲存")</span><span class="sxs-lookup"><span data-stu-id="29d39-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="29d39-229">a.</span><span class="sxs-lookup"><span data-stu-id="29d39-229">a.</span></span> <span data-ttu-id="29d39-230">在相關的文字方塊中，輸入您要佈建之有效 Azure AD 帳戶的 [電子郵件地址]、[全域名稱]、[密碼]、[確認密碼] 屬性。</span><span class="sxs-lookup"><span data-stu-id="29d39-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="29d39-231">b.</span><span class="sxs-lookup"><span data-stu-id="29d39-231">b.</span></span> <span data-ttu-id="29d39-232">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="29d39-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="29d39-233">您可以使用任何其他的 Mimecast Admin Console 使用者帳戶建立工具或 Mimecast Admin Console 提供的 API，佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="29d39-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="29d39-234">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="29d39-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="29d39-235">在本節中，您會將 Mimecast Admin Console 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="29d39-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="29d39-237">**若要將 Britta Simon 指派給 Mimecast Admin Console，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="29d39-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="29d39-238">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="29d39-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="29d39-240">在應用程式清單中，選取 [Mimecast Admin Console]。</span><span class="sxs-lookup"><span data-stu-id="29d39-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![應用程式清單中的 Mimecast Admin Console 連結](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="29d39-242">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="29d39-242">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="29d39-244">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="29d39-244">Click **Add** button.</span></span> <span data-ttu-id="29d39-245">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="29d39-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="29d39-247">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="29d39-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="29d39-248">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="29d39-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29d39-249">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="29d39-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="29d39-250">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="29d39-250">Test single sign-on</span></span>

<span data-ttu-id="29d39-251">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="29d39-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="29d39-252">當您在存取面板中按一下 Mimecast Admin Console 圖格時，應該會自動登入您的 Mimecast Admin Console 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29d39-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="29d39-253">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="29d39-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="29d39-254">其他資源</span><span class="sxs-lookup"><span data-stu-id="29d39-254">Additional resources</span></span>

* [<span data-ttu-id="29d39-255">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="29d39-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29d39-256">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="29d39-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

