---
title: "教學課程：Azure Active Directory 與 LockPath Keylight 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 LockPath Keylight 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e64a966f24411818abc4cc4ab29a428b5577d012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="d13ec-103">教學課程：Azure Active Directory 與 LockPath Keylight 整合</span><span class="sxs-lookup"><span data-stu-id="d13ec-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="d13ec-104">在本教學課程中，您會了解如何整合 LockPath Keylight 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d13ec-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d13ec-105">LockPath Keylight 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d13ec-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d13ec-106">您可以在 Azure AD 中管控可存取 LockPath Keylight 的人員</span><span class="sxs-lookup"><span data-stu-id="d13ec-106">You can control in Azure AD who has access to LockPath Keylight</span></span>
- <span data-ttu-id="d13ec-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 LockPath Keylight (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d13ec-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d13ec-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d13ec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d13ec-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d13ec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d13ec-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d13ec-110">Prerequisites</span></span>

<span data-ttu-id="d13ec-111">若要設定 Azure AD 與 LockPath Keylight 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d13ec-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span></span>

- <span data-ttu-id="d13ec-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d13ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d13ec-113">啟用 LockPath Keylight 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d13ec-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d13ec-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d13ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d13ec-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d13ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d13ec-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d13ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d13ec-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d13ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d13ec-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d13ec-118">Scenario description</span></span>
<span data-ttu-id="d13ec-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d13ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d13ec-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d13ec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d13ec-121">從資源庫新增 LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="d13ec-121">Adding LockPath Keylight from the gallery</span></span>
2. <span data-ttu-id="d13ec-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d13ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-the-gallery"></a><span data-ttu-id="d13ec-123">從資源庫新增 LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="d13ec-123">Adding LockPath Keylight from the gallery</span></span>
<span data-ttu-id="d13ec-124">若要設定將 LockPath Keylight 整合到 Azure AD 中，您需要從資源庫將 LockPath Keylight 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d13ec-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d13ec-125">**若要從資源庫新增 LockPath Keylight，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d13ec-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d13ec-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d13ec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d13ec-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d13ec-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d13ec-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d13ec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d13ec-133">在搜尋方塊中，輸入 **LockPath Keylight**。</span><span class="sxs-lookup"><span data-stu-id="d13ec-133">In the search box, type **LockPath Keylight**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="d13ec-135">在結果面板中，選取 [LockPath Keylight]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d13ec-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d13ec-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d13ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d13ec-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 LockPath Keylight 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d13ec-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d13ec-139">若要讓單一登入運作，Azure AD 必須知道 LockPath Keylight 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d13ec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span></span> <span data-ttu-id="d13ec-140">換句話說，必須在 Azure AD 使用者和 LockPath Keylight 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d13ec-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span></span>

<span data-ttu-id="d13ec-141">在 LockPath Keylight 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d13ec-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d13ec-142">若要設定及測試與 LockPath Keylight 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d13ec-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d13ec-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d13ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d13ec-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d13ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d13ec-145">**[建立 LockPath Keylight 測試使用者](#creating-a-lockpath-keylight-test-user)** - 使 LockPath Keylight 中對應的 Britta Simon 連結到該該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="d13ec-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d13ec-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d13ec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d13ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d13ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d13ec-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d13ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d13ec-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 LockPath Keylight 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d13ec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="d13ec-150">**若要設定與 LockPath Keylight 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d13ec-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="d13ec-151">在 Azure 入口網站的 [LockPath Keylight] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d13ec-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d13ec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="d13ec-155">在 [LockPath Keylight 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d13ec-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="d13ec-157">a.</span><span class="sxs-lookup"><span data-stu-id="d13ec-157">a.</span></span> <span data-ttu-id="d13ec-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="d13ec-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="d13ec-159">b.</span><span class="sxs-lookup"><span data-stu-id="d13ec-159">b.</span></span> <span data-ttu-id="d13ec-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="d13ec-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="d13ec-161">c.</span><span class="sxs-lookup"><span data-stu-id="d13ec-161">c.</span></span> <span data-ttu-id="d13ec-162">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<company name>.keylightgrc.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="d13ec-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="d13ec-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="d13ec-163">These values are not real.</span></span> <span data-ttu-id="d13ec-164">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="d13ec-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d13ec-165">請連絡 [LockPath Keylight 客戶支援小組](https://www.lockpath.com/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="d13ec-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span></span> 

4. <span data-ttu-id="d13ec-166">在 [SAML 簽署憑證] 區段上，按一下 [憑證]\(原始\)，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d13ec-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="d13ec-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d13ec-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="d13ec-170">在 [LockPath Keylight 組態] 區段上，按一下 [設定 LockPath Keylight] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d13ec-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d13ec-171">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="d13ec-173">若要在 LockPath Keylight 中啟用 SSO，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d13ec-173">To enable SSO in LockPath Keylight, perform the following steps:</span></span>
   
    <span data-ttu-id="d13ec-174">a.</span><span class="sxs-lookup"><span data-stu-id="d13ec-174">a.</span></span> <span data-ttu-id="d13ec-175">以系統管理員身分登入 LockPath Keylight 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d13ec-175">Sign-on to your LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="d13ec-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d13ec-176">b.</span></span> <span data-ttu-id="d13ec-177">在頂端功能表中，按一下 [人員]，然後選取 [Keylight 安裝]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="d13ec-179">c.</span><span class="sxs-lookup"><span data-stu-id="d13ec-179">c.</span></span> <span data-ttu-id="d13ec-180">在左側樹狀檢視中，按一下 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-180">In the treeview on the left, click **SAML**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="d13ec-182">d.</span><span class="sxs-lookup"><span data-stu-id="d13ec-182">d.</span></span> <span data-ttu-id="d13ec-183">在 [SAML 設定] 對話方塊中，按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-183">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="d13ec-185">在 [編輯 SAML 設定]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d13ec-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="d13ec-187">a.</span><span class="sxs-lookup"><span data-stu-id="d13ec-187">a.</span></span> <span data-ttu-id="d13ec-188">將 [SAML 驗證] 設為**作用中**。</span><span class="sxs-lookup"><span data-stu-id="d13ec-188">Set **SAML authentication** to **Active**.</span></span>

    <span data-ttu-id="d13ec-189">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d13ec-189">b.</span></span> <span data-ttu-id="d13ec-190">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值，貼到 [識別提供者登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d13ec-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="d13ec-191">c.</span><span class="sxs-lookup"><span data-stu-id="d13ec-191">c.</span></span> <span data-ttu-id="d13ec-192">將您從 Azure 入口網站複製的 [單一登出服務 URL] 值，貼到 [識別提供者登出 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d13ec-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="d13ec-193">d.</span><span class="sxs-lookup"><span data-stu-id="d13ec-193">d.</span></span> <span data-ttu-id="d13ec-194">按一下 [選擇檔案] 來選取下載的 LockPath Keylight 憑證，然後按一下 [開啟] 以上傳憑證。</span><span class="sxs-lookup"><span data-stu-id="d13ec-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="d13ec-195">e.</span><span class="sxs-lookup"><span data-stu-id="d13ec-195">e.</span></span> <span data-ttu-id="d13ec-196">將 [SAML 使用者識別碼位置] 設定為 [Subject 陳述式的 NameIdentifier 元素]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    
    <span data-ttu-id="d13ec-197">f.</span><span class="sxs-lookup"><span data-stu-id="d13ec-197">f.</span></span> <span data-ttu-id="d13ec-198">使用下列模式提供 [Keylight 服務提供者]︰**https://&lt;CompanyName&gt;.keylightgrc.com**。</span><span class="sxs-lookup"><span data-stu-id="d13ec-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="d13ec-199">g.</span><span class="sxs-lookup"><span data-stu-id="d13ec-199">g.</span></span> <span data-ttu-id="d13ec-200">將 [自動佈建使用者] 設定為 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-200">Set **Auto-provision users** to **Active**.</span></span>

    <span data-ttu-id="d13ec-201">h.</span><span class="sxs-lookup"><span data-stu-id="d13ec-201">h.</span></span> <span data-ttu-id="d13ec-202">將 [自動佈建帳戶類型] 設定為 [完整使用者]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-202">Set **Auto-provision account type** to **Full User**.</span></span>

    <span data-ttu-id="d13ec-203">i.</span><span class="sxs-lookup"><span data-stu-id="d13ec-203">i.</span></span> <span data-ttu-id="d13ec-204">設定 [自動佈建安全性角色]，選取 [具備 SAML 的標準使用者]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="d13ec-205">j.</span><span class="sxs-lookup"><span data-stu-id="d13ec-205">j.</span></span> <span data-ttu-id="d13ec-206">設定 [自動佈建安全性設定]，選取 [標準使用者設定]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="d13ec-207">k.</span><span class="sxs-lookup"><span data-stu-id="d13ec-207">k.</span></span> <span data-ttu-id="d13ec-208">在 [電子郵件屬性] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="d13ec-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="d13ec-209">l.</span><span class="sxs-lookup"><span data-stu-id="d13ec-209">l.</span></span> <span data-ttu-id="d13ec-210">在 [名字屬性] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`。</span><span class="sxs-lookup"><span data-stu-id="d13ec-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="d13ec-211">m.</span><span class="sxs-lookup"><span data-stu-id="d13ec-211">m.</span></span> <span data-ttu-id="d13ec-212">在 [姓氏屬性] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`。</span><span class="sxs-lookup"><span data-stu-id="d13ec-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="d13ec-213">n.</span><span class="sxs-lookup"><span data-stu-id="d13ec-213">n.</span></span> <span data-ttu-id="d13ec-214">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d13ec-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d13ec-215">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="d13ec-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d13ec-216">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d13ec-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d13ec-217">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d13ec-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d13ec-218">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d13ec-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="d13ec-219">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d13ec-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d13ec-221">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d13ec-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d13ec-222">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d13ec-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d13ec-224">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-224">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d13ec-226">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-226">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d13ec-228">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d13ec-228">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d13ec-230">a.</span><span class="sxs-lookup"><span data-stu-id="d13ec-230">a.</span></span> <span data-ttu-id="d13ec-231">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d13ec-231">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d13ec-232">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d13ec-232">b.</span></span> <span data-ttu-id="d13ec-233">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d13ec-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d13ec-234">c.</span><span class="sxs-lookup"><span data-stu-id="d13ec-234">c.</span></span> <span data-ttu-id="d13ec-235">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d13ec-235">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d13ec-236">d.</span><span class="sxs-lookup"><span data-stu-id="d13ec-236">d.</span></span> <span data-ttu-id="d13ec-237">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d13ec-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="d13ec-238">建立 LockPath Keylight 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d13ec-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="d13ec-239">在本節中，您要在 LockPath Keylight 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="d13ec-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="d13ec-240">LockPath Keylight 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="d13ec-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="d13ec-241">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="d13ec-241">There is no action item for you in this section.</span></span> <span data-ttu-id="d13ec-242">存取 LockPath Keylight 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="d13ec-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="d13ec-243">如果您需要手動建立使用者，則必須連絡 [LockPath Keylight 客戶支援小組](https://www.lockpath.com/contact/)。</span><span class="sxs-lookup"><span data-stu-id="d13ec-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d13ec-244">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d13ec-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d13ec-245">在本節中，您會將 LockPath Keylight 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d13ec-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span></span>

![指派使用者][200] 

<span data-ttu-id="d13ec-247">**若要將 Britta Simon 指派給 LockPath Keylight，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d13ec-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="d13ec-248">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d13ec-250">在應用程式清單中，選取 [LockPath Keylight]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-250">In the applications list, select **LockPath Keylight**.</span></span>

    ![設定單一登入](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="d13ec-252">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-252">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d13ec-254">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d13ec-254">Click **Add** button.</span></span> <span data-ttu-id="d13ec-255">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d13ec-257">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d13ec-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d13ec-258">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d13ec-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d13ec-259">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d13ec-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d13ec-260">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d13ec-260">Testing single sign-on</span></span>

<span data-ttu-id="d13ec-261">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="d13ec-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d13ec-262">當您在存取面板中按一下 LockPath Keylight 圖格時，應該會自動登入您的 LockPath Keylight 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d13ec-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d13ec-263">其他資源</span><span class="sxs-lookup"><span data-stu-id="d13ec-263">Additional resources</span></span>

* [<span data-ttu-id="d13ec-264">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d13ec-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d13ec-265">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d13ec-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

