---
title: "教學課程：Azure Active Directory 與 Bonusly 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Bonusly 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 29a88b2efdb9f0f33f7933bc654a5a0fdf589c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="7031f-103">教學課程：Azure Active Directory 與 Bonusly 整合</span><span class="sxs-lookup"><span data-stu-id="7031f-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="7031f-104">在本教學課程中，您將了解如何整合 Bonusly 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="7031f-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7031f-105">將 Bonusly 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7031f-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7031f-106">您可以在 Azure AD 中控制可存取 Bonusly 的人員</span><span class="sxs-lookup"><span data-stu-id="7031f-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="7031f-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Bonusly (單一登入)</span><span class="sxs-lookup"><span data-stu-id="7031f-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7031f-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="7031f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7031f-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7031f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7031f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7031f-110">Prerequisites</span></span>

<span data-ttu-id="7031f-111">若要設定 Azure AD 與 Bonusly 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7031f-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="7031f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7031f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7031f-113">已啟用 Bonusly 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7031f-113">A Bonusly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7031f-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7031f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7031f-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7031f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7031f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7031f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7031f-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7031f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7031f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7031f-118">Scenario description</span></span>
<span data-ttu-id="7031f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7031f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7031f-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7031f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7031f-121">從資源庫新增 Bonusly</span><span class="sxs-lookup"><span data-stu-id="7031f-121">Adding Bonusly from the gallery</span></span>
2. <span data-ttu-id="7031f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7031f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="7031f-123">從資源庫新增 Bonusly</span><span class="sxs-lookup"><span data-stu-id="7031f-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="7031f-124">若要設定將 Bonusly 整合到 Azure AD 中，您需要從資源庫將 Bonusly 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7031f-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7031f-125">**若要從資源庫新增 Bonusly，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7031f-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7031f-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7031f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="7031f-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7031f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7031f-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7031f-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="7031f-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7031f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="7031f-133">在搜尋方塊中，輸入 **Bonusly**，從結果面板中選取 [Bonusly]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7031f-133">In the search box, type **Bonusly**, select **Bonusly** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7031f-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7031f-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="7031f-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Bonusly 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7031f-136">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7031f-137">若要讓單一登入能夠運作，Azure AD 必須知道 Bonusly 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7031f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="7031f-138">換句話說，必須建立 Azure AD 使用者和 Bonusly 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7031f-138">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="7031f-139">在 Bonusly 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7031f-139">In Bonusly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7031f-140">若要使用 Bonusly 設定及測試 Azure AD 單一登入功能，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="7031f-140">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7031f-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7031f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7031f-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7031f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7031f-143">**[建立 Bonusly 測試使用者](#create-a-bonusly-test-user)** - 在 Bonusly 中建立一個與 Azure AD 中代表使用者之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="7031f-143">**[Create a Bonusly test user](#create-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7031f-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7031f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7031f-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7031f-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7031f-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7031f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7031f-147">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，並在您的 Bonusly 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7031f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="7031f-148">**若要使用 Bonusly 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7031f-148">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="7031f-149">在 Azure 入口網站的 [Bonusly] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7031f-149">In the Azure portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="7031f-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7031f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. <span data-ttu-id="7031f-153">在 [Bonusly 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7031f-153">On the **Bonusly Domain and URLs** section, perform the following steps:</span></span>

    ![Bonusly 網域及 URL 單一登入資訊](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    <span data-ttu-id="7031f-155">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://Bonus.ly/saml/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="7031f-155">In the **Reply URL** textbox, type a URL using the following pattern: `https://Bonus.ly/saml/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7031f-156">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="7031f-156">The value is not real.</span></span> <span data-ttu-id="7031f-157">請使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="7031f-157">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="7031f-158">請連絡 [Bonusly 支援小組](https://Bonusly/contact)以取得該值。</span><span class="sxs-lookup"><span data-stu-id="7031f-158">Contact [Bonusly support team](https://Bonusly/contact) to get the value.</span></span>
 
4. <span data-ttu-id="7031f-159">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="7031f-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![憑證下載連結](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. <span data-ttu-id="7031f-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7031f-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7031f-163">在 [Bonusly 組態] 區段上，按一下 [設定 Bonusly] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="7031f-163">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7031f-164">從 [快速參考] 區段中複製 [SAML 實體識別碼] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="7031f-164">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Bonusly 組態](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. <span data-ttu-id="7031f-166">在不同的瀏覽器視窗中，登入您的 **Bonusly** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7031f-166">In a different browser window, log in to your **Bonusly** tenant.</span></span>

8. <span data-ttu-id="7031f-167">在頂端工具列中，按一下 [設定]，然後選取 [整合與應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7031f-167">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>
   
    <span data-ttu-id="7031f-168">![Bonusly 社交區段](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="7031f-168">![Bonusly Social Section](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")</span></span>
9. <span data-ttu-id="7031f-169">在 [單一登入] 下方，選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="7031f-169">Under **Single Sign-On**, select **SAML**.</span></span>

10. <span data-ttu-id="7031f-170">在 [SAML]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7031f-170">On the **SAML** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="7031f-171">![Bonusly Saml 對話方塊頁面](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span><span class="sxs-lookup"><span data-stu-id="7031f-171">![Bonusly Saml Dialog page](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")</span></span>
   
    <span data-ttu-id="7031f-172">a.</span><span class="sxs-lookup"><span data-stu-id="7031f-172">a.</span></span> <span data-ttu-id="7031f-173">在 [IdP SSO 目標 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="7031f-173">In the **IdP SSO target URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="7031f-174">b.</span><span class="sxs-lookup"><span data-stu-id="7031f-174">b.</span></span> <span data-ttu-id="7031f-175">在 [IdP 簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="7031f-175">In the **IdP Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="7031f-176">c.</span><span class="sxs-lookup"><span data-stu-id="7031f-176">c.</span></span> <span data-ttu-id="7031f-177">在 [IdP 登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="7031f-177">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7031f-178">d.</span><span class="sxs-lookup"><span data-stu-id="7031f-178">d.</span></span> <span data-ttu-id="7031f-179">在 [憑證指紋] 文字方塊中貼上從 Azure 入口網站複製的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="7031f-179">Paste the **Thumbprint** value copied from Azure portal into the **Cert Fingerprint** textbox.</span></span>
   
11. <span data-ttu-id="7031f-180">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7031f-180">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7031f-181">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7031f-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7031f-182">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7031f-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7031f-183">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7031f-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7031f-184">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7031f-184">Create an Azure AD test user</span></span>
<span data-ttu-id="7031f-185">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7031f-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="7031f-187">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7031f-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7031f-188">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7031f-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7031f-190">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7031f-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7031f-192">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7031f-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7031f-194">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7031f-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7031f-196">a.</span><span class="sxs-lookup"><span data-stu-id="7031f-196">a.</span></span> <span data-ttu-id="7031f-197">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7031f-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7031f-198">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7031f-198">b.</span></span> <span data-ttu-id="7031f-199">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="7031f-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7031f-200">c.</span><span class="sxs-lookup"><span data-stu-id="7031f-200">c.</span></span> <span data-ttu-id="7031f-201">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="7031f-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7031f-202">d.</span><span class="sxs-lookup"><span data-stu-id="7031f-202">d.</span></span> <span data-ttu-id="7031f-203">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7031f-203">Click **Create**.</span></span>
 
### <a name="create-a-bonusly-test-user"></a><span data-ttu-id="7031f-204">建立 Bonusly 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7031f-204">Create a Bonusly test user</span></span>

<span data-ttu-id="7031f-205">若要讓 Azure AD 使用者可以登入 Bonusly，必須將他們佈建到 Bonusly。</span><span class="sxs-lookup"><span data-stu-id="7031f-205">In order to enable Azure AD users to log in to Bonusly, they must be provisioned into Bonusly.</span></span> <span data-ttu-id="7031f-206">Bonusly 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="7031f-206">In the case of Bonusly, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="7031f-207">您可使用任何其他的 Bonusly 使用者帳戶建立工具，或是使用 Bonusly 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7031f-207">You can use any other Bonusly user account creation tools or APIs provided by Bonusly to provision AAD user accounts.</span></span>
>  

<span data-ttu-id="7031f-208">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7031f-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="7031f-209">在網頁瀏覽器視窗中，登入您的 Bonusly 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7031f-209">In a web browser window, log in to your Bonusly tenant.</span></span>

2. <span data-ttu-id="7031f-210">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="7031f-210">Click **Settings**.</span></span>
 
    <span data-ttu-id="7031f-211">![設定](./media/active-directory-saas-bonus-tutorial/ic781041.png "設定")</span><span class="sxs-lookup"><span data-stu-id="7031f-211">![Settings](./media/active-directory-saas-bonus-tutorial/ic781041.png "Settings")</span></span>

3. <span data-ttu-id="7031f-212">按一下 [使用者和獎勵]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7031f-212">Click the **Users and bonuses** tab.</span></span>
   
    <span data-ttu-id="7031f-213">![使用者和獎勵](./media/active-directory-saas-bonus-tutorial/ic781042.png "使用者和獎勵")</span><span class="sxs-lookup"><span data-stu-id="7031f-213">![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")</span></span>

4. <span data-ttu-id="7031f-214">按一下 [管理使用者] 。</span><span class="sxs-lookup"><span data-stu-id="7031f-214">Click **Manage Users**.</span></span>
   
    <span data-ttu-id="7031f-215">![管理使用者](./media/active-directory-saas-bonus-tutorial/ic781043.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="7031f-215">![Manage Users](./media/active-directory-saas-bonus-tutorial/ic781043.png "Manage Users")</span></span>

5. <span data-ttu-id="7031f-216">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="7031f-216">Click **Add User**.</span></span>
   
    <span data-ttu-id="7031f-217">![新增使用者](./media/active-directory-saas-bonus-tutorial/ic781044.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="7031f-217">![Add User](./media/active-directory-saas-bonus-tutorial/ic781044.png "Add User")</span></span>

6. <span data-ttu-id="7031f-218">在 [加入使用者]  對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7031f-218">On the **Add User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="7031f-219">![新增使用者](./media/active-directory-saas-bonus-tutorial/ic781045.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="7031f-219">![Add User](./media/active-directory-saas-bonus-tutorial/ic781045.png "Add User")</span></span>  

    <span data-ttu-id="7031f-220">a.</span><span class="sxs-lookup"><span data-stu-id="7031f-220">a.</span></span> <span data-ttu-id="7031f-221">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="7031f-221">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="7031f-222">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7031f-222">b.</span></span> <span data-ttu-id="7031f-223">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="7031f-223">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="7031f-224">c.</span><span class="sxs-lookup"><span data-stu-id="7031f-224">c.</span></span> <span data-ttu-id="7031f-225">在 [電子郵件] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="7031f-225">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="7031f-226">d.</span><span class="sxs-lookup"><span data-stu-id="7031f-226">d.</span></span> <span data-ttu-id="7031f-227">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7031f-227">Click **Save**.</span></span>
   
     >[!NOTE]
     ><span data-ttu-id="7031f-228">Azure AD 帳戶持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="7031f-228">The Azure AD account holder receives an email that includes a link to confirm the account before it becomes active.</span></span>
     >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7031f-229">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7031f-229">Assign the Azure AD test user</span></span>

<span data-ttu-id="7031f-230">在本節中，您會將 Bonusly 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7031f-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bonusly.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="7031f-232">**若要將 Britta Simon 指派到 Bonusly，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7031f-232">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="7031f-233">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7031f-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7031f-235">在應用程式清單中，選取 [Bonusly]。</span><span class="sxs-lookup"><span data-stu-id="7031f-235">In the applications list, select **Bonusly**.</span></span>

    ![應用程式清單中的 Bonusly 連結](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. <span data-ttu-id="7031f-237">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7031f-237">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202] 

4. <span data-ttu-id="7031f-239">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7031f-239">Click **Add** button.</span></span> <span data-ttu-id="7031f-240">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7031f-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="7031f-242">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7031f-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7031f-243">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7031f-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7031f-244">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7031f-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7031f-245">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7031f-245">Test single sign-on</span></span>

<span data-ttu-id="7031f-246">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="7031f-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7031f-247">當您在存取面板中按一下 Bonusly 圖格時，應該會自動登入 Bonusly 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7031f-247">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7031f-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="7031f-248">Additional resources</span></span>

* [<span data-ttu-id="7031f-249">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7031f-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7031f-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7031f-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

