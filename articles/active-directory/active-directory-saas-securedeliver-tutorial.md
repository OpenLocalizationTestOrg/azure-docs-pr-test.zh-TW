---
title: "教學課程：Azure Active Directory 與 SECURE DELIVER 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SECURE DELIVER 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fccd5668-fe6f-4e6d-a9ce-ba4f321c33d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: f6e5b1e34893f6b8fe14e238e24086bb47d009a5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-secure-deliver"></a><span data-ttu-id="25205-103">教學課程：Azure Active Directory 與 SECURE DELIVER 整合</span><span class="sxs-lookup"><span data-stu-id="25205-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span></span>

<span data-ttu-id="25205-104">在本教學課程中，您將了解如何整合 SECURE DELIVER 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="25205-104">In this tutorial, you learn how to integrate SECURE DELIVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25205-105">SECURE DELIVER 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="25205-105">Integrating SECURE DELIVER with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="25205-106">您可以在 Azure AD 中控制可存取 SECURE DELIVER 的人員</span><span class="sxs-lookup"><span data-stu-id="25205-106">You can control in Azure AD who has access to SECURE DELIVER</span></span>
- <span data-ttu-id="25205-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SECURE DELIVER (單一登入)</span><span class="sxs-lookup"><span data-stu-id="25205-107">You can enable your users to automatically get signed-on to SECURE DELIVER (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="25205-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="25205-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="25205-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="25205-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25205-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="25205-110">Prerequisites</span></span>

<span data-ttu-id="25205-111">若要設定 Azure AD 與 SECURE DELIVER 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="25205-111">To configure Azure AD integration with SECURE DELIVER, you need the following items:</span></span>

- <span data-ttu-id="25205-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="25205-112">An Azure AD subscription</span></span>
- <span data-ttu-id="25205-113">已啟用 SECURE DELIVER 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="25205-113">A SECURE DELIVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="25205-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="25205-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="25205-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="25205-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="25205-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="25205-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="25205-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="25205-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25205-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="25205-118">Scenario description</span></span>
<span data-ttu-id="25205-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="25205-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="25205-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="25205-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25205-121">從資源庫加入 SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="25205-121">Adding SECURE DELIVER from the gallery</span></span>
2. <span data-ttu-id="25205-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="25205-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-secure-deliver-from-the-gallery"></a><span data-ttu-id="25205-123">從資源庫加入 SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="25205-123">Adding SECURE DELIVER from the gallery</span></span>
<span data-ttu-id="25205-124">若要設定 SECURE DELIVER 與 Azure AD 整合，您需要從資源庫將 SECURE DELIVER 加入到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="25205-124">To configure the integration of SECURE DELIVER into Azure AD, you need to add SECURE DELIVER from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="25205-125">**若要從資源庫加入 SECURE DELIVER，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="25205-125">**To add SECURE DELIVER from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="25205-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="25205-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="25205-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="25205-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="25205-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="25205-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="25205-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="25205-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="25205-133">在搜尋方塊中，輸入 **SECURE DELIVER**。</span><span class="sxs-lookup"><span data-stu-id="25205-133">In the search box, type **SECURE DELIVER**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_search.png)

5. <span data-ttu-id="25205-135">在結果窗格中，選取 [SECURE DELIVER]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="25205-135">In the results panel, select **SECURE DELIVER**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="25205-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="25205-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="25205-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SECURE DELIVER 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="25205-138">In this section, you configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25205-139">若要讓單一登入運作，Azure AD 必須知道 SECURE DELIVER 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="25205-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SECURE DELIVER is to a user in Azure AD.</span></span> <span data-ttu-id="25205-140">換句話說，必須在 Azure AD 使用者與 SECURE DELIVER 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="25205-140">In other words, a link relationship between an Azure AD user and the related user in SECURE DELIVER needs to be established.</span></span>

<span data-ttu-id="25205-141">在 SECURE DELIVER 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="25205-141">In SECURE DELIVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="25205-142">若要使用 SECURE DELIVER 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="25205-142">To configure and test Azure AD single sign-on with SECURE DELIVER, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="25205-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="25205-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="25205-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="25205-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25205-145">**[建立 SECURE DELIVER 測試使用者](#creating-a-secure-deliver-test-user)** - 使 SECURE DELIVER 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="25205-145">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - to have a counterpart of Britta Simon in SECURE DELIVER that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="25205-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="25205-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25205-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="25205-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="25205-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="25205-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="25205-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 SECURE DELIVER 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="25205-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SECURE DELIVER application.</span></span>

<span data-ttu-id="25205-150">**若要使用 SECURE DELIVER 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="25205-150">**To configure Azure AD single sign-on with SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="25205-151">在 Azure 入口網站的 [SECURE DELIVER] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="25205-151">In the Azure portal, on the **SECURE DELIVER** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="25205-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="25205-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_samlbase.png)

3. <span data-ttu-id="25205-155">在 [SECURE DELIVER 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="25205-155">On the **SECURE DELIVER Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_url.png)

    <span data-ttu-id="25205-157">a.</span><span class="sxs-lookup"><span data-stu-id="25205-157">a.</span></span> <span data-ttu-id="25205-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span><span class="sxs-lookup"><span data-stu-id="25205-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span></span>

    <span data-ttu-id="25205-159">b.</span><span class="sxs-lookup"><span data-stu-id="25205-159">b.</span></span> <span data-ttu-id="25205-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span><span class="sxs-lookup"><span data-stu-id="25205-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="25205-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="25205-161">These values are not real.</span></span> <span data-ttu-id="25205-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="25205-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="25205-163">請連絡 [SECURE DELIVER 客戶支援小組](mailto:iw-sd-support@fujifilm.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="25205-163">Contact [SECURE DELIVER Client support team](mailto:iw-sd-support@fujifilm.com) to get these values.</span></span> 
 
4. <span data-ttu-id="25205-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="25205-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_certificate.png) 

5. <span data-ttu-id="25205-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="25205-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="25205-168">在 [SECURE DELIVER 組態] 區段上，按一下 [設定 SECURE DELIVER] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="25205-168">On the **SECURE DELIVER Configuration** section, click **Configure SECURE DELIVER** to open **Configure sign-on** window.</span></span> <span data-ttu-id="25205-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="25205-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_configure.png) 

7. <span data-ttu-id="25205-171">若要在 **SECURE DELIVER** 端設定單一登入，您必須將下載的**憑證 (Base64)**、**登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL** 傳送至 [SECURE DELIVER 支援小組](mailto:iw-sd-support@fujifilm.com)。</span><span class="sxs-lookup"><span data-stu-id="25205-171">To configure single sign-on on **SECURE DELIVER** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com).</span></span> <span data-ttu-id="25205-172">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="25205-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="25205-173">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="25205-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="25205-174">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="25205-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="25205-175">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="25205-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="25205-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="25205-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="25205-177">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="25205-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="25205-179">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="25205-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="25205-180">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="25205-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="25205-182">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="25205-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="25205-184">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="25205-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="25205-186">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="25205-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="25205-188">a.</span><span class="sxs-lookup"><span data-stu-id="25205-188">a.</span></span> <span data-ttu-id="25205-189">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="25205-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="25205-190">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="25205-190">b.</span></span> <span data-ttu-id="25205-191">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="25205-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="25205-192">c.</span><span class="sxs-lookup"><span data-stu-id="25205-192">c.</span></span> <span data-ttu-id="25205-193">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="25205-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="25205-194">d.</span><span class="sxs-lookup"><span data-stu-id="25205-194">d.</span></span> <span data-ttu-id="25205-195">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="25205-195">Click **Create**.</span></span>
 
### <a name="creating-a-secure-deliver-test-user"></a><span data-ttu-id="25205-196">建立 SECURE DELIVER 測試使用者</span><span class="sxs-lookup"><span data-stu-id="25205-196">Creating a SECURE DELIVER test user</span></span>

<span data-ttu-id="25205-197">本節的目標是在 SECURE DELIVER 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="25205-197">The objective of this section is to create a user called Britta Simon in SECURE DELIVER.</span></span> <span data-ttu-id="25205-198">請與 [SECURE DELIVER 支援小組](mailto:iw-sd-support@fujifilm.com)合作，以在 SECURE DELIVER 帳戶中加入使用者。</span><span class="sxs-lookup"><span data-stu-id="25205-198">Work with [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com) to add the users in the SECURE DELIVER account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="25205-199">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="25205-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="25205-200">在本節中，您會將 SECURE DELIVER 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="25205-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SECURE DELIVER.</span></span>

![指派使用者][200] 

<span data-ttu-id="25205-202">**若要將 Britta Simon 指派到 SECURE DELIVER，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="25205-202">**To assign Britta Simon to SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="25205-203">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="25205-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="25205-205">在應用程式清單中，選取 [SECURE DELIVER] 。</span><span class="sxs-lookup"><span data-stu-id="25205-205">In the applications list, select **SECURE DELIVER**.</span></span>

    ![設定單一登入](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_app.png) 

3. <span data-ttu-id="25205-207">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="25205-207">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="25205-209">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="25205-209">Click **Add** button.</span></span> <span data-ttu-id="25205-210">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="25205-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="25205-212">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="25205-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="25205-213">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="25205-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="25205-214">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="25205-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="25205-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="25205-215">Testing single sign-on</span></span>

<span data-ttu-id="25205-216">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="25205-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="25205-217">當您在存取面板中按一下 [SECURE DELIVER] 圖格時，應該會自動登入您的 SECURE DELIVER 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25205-217">When you click the SECURE DELIVER tile in the Access Panel, you should get automatically signed-on to your SECURE DELIVER application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25205-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="25205-218">Additional resources</span></span>

* [<span data-ttu-id="25205-219">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="25205-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25205-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="25205-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_203.png

