---
title: "教學課程：Azure Active Directory 與 Kintone 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Kintone 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: e5e847c12cba3611ce7ea2c3e956dbd55b1e0cac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="65bc9-103">教學課程：Azure Active Directory 與 Kintone 整合</span><span class="sxs-lookup"><span data-stu-id="65bc9-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="65bc9-104">在本教學課程中，您將了解如何整合 Kintone 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="65bc9-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65bc9-105">Kintone 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="65bc9-105">Integrating Kintone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65bc9-106">您可以在 Azure AD 中控制可存取 Kintone 的人員</span><span class="sxs-lookup"><span data-stu-id="65bc9-106">You can control in Azure AD who has access to Kintone</span></span>
- <span data-ttu-id="65bc9-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Kintone (單一登入)</span><span class="sxs-lookup"><span data-stu-id="65bc9-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="65bc9-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="65bc9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="65bc9-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="65bc9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65bc9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="65bc9-110">Prerequisites</span></span>

<span data-ttu-id="65bc9-111">若要設定 Azure AD 與 Kintone 的整合作業，需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="65bc9-111">To configure Azure AD integration with Kintone, you need the following items:</span></span>

- <span data-ttu-id="65bc9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="65bc9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65bc9-113">啟用 Kintone 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="65bc9-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65bc9-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="65bc9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65bc9-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="65bc9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65bc9-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="65bc9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65bc9-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="65bc9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65bc9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="65bc9-118">Scenario description</span></span>
<span data-ttu-id="65bc9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65bc9-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="65bc9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65bc9-121">從資源庫新增 Kintone</span><span class="sxs-lookup"><span data-stu-id="65bc9-121">Adding Kintone from the gallery</span></span>
2. <span data-ttu-id="65bc9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="65bc9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-the-gallery"></a><span data-ttu-id="65bc9-123">從資源庫新增 Kintone</span><span class="sxs-lookup"><span data-stu-id="65bc9-123">Adding Kintone from the gallery</span></span>
<span data-ttu-id="65bc9-124">若要設定將 Kintone 整合到 Azure AD 中，您需要從資源庫將 Kintone 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="65bc9-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65bc9-125">**若要從資源庫新增 Kintone，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="65bc9-125">**To add Kintone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65bc9-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="65bc9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="65bc9-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65bc9-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="65bc9-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="65bc9-133">在搜尋方塊中，輸入 **Kintone**。</span><span class="sxs-lookup"><span data-stu-id="65bc9-133">In the search box, type **Kintone**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="65bc9-135">在結果窗格中，選取 [Kintone]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="65bc9-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="65bc9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="65bc9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="65bc9-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Kintone 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc9-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65bc9-139">若要讓單一登入運作，Azure AD 必須知道 Kintone 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="65bc9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span></span> <span data-ttu-id="65bc9-140">換句話說，必須建立 Azure AD 使用者和 Kintone 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="65bc9-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span></span>

<span data-ttu-id="65bc9-141">在 Kintone 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="65bc9-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65bc9-142">若要設定及測試與 Kintone 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="65bc9-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65bc9-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="65bc9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65bc9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65bc9-145">**[建立 Kintone 測試使用者](#creating-a-kintone-test-user)** - 使 Kintone 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="65bc9-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65bc9-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65bc9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="65bc9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="65bc9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="65bc9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="65bc9-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Kintone 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="65bc9-150">**若要設定與 Kintone 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="65bc9-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="65bc9-151">在 Azure 入口網站的 [Kintone] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="65bc9-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="65bc9-155">在 [Kintone 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="65bc9-155">On the **Kintone Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="65bc9-157">a.</span><span class="sxs-lookup"><span data-stu-id="65bc9-157">a.</span></span> <span data-ttu-id="65bc9-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="65bc9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="65bc9-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="65bc9-159">b.</span></span> <span data-ttu-id="65bc9-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="65bc9-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="65bc9-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="65bc9-161">These values are not real.</span></span> <span data-ttu-id="65bc9-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="65bc9-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="65bc9-163">請連絡 [Kintone 用戶端支援小組](https://www.kintone.com/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="65bc9-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="65bc9-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="65bc9-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="65bc9-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc9-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="65bc9-168">在 [Kintone 組態] 區段上，按一下 [設定 Kintone] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="65bc9-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="65bc9-169">從 [快速參考] 區段中複製**登入 URL 和 SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="65bc9-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="65bc9-171">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 **Kintone** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="65bc9-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="65bc9-172">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="65bc9-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="65bc9-173">![設定](./media/active-directory-saas-kintone-tutorial/ic785879.png "設定")</span><span class="sxs-lookup"><span data-stu-id="65bc9-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="65bc9-174">按一下 [使用者與系統管理]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="65bc9-175">![使用者與系統管理](./media/active-directory-saas-kintone-tutorial/ic785880.png "使用者與系統管理")</span><span class="sxs-lookup"><span data-stu-id="65bc9-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="65bc9-176">在 [系統管理 \> 安全性] 底下，按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="65bc9-177">![登入](./media/active-directory-saas-kintone-tutorial/ic785881.png "登入")</span><span class="sxs-lookup"><span data-stu-id="65bc9-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="65bc9-178">按一下 [啟用 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="65bc9-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="65bc9-179">![SAML 驗證](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML 驗證")</span><span class="sxs-lookup"><span data-stu-id="65bc9-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="65bc9-180">在 [SAML 驗證] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="65bc9-180">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="65bc9-181">![SAML 驗證](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML 驗證")</span><span class="sxs-lookup"><span data-stu-id="65bc9-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="65bc9-182">a.</span><span class="sxs-lookup"><span data-stu-id="65bc9-182">a.</span></span> <span data-ttu-id="65bc9-183">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="65bc9-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="65bc9-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="65bc9-184">b.</span></span> <span data-ttu-id="65bc9-185">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="65bc9-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="65bc9-186">c.</span><span class="sxs-lookup"><span data-stu-id="65bc9-186">c.</span></span> <span data-ttu-id="65bc9-187">按一下 [瀏覽]  來上傳您下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="65bc9-187">Click **Browse** to upload your downloaded certificate.</span></span>
    
    <span data-ttu-id="65bc9-188">d.</span><span class="sxs-lookup"><span data-stu-id="65bc9-188">d.</span></span> <span data-ttu-id="65bc9-189">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="65bc9-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="65bc9-190">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="65bc9-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65bc9-191">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="65bc9-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65bc9-192">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65bc9-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="65bc9-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="65bc9-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="65bc9-194">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="65bc9-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="65bc9-196">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="65bc9-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65bc9-197">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="65bc9-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="65bc9-199">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="65bc9-201">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="65bc9-203">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="65bc9-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="65bc9-205">a.</span><span class="sxs-lookup"><span data-stu-id="65bc9-205">a.</span></span> <span data-ttu-id="65bc9-206">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="65bc9-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65bc9-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="65bc9-207">b.</span></span> <span data-ttu-id="65bc9-208">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="65bc9-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="65bc9-209">c.</span><span class="sxs-lookup"><span data-stu-id="65bc9-209">c.</span></span> <span data-ttu-id="65bc9-210">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="65bc9-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="65bc9-211">d.</span><span class="sxs-lookup"><span data-stu-id="65bc9-211">d.</span></span> <span data-ttu-id="65bc9-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="65bc9-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="65bc9-213">建立 Kintone 測試使用者</span><span class="sxs-lookup"><span data-stu-id="65bc9-213">Creating a Kintone test user</span></span>

<span data-ttu-id="65bc9-214">若要讓 Azure AD 使用者能夠登入 Kintone，必須將他們佈建到 Kintone。</span><span class="sxs-lookup"><span data-stu-id="65bc9-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="65bc9-215">Kintone 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="65bc9-215">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="65bc9-216">若要佈建使用者帳戶，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="65bc9-216">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="65bc9-217">以系統管理員身分登入您的 **Kintone** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="65bc9-217">Log in to your **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="65bc9-218">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="65bc9-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="65bc9-219">![設定](./media/active-directory-saas-kintone-tutorial/ic785879.png "設定")</span><span class="sxs-lookup"><span data-stu-id="65bc9-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="65bc9-220">按一下 [使用者與系統管理]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="65bc9-221">![使用者與系統管理](./media/active-directory-saas-kintone-tutorial/ic785880.png "使用者與系統管理")</span><span class="sxs-lookup"><span data-stu-id="65bc9-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="65bc9-222">在 [使用者管理] 底下，按一下 [部門與使用者]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="65bc9-223">![部門與使用者](./media/active-directory-saas-kintone-tutorial/ic785888.png "部門與使用者")</span><span class="sxs-lookup"><span data-stu-id="65bc9-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="65bc9-224">按一下 [新使用者] 。</span><span class="sxs-lookup"><span data-stu-id="65bc9-224">Click **New User**.</span></span>
   
    <span data-ttu-id="65bc9-225">![新使用者](./media/active-directory-saas-kintone-tutorial/ic785889.png "新使用者")</span><span class="sxs-lookup"><span data-stu-id="65bc9-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="65bc9-226">在 [新增使用者]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="65bc9-226">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="65bc9-227">![新使用者](./media/active-directory-saas-kintone-tutorial/ic785890.png "新使用者")</span><span class="sxs-lookup"><span data-stu-id="65bc9-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="65bc9-228">a.</span><span class="sxs-lookup"><span data-stu-id="65bc9-228">a.</span></span> <span data-ttu-id="65bc9-229">在相關文字方塊中輸入您想要佈建之有效 AAD 帳戶的 [顯示名稱]、[登入名稱]、[新密碼]、[確認密碼]、[電子郵件地址] 及其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="65bc9-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span></span>
 
    <span data-ttu-id="65bc9-230">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="65bc9-230">b.</span></span> <span data-ttu-id="65bc9-231">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="65bc9-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="65bc9-232">您可以使用任何其他的 Kintone 使用者帳戶建立工具或 Kintone 提供的 API，佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="65bc9-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="65bc9-233">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="65bc9-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="65bc9-234">在本節中，您會把 Kintone 的存取權授予，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="65bc9-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span></span>

![指派使用者][200] 

<span data-ttu-id="65bc9-236">**若要將 Britta Simon 指派給 Kintone，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="65bc9-236">**To assign Britta Simon to Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="65bc9-237">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="65bc9-239">在應用程式清單中，選取 [Kintone]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-239">In the applications list, select **Kintone**.</span></span>

    ![設定單一登入](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="65bc9-241">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-241">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="65bc9-243">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc9-243">Click **Add** button.</span></span> <span data-ttu-id="65bc9-244">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="65bc9-246">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="65bc9-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65bc9-247">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc9-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65bc9-248">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="65bc9-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="65bc9-249">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="65bc9-249">Testing single sign-on</span></span>

<span data-ttu-id="65bc9-250">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="65bc9-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65bc9-251">當您在「存取面板」中按一下 [Kintone] 圖格時，應該會自動登入您的 Kintone 應用程式。</span><span class="sxs-lookup"><span data-stu-id="65bc9-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="65bc9-252">其他資源</span><span class="sxs-lookup"><span data-stu-id="65bc9-252">Additional resources</span></span>

* [<span data-ttu-id="65bc9-253">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="65bc9-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="65bc9-254">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="65bc9-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

