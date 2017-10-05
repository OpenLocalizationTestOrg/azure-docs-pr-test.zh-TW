---
title: "教學課程：Azure Active Directory 與 ClickTime 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ClickTime 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 0e0123a40d52dfd7a2e29c29cb2239e979089ca9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="3a548-103">教學課程：Azure Active Directory 與 ClickTime 整合</span><span class="sxs-lookup"><span data-stu-id="3a548-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="3a548-104">在本教學課程中，您會了解如何整合 ClickTime 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="3a548-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a548-105">ClickTime 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="3a548-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a548-106">您可以在 Azure AD 中控制可存取 ClickTime 的人員</span><span class="sxs-lookup"><span data-stu-id="3a548-106">You can control in Azure AD who has access to ClickTime</span></span>
- <span data-ttu-id="3a548-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 ClickTime (單一登入)</span><span class="sxs-lookup"><span data-stu-id="3a548-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a548-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="3a548-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3a548-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="3a548-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a548-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3a548-110">Prerequisites</span></span>

<span data-ttu-id="3a548-111">若要設定 Azure AD 與 ClickTime 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="3a548-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

- <span data-ttu-id="3a548-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3a548-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a548-113">啟用 ClickTime 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3a548-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a548-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3a548-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a548-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="3a548-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a548-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="3a548-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a548-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3a548-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a548-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="3a548-118">Scenario description</span></span>
<span data-ttu-id="3a548-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a548-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a548-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="3a548-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a548-121">從資源庫新增 ClickTime</span><span class="sxs-lookup"><span data-stu-id="3a548-121">Adding ClickTime from the gallery</span></span>
2. <span data-ttu-id="3a548-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3a548-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="3a548-123">從資源庫新增 ClickTime</span><span class="sxs-lookup"><span data-stu-id="3a548-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="3a548-124">若要設定 ClickTime 與 Azure AD 整合，您需要從資源庫將 ClickTime 新增至受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="3a548-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a548-125">**若要從資源庫新增 ClickTime，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3a548-125">**To add ClickTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a548-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="3a548-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="3a548-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3a548-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3a548-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3a548-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="3a548-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a548-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="3a548-133">在搜尋方塊中，輸入 **ClickTime**，從結果面板中選取 [ClickTime]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a548-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3a548-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3a548-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3a548-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 ClickTime 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a548-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3a548-137">若要讓單一登入運作，Azure AD 必須知道 ClickTime 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="3a548-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="3a548-138">換句話說，必須建立 Azure AD 使用者和 ClickTime 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3a548-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="3a548-139">在 ClickTime 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="3a548-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3a548-140">若要設定及測試與 ClickTime 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="3a548-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a548-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="3a548-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3a548-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a548-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a548-143">**[建立 ClickTime 測試使用者](#create-a-clicktime-test-user)** - 在 ClickTime 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="3a548-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a548-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a548-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a548-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="3a548-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3a548-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="3a548-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3a548-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 ClickTime 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a548-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="3a548-148">**若要設定與 ClickTime 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3a548-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="3a548-149">在 Azure 入口網站的 [ClickTime] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="3a548-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="3a548-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a548-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="3a548-153">在 [ClickTime 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a548-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span></span>

    ![ClickTime 網域與 URL 單一登入資訊](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="3a548-155">a.</span><span class="sxs-lookup"><span data-stu-id="3a548-155">a.</span></span> <span data-ttu-id="3a548-156">在 [識別碼] 文字方塊中輸入 URL：`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="3a548-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="3a548-157">b.</span><span class="sxs-lookup"><span data-stu-id="3a548-157">b.</span></span> <span data-ttu-id="3a548-158">在 [回覆 URL] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="3a548-158">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="3a548-159">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="3a548-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="3a548-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a548-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3a548-163">在 [ClickTime 組態] 區段上，按一下 [設定 ClickTime] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="3a548-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3a548-164">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="3a548-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![ClickTime 組態](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="3a548-166">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 ClickTime 公司網站。</span><span class="sxs-lookup"><span data-stu-id="3a548-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="3a548-167">在頂端工具列中，按一下 [喜好設定]，然後按一下 [安全性設定]。</span><span class="sxs-lookup"><span data-stu-id="3a548-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="3a548-168">在 [單一登入喜好設定]  組態區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a548-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="3a548-169">![安全性設定](./media/active-directory-saas-clicktime-tutorial/tic777280.png "安全性設定")</span><span class="sxs-lookup"><span data-stu-id="3a548-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="3a548-170">a.</span><span class="sxs-lookup"><span data-stu-id="3a548-170">a.</span></span>  <span data-ttu-id="3a548-171">選取 [允許]，以搭配 **Azure AD** 使用單一登入 (SSO) 進行登入。</span><span class="sxs-lookup"><span data-stu-id="3a548-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="3a548-172">b.</span><span class="sxs-lookup"><span data-stu-id="3a548-172">b.</span></span> <span data-ttu-id="3a548-173">在 [識別提供者端點] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="3a548-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="3a548-174">c.</span><span class="sxs-lookup"><span data-stu-id="3a548-174">c.</span></span>  <span data-ttu-id="3a548-175">在 [記事本] 中開啟從 Azure 入口網站下載的 Base-64 編碼憑證，複製其內容，然後貼到 [X.509 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="3a548-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="3a548-176">d.</span><span class="sxs-lookup"><span data-stu-id="3a548-176">d.</span></span>  <span data-ttu-id="3a548-177">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3a548-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3a548-178">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="3a548-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3a548-179">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="3a548-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3a548-180">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3a548-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3a548-181">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3a548-181">Create an Azure AD test user</span></span>
<span data-ttu-id="3a548-182">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="3a548-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="3a548-184">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3a548-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a548-185">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a548-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a548-187">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="3a548-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a548-189">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3a548-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a548-191">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a548-191">In the **User** dialog box, perform the following steps:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a548-193">a.</span><span class="sxs-lookup"><span data-stu-id="3a548-193">a.</span></span> <span data-ttu-id="3a548-194">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="3a548-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a548-195">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a548-195">b.</span></span> <span data-ttu-id="3a548-196">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="3a548-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a548-197">c.</span><span class="sxs-lookup"><span data-stu-id="3a548-197">c.</span></span> <span data-ttu-id="3a548-198">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="3a548-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3a548-199">d.</span><span class="sxs-lookup"><span data-stu-id="3a548-199">d.</span></span> <span data-ttu-id="3a548-200">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3a548-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="3a548-201">建立 ClickTime 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3a548-201">Create a ClickTime test user</span></span>

<span data-ttu-id="3a548-202">若要讓 Azure AD 使用者可以登入 ClickTime，必須將他們佈建到 ClickTime。</span><span class="sxs-lookup"><span data-stu-id="3a548-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="3a548-203">ClickTime 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="3a548-203">In the case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="3a548-204">您可以使用任何其他的 ClickTime 使用者帳戶建立工具或 ClickTime 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a548-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>

<span data-ttu-id="3a548-205">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3a548-205">**To provision a user account, perform the following steps:**</span></span>
1. <span data-ttu-id="3a548-206">登入您的 **ClickTime** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="3a548-206">Log in to your **ClickTime** tenant.</span></span>
2. <span data-ttu-id="3a548-207">在頂端工具列中，按一下 [公司]，然後按一下 [人員]。</span><span class="sxs-lookup"><span data-stu-id="3a548-207">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="3a548-208">![人員](./media/active-directory-saas-clicktime-tutorial/tic777282.png "人員")</span><span class="sxs-lookup"><span data-stu-id="3a548-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="3a548-209">按一下 [新增人員] 。</span><span class="sxs-lookup"><span data-stu-id="3a548-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="3a548-210">![新增人員](./media/active-directory-saas-clicktime-tutorial/tic777283.png "新增人員")</span><span class="sxs-lookup"><span data-stu-id="3a548-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="3a548-211">在 [新人員] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3a548-211">In the New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="3a548-212">![人員](./media/active-directory-saas-clicktime-tutorial/tic777284.png "人員")</span><span class="sxs-lookup"><span data-stu-id="3a548-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="3a548-213">a.</span><span class="sxs-lookup"><span data-stu-id="3a548-213">a.</span></span>  <span data-ttu-id="3a548-214">在 [全名] 文字方塊中，輸入使用者 (例如 **Britta Simon**) 的全名。</span><span class="sxs-lookup"><span data-stu-id="3a548-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="3a548-215">b.</span><span class="sxs-lookup"><span data-stu-id="3a548-215">b.</span></span>  <span data-ttu-id="3a548-216">在 [電子郵件地址] 文字方塊中，輸入像是 **brittasimon@contoso.com** 的使用者電子郵件。</span><span class="sxs-lookup"><span data-stu-id="3a548-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="3a548-217">您可以視需要設定新人員物件的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="3a548-217">If you want to, you can set additional properties of the new person object.</span></span>
   
    <span data-ttu-id="3a548-218">c.</span><span class="sxs-lookup"><span data-stu-id="3a548-218">c.</span></span>  <span data-ttu-id="3a548-219">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="3a548-219">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3a548-220">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="3a548-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="3a548-221">在本節中，您會將 ClickTime 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="3a548-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="3a548-223">**若要將 Britta Simon 指派給 ClickTime，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="3a548-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="3a548-224">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="3a548-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="3a548-226">在應用程式清單中，選取 [ClickTime] 。</span><span class="sxs-lookup"><span data-stu-id="3a548-226">In the applications list, select **ClickTime**.</span></span>

    ![應用程式清單中的 ClickTimne 連結](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="3a548-228">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3a548-228">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202] 

4. <span data-ttu-id="3a548-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a548-230">Click **Add** button.</span></span> <span data-ttu-id="3a548-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="3a548-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="3a548-233">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="3a548-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3a548-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a548-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a548-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a548-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3a548-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="3a548-236">Test single sign-on</span></span>

<span data-ttu-id="3a548-237">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="3a548-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3a548-238">當您在「存取面板」中按一下 [ClickTime] 圖格時，應該會自動登入您的 ClickTime 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a548-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>
<span data-ttu-id="3a548-239">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3a548-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a548-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="3a548-240">Additional resources</span></span>

* [<span data-ttu-id="3a548-241">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="3a548-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a548-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="3a548-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

