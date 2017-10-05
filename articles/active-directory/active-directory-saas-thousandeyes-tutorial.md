---
title: "教學課程：Azure Active Directory 與 ThousandEyes 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ThousandEyes 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: 392add7d5f0a55598b8b90760f5c3f2d1e67ac02
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a><span data-ttu-id="da44b-103">教學課程：Azure Active Directory 與 ThousandEyes 整合</span><span class="sxs-lookup"><span data-stu-id="da44b-103">Tutorial: Azure Active Directory integration with ThousandEyes</span></span>

<span data-ttu-id="da44b-104">在本教學課程中，您將了解如何整合 ThousandEyes 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="da44b-104">In this tutorial, you learn how to integrate ThousandEyes with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da44b-105">ThousandEyes 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="da44b-105">Integrating ThousandEyes with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="da44b-106">您可以在 Azure AD 中控制可存取 ThousandEyes 的人員</span><span class="sxs-lookup"><span data-stu-id="da44b-106">You can control in Azure AD who has access to ThousandEyes</span></span>
- <span data-ttu-id="da44b-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 ThousandEyes (單一登入)</span><span class="sxs-lookup"><span data-stu-id="da44b-107">You can enable your users to automatically get signed-on to ThousandEyes (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da44b-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="da44b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="da44b-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="da44b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da44b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="da44b-110">Prerequisites</span></span>

<span data-ttu-id="da44b-111">如要設定 Azure AD 與 ThousandEyes 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="da44b-111">To configure Azure AD integration with ThousandEyes, you need the following items:</span></span>

- <span data-ttu-id="da44b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="da44b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da44b-113">已啟用 ThousandEyes 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="da44b-113">A ThousandEyes single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da44b-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="da44b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da44b-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="da44b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da44b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="da44b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="da44b-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="da44b-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da44b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="da44b-118">Scenario description</span></span>
<span data-ttu-id="da44b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da44b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da44b-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="da44b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da44b-121">從資源庫新增 ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="da44b-121">Adding ThousandEyes from the gallery</span></span>
2. <span data-ttu-id="da44b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="da44b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thousandeyes-from-the-gallery"></a><span data-ttu-id="da44b-123">從資源庫新增 ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="da44b-123">Adding ThousandEyes from the gallery</span></span>
<span data-ttu-id="da44b-124">若要設定將 ThousandEyes 整合到 Azure AD 中，您需要從資源庫將 ThousandEyes 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="da44b-124">To configure the integration of ThousandEyes into Azure AD, you need to add ThousandEyes from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="da44b-125">**若要從資源庫新增 ThousandEyes，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="da44b-125">**To add ThousandEyes from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="da44b-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="da44b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da44b-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="da44b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="da44b-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="da44b-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="da44b-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da44b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="da44b-133">在搜尋方塊中，輸入 **ThousandEyes**。</span><span class="sxs-lookup"><span data-stu-id="da44b-133">In the search box, type **ThousandEyes**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. <span data-ttu-id="da44b-135">在結果窗格中，選取 [ThousandEyes]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="da44b-135">In the results panel, select **ThousandEyes**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da44b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="da44b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da44b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ThousandEyes 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da44b-138">In this section, you configure and test Azure AD single sign-on with ThousandEyes based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="da44b-139">若要讓單一登入能夠運作，Azure AD 必須知道 ThousandEyes 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="da44b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThousandEyes is to a user in Azure AD.</span></span> <span data-ttu-id="da44b-140">換句話說，必須在 Azure AD 使用者和 ThousandEyes 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="da44b-140">In other words, a link relationship between an Azure AD user and the related user in ThousandEyes needs to be established.</span></span>

<span data-ttu-id="da44b-141">在 ThousandEyes 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="da44b-141">In ThousandEyes, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="da44b-142">若要設定及測試與 ThousandEyes 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="da44b-142">To configure and test Azure AD single sign-on with ThousandEyes, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="da44b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="da44b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="da44b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da44b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da44b-145">**[建立 ThousandEyes 測試使用者](#creating-a-thousandeyes-test-user)** - 使 ThousandEyes 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="da44b-145">**[Creating a ThousandEyes test user](#creating-a-thousandeyes-test-user)** - to have a counterpart of Britta Simon in ThousandEyes that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="da44b-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da44b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da44b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="da44b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da44b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="da44b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da44b-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 ThousandEyes 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="da44b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThousandEyes application.</span></span>

<span data-ttu-id="da44b-150">**若要使用 ThousandEyes 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="da44b-150">**To configure Azure AD single sign-on with ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="da44b-151">在 Azure 入口網站的 [ThousandEyes] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="da44b-151">In the Azure portal, on the **ThousandEyes** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="da44b-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="da44b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. <span data-ttu-id="da44b-155">在 [ThousandEyes 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="da44b-155">On the **ThousandEyes Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    <span data-ttu-id="da44b-157">在 [登入 URL] 文字方塊中，將 URL 輸入為：`https://app.thousandeyes.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="da44b-157">In the **Sign-on URL** textbox, type a URL as: `https://app.thousandeyes.com/login/sso`</span></span>

4. <span data-ttu-id="da44b-158">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="da44b-158">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. <span data-ttu-id="da44b-160">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="da44b-160">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="da44b-162">在 [ThousandEyes 組態] 區段上，按一下 [設定 ThousandEyes] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="da44b-162">On the **ThousandEyes Configuration** section, click **Configure ThousandEyes** to open **Configure sign-on** window.</span></span> <span data-ttu-id="da44b-163">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="da44b-163">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. <span data-ttu-id="da44b-165">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **ThousandEyes** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="da44b-165">In a different web browser window, sign on to your **ThousandEyes** company site as an administrator.</span></span>

8. <span data-ttu-id="da44b-166">在頂端的功能表中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="da44b-166">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="da44b-167">![設定](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "設定")</span><span class="sxs-lookup"><span data-stu-id="da44b-167">![Settings](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Settings")</span></span>

9. <span data-ttu-id="da44b-168">按一下 [帳戶] </span><span class="sxs-lookup"><span data-stu-id="da44b-168">Click **Account**</span></span>
   
    <span data-ttu-id="da44b-169">![帳戶](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "帳戶")</span><span class="sxs-lookup"><span data-stu-id="da44b-169">![Account](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Account")</span></span>

10. <span data-ttu-id="da44b-170">按一下 [安全性與驗證] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da44b-170">Click the **Security & Authentication** tab.</span></span>
   
    <span data-ttu-id="da44b-171">![安全性和驗證](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "安全性和驗證")</span><span class="sxs-lookup"><span data-stu-id="da44b-171">![Security & Authentication](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Security & Authentication")</span></span>

11. <span data-ttu-id="da44b-172">在 [設定單一登入]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="da44b-172">In the **Setup Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="da44b-173">![設定單一登入](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="da44b-173">![Setup Single Sign-On](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Setup Single Sign-On")</span></span>
  
    <span data-ttu-id="da44b-174">a.</span><span class="sxs-lookup"><span data-stu-id="da44b-174">a.</span></span> <span data-ttu-id="da44b-175">選取 [啟用單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="da44b-175">Select **Enable Single Sign-On**.</span></span>
  
    <span data-ttu-id="da44b-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="da44b-176">b.</span></span> <span data-ttu-id="da44b-177">在 [登入頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="da44b-177">In **Login Page URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="da44b-178">c.</span><span class="sxs-lookup"><span data-stu-id="da44b-178">c.</span></span> <span data-ttu-id="da44b-179">在 [登出頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL]。</span><span class="sxs-lookup"><span data-stu-id="da44b-179">In **Logout Page URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="da44b-180">d.</span><span class="sxs-lookup"><span data-stu-id="da44b-180">d.</span></span> <span data-ttu-id="da44b-181">在 [識別提供者簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="da44b-181">**Identity Provider Issuer** textbox, paste **SAML Entity ID** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="da44b-182">e.</span><span class="sxs-lookup"><span data-stu-id="da44b-182">e.</span></span> <span data-ttu-id="da44b-183">在 [驗證憑證] 中，按一下 [選擇檔案]，然後上傳您從 Azure 入口網站下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="da44b-183">In **Verification Certificate**, click **Choose file**, and then upload the certificate you have downloaded from Azure portal.</span></span>
  
    <span data-ttu-id="da44b-184">f.</span><span class="sxs-lookup"><span data-stu-id="da44b-184">f.</span></span> <span data-ttu-id="da44b-185">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="da44b-185">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="da44b-186">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="da44b-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="da44b-187">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="da44b-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="da44b-188">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="da44b-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da44b-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="da44b-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="da44b-190">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="da44b-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="da44b-192">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="da44b-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="da44b-193">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="da44b-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da44b-195">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="da44b-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da44b-197">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="da44b-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da44b-199">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="da44b-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da44b-201">a.</span><span class="sxs-lookup"><span data-stu-id="da44b-201">a.</span></span> <span data-ttu-id="da44b-202">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="da44b-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da44b-203">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="da44b-203">b.</span></span> <span data-ttu-id="da44b-204">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="da44b-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da44b-205">c.</span><span class="sxs-lookup"><span data-stu-id="da44b-205">c.</span></span> <span data-ttu-id="da44b-206">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="da44b-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="da44b-207">d.</span><span class="sxs-lookup"><span data-stu-id="da44b-207">d.</span></span> <span data-ttu-id="da44b-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="da44b-208">Click **Create**.</span></span>
 
### <a name="creating-a-thousandeyes-test-user"></a><span data-ttu-id="da44b-209">建立 ThousandEyes 測試使用者</span><span class="sxs-lookup"><span data-stu-id="da44b-209">Creating a ThousandEyes test user</span></span>

<span data-ttu-id="da44b-210">若要讓 Azure AD 使用者可以登入 ThousandEyes，則必須將他們佈建到 ThousandEyes。</span><span class="sxs-lookup"><span data-stu-id="da44b-210">In order to enable Azure AD users to log into ThousandEyes, they must be provisioned into ThousandEyes.</span></span>  
<span data-ttu-id="da44b-211">ThousandEyes 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="da44b-211">In the case of ThousandEyes, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="da44b-212">您可以使用任何其他的 ThousandEyes 使用者帳戶建立工具或 ThousandEyes 提供的 API 來佈建 Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="da44b-212">You can use any other ThousandEyes user account creation tools or APIs provided by ThousandEyes to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="da44b-213">**若要將使用者帳戶佈建到 ThousandEyes，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="da44b-213">**To provision a user account to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="da44b-214">以系統管理員身分登入您的 ThousandEyes 公司網站。</span><span class="sxs-lookup"><span data-stu-id="da44b-214">Log into your ThousandEyes company site as an administrator.</span></span>

2. <span data-ttu-id="da44b-215">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="da44b-215">Click **Settings**.</span></span>
   
    <span data-ttu-id="da44b-216">![設定](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "設定")</span><span class="sxs-lookup"><span data-stu-id="da44b-216">![Settings](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Settings")</span></span>

3. <span data-ttu-id="da44b-217">按一下 [帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="da44b-217">Click **Account**.</span></span>
   
    <span data-ttu-id="da44b-218">![帳戶](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "帳戶")</span><span class="sxs-lookup"><span data-stu-id="da44b-218">![Account](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Account")</span></span>

4. <span data-ttu-id="da44b-219">按一下 [帳戶和使用者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da44b-219">Click the **Accounts & Users** tab.</span></span>
   
    <span data-ttu-id="da44b-220">![帳戶和使用者](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "帳戶和使用者")</span><span class="sxs-lookup"><span data-stu-id="da44b-220">![Accounts & Users](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Accounts & Users")</span></span>

5. <span data-ttu-id="da44b-221">在 [加入使用者和帳戶] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="da44b-221">In the **Add Users & Accounts** section, perform the following steps:</span></span>
   
    <span data-ttu-id="da44b-222">![新增使用者帳戶](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "新增使用者帳戶")</span><span class="sxs-lookup"><span data-stu-id="da44b-222">![Add User Accounts](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Add User Accounts")</span></span>   
  
    <span data-ttu-id="da44b-223">a.</span><span class="sxs-lookup"><span data-stu-id="da44b-223">a.</span></span> <span data-ttu-id="da44b-224">在 [名稱] 文字方塊中，輸入使用者的名稱，例如 **Britta Simon**。</span><span class="sxs-lookup"><span data-stu-id="da44b-224">In **Name** textbox, type the name of user like **Britta Simon**.</span></span>

    <span data-ttu-id="da44b-225">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="da44b-225">b.</span></span> <span data-ttu-id="da44b-226">在 [電子郵件] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="da44b-226">In **Email** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="da44b-227">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="da44b-227">b.</span></span> <span data-ttu-id="da44b-228">按一下 [加入使用者至帳戶] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da44b-228">Click **Add New User to Account**.</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="da44b-229">Azure Active Directory 帳戶的持有者會收到一封包含連結的電子郵件，以供其確認並啟用帳戶。</span><span class="sxs-lookup"><span data-stu-id="da44b-229">The Azure Active Directory account holder will get an email including a link to confirm and activate the account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="da44b-230">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="da44b-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="da44b-231">在本節中，您會將 ThousandEyes 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="da44b-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThousandEyes.</span></span>

![指派使用者][200] 

<span data-ttu-id="da44b-233">**若要將 Britta Simon 指派給 ThousandEyes，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="da44b-233">**To assign Britta Simon to ThousandEyes, perform the following steps:**</span></span>

1. <span data-ttu-id="da44b-234">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="da44b-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="da44b-236">在應用程式清單中，選取 [ThousandEyes]。</span><span class="sxs-lookup"><span data-stu-id="da44b-236">In the applications list, select **ThousandEyes**.</span></span>

    ![設定單一登入](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. <span data-ttu-id="da44b-238">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="da44b-238">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="da44b-240">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da44b-240">Click **Add** button.</span></span> <span data-ttu-id="da44b-241">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="da44b-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="da44b-243">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="da44b-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="da44b-244">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da44b-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da44b-245">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="da44b-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="da44b-246">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="da44b-246">Testing single sign-on</span></span>

<span data-ttu-id="da44b-247">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="da44b-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="da44b-248">當您在「存取面板」中按一下 [ThousandEyes] 圖格時，應該會自動登入您的 ThousandEyes 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da44b-248">When you click the ThousandEyes tile in the Access Panel, you should get automatically signed-on to your ThousandEyes application.</span></span>

<span data-ttu-id="da44b-249">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="da44b-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="da44b-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="da44b-250">Additional resources</span></span>

* [<span data-ttu-id="da44b-251">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="da44b-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da44b-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="da44b-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

