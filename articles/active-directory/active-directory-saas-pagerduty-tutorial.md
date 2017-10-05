---
title: "教學課程：Azure Active Directory 與 PagerDuty 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 PagerDuty 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bf5263ce4d8fbc231029c101f167f4b55a921e60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="6086f-103">教學課程：Azure Active Directory 與 PagerDuty 整合</span><span class="sxs-lookup"><span data-stu-id="6086f-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="6086f-104">在本教學課程中，您會了解如何整合 PagerDuty 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6086f-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6086f-105">將 PagerDuty 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="6086f-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6086f-106">您可以在 Azure AD 中管控可存取 PagerDuty 的人員</span><span class="sxs-lookup"><span data-stu-id="6086f-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="6086f-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 PagerDuty (單一登入)</span><span class="sxs-lookup"><span data-stu-id="6086f-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6086f-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="6086f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6086f-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6086f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6086f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6086f-110">Prerequisites</span></span>

<span data-ttu-id="6086f-111">若要設定 Azure AD 與 PagerDuty 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6086f-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="6086f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6086f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6086f-113">已啟用 PagerDuty 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6086f-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6086f-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6086f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6086f-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6086f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6086f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6086f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6086f-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6086f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6086f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6086f-118">Scenario description</span></span>
<span data-ttu-id="6086f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6086f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6086f-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="6086f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6086f-121">從資源庫新增 PagerDuty</span><span class="sxs-lookup"><span data-stu-id="6086f-121">Adding PagerDuty from the gallery</span></span>
2. <span data-ttu-id="6086f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6086f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="6086f-123">從資源庫新增 PagerDuty</span><span class="sxs-lookup"><span data-stu-id="6086f-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="6086f-124">若要設定將 PagerDuty 整合到 Azure AD 中，您需要從資源庫將 PagerDuty 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="6086f-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6086f-125">**若要從資源庫新增 PagerDuty，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6086f-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6086f-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6086f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="6086f-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6086f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6086f-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6086f-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="6086f-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6086f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="6086f-133">在搜尋方塊中，輸入 **PagerDuty**，從結果面板中選取 [PagerDuty]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="6086f-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6086f-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6086f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6086f-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 PagerDuty 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6086f-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6086f-137">若要讓單一登入運作，Azure AD 必須知道 PagerDuty 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="6086f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="6086f-138">換句話說，必須要建立某位 Azure AD 使用者與 PagerDuty 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6086f-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="6086f-139">在 PagerDuty 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6086f-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6086f-140">若要使用 PagerDuty 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6086f-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6086f-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="6086f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6086f-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6086f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6086f-143">**[建立 PagerDuty 測試使用者](#create-a-pagerduty-test-user)** - 使 PagerDuty 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="6086f-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6086f-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6086f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6086f-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="6086f-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6086f-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6086f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6086f-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 PagerDuty 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6086f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="6086f-148">**若要使用 PagerDuty 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6086f-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="6086f-149">在 Azure 入口網站的 [PagerDuty] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="6086f-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="6086f-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6086f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="6086f-153">在 [PagerDuty 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6086f-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![PagerDuty 網域及 URL 單一登入資訊](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="6086f-155">a.</span><span class="sxs-lookup"><span data-stu-id="6086f-155">a.</span></span> <span data-ttu-id="6086f-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="6086f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="6086f-157">b.</span><span class="sxs-lookup"><span data-stu-id="6086f-157">b.</span></span> <span data-ttu-id="6086f-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="6086f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6086f-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="6086f-159">These values are not real.</span></span> <span data-ttu-id="6086f-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="6086f-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6086f-161">請連絡 [PagerDuty 用戶端支援小組](https://www.pagerduty.com/support/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="6086f-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="6086f-162">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6086f-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="6086f-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6086f-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6086f-166">在 [PagerDuty 設定] 區段上，按一下 [設定 PagerDuty] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6086f-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6086f-167">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="6086f-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![PagerDuty 設定](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="6086f-169">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Pagerduty 公司網站。</span><span class="sxs-lookup"><span data-stu-id="6086f-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="6086f-170">在頂端的功能表中，按一下 [帳戶設定] 。</span><span class="sxs-lookup"><span data-stu-id="6086f-170">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="6086f-171">![帳戶設定](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "帳戶設定")</span><span class="sxs-lookup"><span data-stu-id="6086f-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="6086f-172">按一下 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="6086f-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="6086f-173">![單一登入](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="6086f-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="6086f-174">在 [啟用單一登入 (SSO)] 頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6086f-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>
   
    <span data-ttu-id="6086f-175">![啟用單一登入](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "啟用單一登入")</span><span class="sxs-lookup"><span data-stu-id="6086f-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="6086f-176">a.</span><span class="sxs-lookup"><span data-stu-id="6086f-176">a.</span></span> <span data-ttu-id="6086f-177">在記事本中開啟從 Azure 入口網站下載的 Base-64 編碼憑證，將其內容複製到您的剪貼簿，然後貼到 [X.509 憑證] 文字方塊中</span><span class="sxs-lookup"><span data-stu-id="6086f-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="6086f-178">b.</span><span class="sxs-lookup"><span data-stu-id="6086f-178">b.</span></span> <span data-ttu-id="6086f-179">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 **SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="6086f-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="6086f-180">c.</span><span class="sxs-lookup"><span data-stu-id="6086f-180">c.</span></span> <span data-ttu-id="6086f-181">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的**登出 URL**。</span><span class="sxs-lookup"><span data-stu-id="6086f-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="6086f-182">d.</span><span class="sxs-lookup"><span data-stu-id="6086f-182">d.</span></span> <span data-ttu-id="6086f-183">選取 [開啟單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="6086f-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="6086f-184">e.</span><span class="sxs-lookup"><span data-stu-id="6086f-184">e.</span></span> <span data-ttu-id="6086f-185">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="6086f-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="6086f-186">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="6086f-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6086f-187">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="6086f-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6086f-188">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6086f-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6086f-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6086f-189">Create an Azure AD test user</span></span>

<span data-ttu-id="6086f-190">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6086f-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="6086f-192">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6086f-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6086f-193">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6086f-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6086f-195">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="6086f-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6086f-197">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6086f-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6086f-199">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6086f-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6086f-201">a.</span><span class="sxs-lookup"><span data-stu-id="6086f-201">a.</span></span> <span data-ttu-id="6086f-202">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6086f-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6086f-203">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6086f-203">b.</span></span> <span data-ttu-id="6086f-204">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="6086f-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6086f-205">c.</span><span class="sxs-lookup"><span data-stu-id="6086f-205">c.</span></span> <span data-ttu-id="6086f-206">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="6086f-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6086f-207">d.</span><span class="sxs-lookup"><span data-stu-id="6086f-207">d.</span></span> <span data-ttu-id="6086f-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6086f-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="6086f-209">建立 PagerDuty 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6086f-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="6086f-210">若要讓 Azure AD 使用者能夠登入 PagerDuty，必須將他們佈建到 PagerDuty 中。</span><span class="sxs-lookup"><span data-stu-id="6086f-210">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="6086f-211">PagerDuty 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="6086f-211">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="6086f-212">您可以使用任何其他的 Pagerduty 使用者帳戶建立工具或 Pagerduty 提供的 API 來佈建 Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="6086f-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="6086f-213">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6086f-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="6086f-214">登入您的 **Pagerduty** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="6086f-214">Log in to your **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="6086f-215">在頂端的功能表中，按一下 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="6086f-215">In the menu on the top, click **Users**.</span></span>

3. <span data-ttu-id="6086f-216">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="6086f-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="6086f-217">![新增使用者](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="6086f-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="6086f-218">在 [邀請小組] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6086f-218">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="6086f-219">![邀請團隊成員](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "邀請團隊成員")</span><span class="sxs-lookup"><span data-stu-id="6086f-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="6086f-220">a.</span><span class="sxs-lookup"><span data-stu-id="6086f-220">a.</span></span> <span data-ttu-id="6086f-221">輸入使用者的**名字及姓氏**，如 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="6086f-221">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="6086f-222">b.</span><span class="sxs-lookup"><span data-stu-id="6086f-222">b.</span></span> <span data-ttu-id="6086f-223">輸入使用者的**電子郵件**地址，如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="6086f-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="6086f-224">c.</span><span class="sxs-lookup"><span data-stu-id="6086f-224">c.</span></span> <span data-ttu-id="6086f-225">按一下 [新增]，然後按一下 [傳送邀請]。</span><span class="sxs-lookup"><span data-stu-id="6086f-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="6086f-226">所有加入的使用者將會收到建立 PagerDuty 帳戶的邀請。</span><span class="sxs-lookup"><span data-stu-id="6086f-226">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6086f-227">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6086f-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="6086f-228">在本節中，您會將 PagerDuty 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6086f-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![指派使用者角色][200]

<span data-ttu-id="6086f-230">**若要將 Britta Simon 指派到 PagerDuty，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="6086f-230">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="6086f-231">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6086f-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6086f-233">在應用程式清單中，選取 [PagerDuty]。</span><span class="sxs-lookup"><span data-stu-id="6086f-233">In the applications list, select **PagerDuty**.</span></span>

    ![應用程式清單中的 PagerDuty 連結](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="6086f-235">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6086f-235">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="6086f-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6086f-237">Click **Add** button.</span></span> <span data-ttu-id="6086f-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6086f-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="6086f-240">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="6086f-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6086f-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6086f-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6086f-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6086f-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6086f-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6086f-243">Test single sign-on</span></span>

<span data-ttu-id="6086f-244">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="6086f-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6086f-245">在存取面板中按一下 PagerDuty 圖格時，應該會自動登入 PagerDuty 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6086f-245">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="6086f-246">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="6086f-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6086f-247">其他資源</span><span class="sxs-lookup"><span data-stu-id="6086f-247">Additional resources</span></span>

* [<span data-ttu-id="6086f-248">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="6086f-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6086f-249">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6086f-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

