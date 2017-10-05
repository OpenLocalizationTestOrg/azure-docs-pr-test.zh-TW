---
title: "教學課程：Azure Active Directory 與 Evernote 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Evernote 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: be94152a84bbbeacb623d7dd8b540e3981931a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evernote"></a><span data-ttu-id="0d095-103">教學課程：Azure Active Directory 與 Evernote 整合</span><span class="sxs-lookup"><span data-stu-id="0d095-103">Tutorial: Azure Active Directory integration with Evernote</span></span>

<span data-ttu-id="0d095-104">在本教學課程中，您將了解如何整合 Evernote 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0d095-104">In this tutorial, you learn how to integrate Evernote with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d095-105">Evernote 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="0d095-105">Integrating Evernote with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0d095-106">您可以在 Azure AD 中控制可存取 Evernote 的人員。</span><span class="sxs-lookup"><span data-stu-id="0d095-106">You can control in Azure AD who has access to Evernote.</span></span>
- <span data-ttu-id="0d095-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Evernote (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="0d095-107">You can enable your users to automatically get signed-on to Evernote (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0d095-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d095-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0d095-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0d095-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d095-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0d095-110">Prerequisites</span></span>

<span data-ttu-id="0d095-111">若要設定 Azure AD 與 Evernote 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0d095-111">To configure Azure AD integration with Evernote, you need the following items:</span></span>

- <span data-ttu-id="0d095-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0d095-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d095-113">已啟用 Evernote 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0d095-113">An Evernote single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d095-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0d095-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d095-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0d095-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d095-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0d095-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d095-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="0d095-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d095-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0d095-118">Scenario description</span></span>
<span data-ttu-id="0d095-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d095-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d095-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="0d095-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d095-121">從資源庫新增 Evernote</span><span class="sxs-lookup"><span data-stu-id="0d095-121">Adding Evernote from the gallery</span></span>
2. <span data-ttu-id="0d095-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0d095-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evernote-from-the-gallery"></a><span data-ttu-id="0d095-123">從資源庫新增 Evernote</span><span class="sxs-lookup"><span data-stu-id="0d095-123">Adding Evernote from the gallery</span></span>
<span data-ttu-id="0d095-124">若要設定 Evernote 與 Azure AD 的整合作業，您必須從資源庫將 Evernote 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="0d095-124">To configure the integration of Evernote into Azure AD, you need to add Evernote from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0d095-125">**若要從資源庫新增 Evernote，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0d095-125">**To add Evernote from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0d095-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0d095-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="0d095-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0d095-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0d095-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0d095-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="0d095-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d095-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="0d095-133">在搜尋方塊中，輸入 **Evernote**，從結果面板中選取 **Evernote**，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d095-133">In the search box, type **Evernote**, select **Evernote** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Evernote](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0d095-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0d095-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0d095-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Evernote 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d095-136">In this section, you configure and test Azure AD single sign-on with Evernote based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0d095-137">若要讓單一登入運作，Azure AD 必須知道 Evernote 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="0d095-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Evernote is to a user in Azure AD.</span></span> <span data-ttu-id="0d095-138">換句話說，必須在 Azure AD 使用者和 Evernote 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0d095-138">In other words, a link relationship between an Azure AD user and the related user in Evernote needs to be established.</span></span>

<span data-ttu-id="0d095-139">在 Evernote 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0d095-139">In Evernote, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0d095-140">若要設定並測試透過 Evernote 使用 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0d095-140">To configure and test Azure AD single sign-on with Evernote, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0d095-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0d095-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0d095-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d095-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d095-143">**[建立 Evernote 測試使用者](#create-an-evernote-test-user)** - 在 Evernote 中建立一個與 Azure AD 中代表使用者之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="0d095-143">**[Create an Evernote test user](#create-an-evernote-test-user)** - to have a counterpart of Britta Simon in Evernote that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d095-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d095-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d095-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="0d095-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0d095-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0d095-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0d095-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Evernote 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d095-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Evernote application.</span></span>

<span data-ttu-id="0d095-148">**若要使用 Evernote 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0d095-148">**To configure Azure AD single sign-on with Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="0d095-149">在 Azure 入口網站的 [Evernote] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0d095-149">In the Azure portal, on the **Evernote** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="0d095-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d095-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_samlbase.png)

3. <span data-ttu-id="0d095-153">如果您想要以 IDP 起始模式設定應用程式，請在 [Evernote 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0d095-153">On the **Evernote Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Evernote 網域和 URL 單一登入資訊](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url.png)

    <span data-ttu-id="0d095-155">在 [識別碼] 文字方塊中，輸入 URL：`https://www.evernote.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="0d095-155">In the **Identifier** textbox, type the URL: `https://www.evernote.com/saml2`</span></span>

4. <span data-ttu-id="0d095-156">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0d095-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Evernote 網域和 URL 單一登入資訊](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_url1.png)

    <span data-ttu-id="0d095-158">在 [登入 URL] 文字方塊中，輸入 URL：`https://www.evernote.com/Login.action`</span><span class="sxs-lookup"><span data-stu-id="0d095-158">In the **Sign on URL** textbox, type the URL: `https://www.evernote.com/Login.action`</span></span>   

5. <span data-ttu-id="0d095-159">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0d095-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certificate.png) 

6. <span data-ttu-id="0d095-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d095-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-evernote-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0d095-163">在 [Evernote 組態] 區段上，按一下 [設定 Evernote] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="0d095-163">On the **Evernote Configuration** section, click **Configure Evernote** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0d095-164">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="0d095-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Evernote 組態](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_configure.png) 

8. <span data-ttu-id="0d095-166">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Evernote 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0d095-166">In a different web browser window, log into your Evernote company site as an administrator.</span></span>

9. <span data-ttu-id="0d095-167">移至 [管理主控台]</span><span class="sxs-lookup"><span data-stu-id="0d095-167">Go to **'Admin Console'**</span></span>

    ![管理主控台](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

10. <span data-ttu-id="0d095-169">從 [管理主控台]，移至 [安全性]，然後選取 [單一登入]</span><span class="sxs-lookup"><span data-stu-id="0d095-169">From the **'Admin Console'**, go to **‘Security’** and select **‘Single Sign-On’**</span></span>

    ![SSO 設定](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_sso.png)

11. <span data-ttu-id="0d095-171">設定下列值：</span><span class="sxs-lookup"><span data-stu-id="0d095-171">Configure the following values:</span></span>

    ![憑證設定](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_certx.png)
    
    <span data-ttu-id="0d095-173">a.</span><span class="sxs-lookup"><span data-stu-id="0d095-173">a.</span></span>  <span data-ttu-id="0d095-174">**啟用 SSO：**預設會啟用 SSO (按一下 [停用單一登入] 以移除 SSO 需求)</span><span class="sxs-lookup"><span data-stu-id="0d095-174">**Enable SSO:** SSO is enabled by default (Click **Disable Single Sign-on** to remove the SSO requirement)</span></span>

    <span data-ttu-id="0d095-175">b.</span><span class="sxs-lookup"><span data-stu-id="0d095-175">b.</span></span> <span data-ttu-id="0d095-176">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值，貼到 [SAML HTTP 要求 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="0d095-176">Paste **SAML Single sign-on Service URL** value, which you have copied from the Azure portal into the **SAML HTTP Request URL** textbox.</span></span>

    <span data-ttu-id="0d095-177">c.</span><span class="sxs-lookup"><span data-stu-id="0d095-177">c.</span></span> <span data-ttu-id="0d095-178">在記事本中開啟已從 Azure AD 下載的憑證並複製內容，包括 "BEGIN CERTIFICATE" 和 "END CERTIFICATE"，並將它貼入 [X.509 憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0d095-178">Open the downloaded certificate from Azure AD in a notepad and copy the content including "BEGIN CERTIFICATE" and "END CERTIFICATE" and paste it into the **X.509 Certificate** textbox.</span></span> 

    <span data-ttu-id="0d095-179">d. 按一下 [儲存變更]</span><span class="sxs-lookup"><span data-stu-id="0d095-179">d.Click **Save Changes**</span></span>

> [!TIP]
> <span data-ttu-id="0d095-180">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="0d095-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0d095-181">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="0d095-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0d095-182">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d095-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0d095-183">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0d095-183">Create an Azure AD test user</span></span>

<span data-ttu-id="0d095-184">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0d095-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="0d095-186">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0d095-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0d095-187">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d095-187">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-evernote-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0d095-189">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="0d095-189">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-evernote-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0d095-191">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0d095-191">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-evernote-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0d095-193">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0d095-193">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-evernote-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0d095-195">a.</span><span class="sxs-lookup"><span data-stu-id="0d095-195">a.</span></span> <span data-ttu-id="0d095-196">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0d095-196">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d095-197">b.</span><span class="sxs-lookup"><span data-stu-id="0d095-197">b.</span></span> <span data-ttu-id="0d095-198">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0d095-198">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0d095-199">c.</span><span class="sxs-lookup"><span data-stu-id="0d095-199">c.</span></span> <span data-ttu-id="0d095-200">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="0d095-200">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0d095-201">d.</span><span class="sxs-lookup"><span data-stu-id="0d095-201">d.</span></span> <span data-ttu-id="0d095-202">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0d095-202">Click **Create**.</span></span>
 
### <a name="create-an-evernote-test-user"></a><span data-ttu-id="0d095-203">建立 Evernote 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0d095-203">Create an Evernote test user</span></span>

<span data-ttu-id="0d095-204">若要讓 Azure AD 使用者可以登入 Evernote，則必須將他們佈建到 Evernote。</span><span class="sxs-lookup"><span data-stu-id="0d095-204">In order to enable Azure AD users to log into Evernote, they must be provisioned into Evernote.</span></span>  
<span data-ttu-id="0d095-205">Evernote 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="0d095-205">In the case of Evernote, provisioning is a manual task.</span></span>

<span data-ttu-id="0d095-206">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0d095-206">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="0d095-207">以系統管理員身分登入您的 Evernote 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0d095-207">Log in to your Evernote company site as an administrator.</span></span>

2. <span data-ttu-id="0d095-208">按一下 [管理主控台]。</span><span class="sxs-lookup"><span data-stu-id="0d095-208">Click the **'Admin Console'**.</span></span>

    ![管理主控台](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_adminconsole.png)

3. <span data-ttu-id="0d095-210">從 [管理主控台]，移至 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="0d095-210">From the **'Admin Console'**, go to **‘Add users’**.</span></span>

    ![新增測試使用者](./media/active-directory-saas-evernote-tutorial/create_aaduser_0001.png)

4. <span data-ttu-id="0d095-212">在 [新增小組成員]的 [電子郵件] 文字方塊中，輸入使用者帳戶的電子郵件地址，然後按一下 [邀請]。</span><span class="sxs-lookup"><span data-stu-id="0d095-212">**Add team members** in the **Email** textbox, type the email address of user account and click **Invite.**</span></span>

    ![新增測試使用者](./media/active-directory-saas-evernote-tutorial/create_aaduser_0002.png)
    
5. <span data-ttu-id="0d095-214">傳送邀請之後，Azure Active Directory 帳戶持有者會收到一封接受邀請的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0d095-214">After invitation is sent, the Azure Active Directory account holder will receive an email to accept the invitation.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0d095-215">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0d095-215">Assign the Azure AD test user</span></span>

<span data-ttu-id="0d095-216">在本節中，您會將 Evernote 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d095-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Evernote.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="0d095-218">**若要將 Britta Simon 指派到 Evernote，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="0d095-218">**To assign Britta Simon to Evernote, perform the following steps:**</span></span>

1. <span data-ttu-id="0d095-219">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0d095-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0d095-221">在應用程式清單中，選取 [Evernote]。</span><span class="sxs-lookup"><span data-stu-id="0d095-221">In the applications list, select **Evernote**.</span></span>

    ![應用程式清單中的 Evernote 連結](./media/active-directory-saas-evernote-tutorial/tutorial_evernote_app.png)  

3. <span data-ttu-id="0d095-223">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0d095-223">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="0d095-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d095-225">Click **Add** button.</span></span> <span data-ttu-id="0d095-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0d095-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="0d095-228">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="0d095-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0d095-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d095-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d095-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d095-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0d095-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0d095-231">Test single sign-on</span></span>

<span data-ttu-id="0d095-232">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="0d095-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0d095-233">當您在存取面板中按一下 Evernote 圖格時，應該會登入您的 Evernote 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d095-233">When you click the Evernote tile in the Access Panel, you should get signed-on to your Evernote application.</span></span> <span data-ttu-id="0d095-234">您將會以組織帳戶登入，但隨後需要以您的個人帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="0d095-234">You'll be logging in as an Organization account but then need to log in with your personal account.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0d095-235">其他資源</span><span class="sxs-lookup"><span data-stu-id="0d095-235">Additional resources</span></span>

* [<span data-ttu-id="0d095-236">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="0d095-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d095-237">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0d095-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evernote-tutorial/tutorial_general_203.png

