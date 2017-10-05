---
title: "教學課程：Azure Active Directory 與 Workday 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Workday 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 164d5c644f120fa86e2b690649241892764b64b7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="b866f-103">教學課程：Azure Active Directory 與 Workday 整合</span><span class="sxs-lookup"><span data-stu-id="b866f-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="b866f-104">在本教學課程中，您將了解如何整合 Workday 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b866f-104">In this tutorial, you learn how to integrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b866f-105">Workday 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="b866f-105">Integrating Workday with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b866f-106">您可以在 Azure AD 中控制可存取 Workday 的人員</span><span class="sxs-lookup"><span data-stu-id="b866f-106">You can control in Azure AD who has access to Workday</span></span>
- <span data-ttu-id="b866f-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Workday (單一登入)</span><span class="sxs-lookup"><span data-stu-id="b866f-107">You can enable your users to automatically get signed-on to Workday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b866f-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="b866f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b866f-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b866f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b866f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b866f-110">Prerequisites</span></span>

<span data-ttu-id="b866f-111">若要設定 Azure AD 與 Workday 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="b866f-111">To configure Azure AD integration with Workday, you need the following items:</span></span>

- <span data-ttu-id="b866f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b866f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b866f-113">已啟用 Workday 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b866f-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b866f-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b866f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b866f-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b866f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b866f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b866f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b866f-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="b866f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b866f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b866f-118">Scenario description</span></span>
<span data-ttu-id="b866f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b866f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b866f-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="b866f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b866f-121">從資源庫新增 Workday</span><span class="sxs-lookup"><span data-stu-id="b866f-121">Adding Workday from the gallery</span></span>
2. <span data-ttu-id="b866f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b866f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-the-gallery"></a><span data-ttu-id="b866f-123">從資源庫新增 Workday</span><span class="sxs-lookup"><span data-stu-id="b866f-123">Adding Workday from the gallery</span></span>
<span data-ttu-id="b866f-124">若要設定將 Workday 整合到 Azure AD 中，您需要從資源庫將 Workday 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="b866f-124">To configure the integration of Workday into Azure AD, you need to add Workday from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b866f-125">**若要從資源庫新增 Workday，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b866f-125">**To add Workday from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b866f-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b866f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b866f-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b866f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b866f-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b866f-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b866f-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b866f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b866f-133">在搜尋方塊中，輸入 **Workday**。</span><span class="sxs-lookup"><span data-stu-id="b866f-133">In the search box, type **Workday**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="b866f-135">在結果窗格中，選取 [Workday]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b866f-135">In the results panel, select **Workday**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b866f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b866f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b866f-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Workday 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b866f-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b866f-139">若要讓單一登入運作，Azure AD 必須知道 Workday 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="b866f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workday is to a user in Azure AD.</span></span> <span data-ttu-id="b866f-140">換句話說，必須在 Azure AD 使用者和 Workday 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b866f-140">In other words, a link relationship between an Azure AD user and the related user in Workday needs to be established.</span></span>

<span data-ttu-id="b866f-141">建立此連結關聯性的方法，就是指派 Azure AD 中**使用者名稱**的值作為 Workday 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="b866f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Workday.</span></span>

<span data-ttu-id="b866f-142">若要使用 Workday 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="b866f-142">To configure and test Azure AD single sign-on with Workday, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b866f-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b866f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b866f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b866f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b866f-145">**[建立 Workday 測試使用者](#creating-a-workday-test-user)** - 使 Workday 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="b866f-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - to have a counterpart of Britta Simon in Workday that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b866f-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b866f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b866f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="b866f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b866f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b866f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b866f-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Workday 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b866f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="b866f-150">**若要使用 Workday 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b866f-150">**To configure Azure AD single sign-on with Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="b866f-151">在 Azure 入口網站的 [Workday] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b866f-151">In the Azure portal, on the **Workday** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b866f-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b866f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="b866f-155">在 [Workday 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b866f-155">On the **Workday Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="b866f-157">a.</span><span class="sxs-lookup"><span data-stu-id="b866f-157">a.</span></span> <span data-ttu-id="b866f-158">在 [登入 URL] 文字方塊中，輸入下列值：`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="b866f-158">In the **Sign-on URL** textbox, type the value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="b866f-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b866f-159">b.</span></span> <span data-ttu-id="b866f-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="b866f-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b866f-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="b866f-161">These values are not the real.</span></span> <span data-ttu-id="b866f-162">請使用實際的「登入 URL」及「回覆 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="b866f-162">Update these values with the actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="b866f-163">您的回覆 URL 必須有子網域 (例如：www、wd2、wd3、wd3-impl、wd5、wd5-impl)。</span><span class="sxs-lookup"><span data-stu-id="b866f-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="b866f-164">例如，使用 " *http://www.myworkday.com* " 有效，但 " *http://myworkday.com* " 則無效。</span><span class="sxs-lookup"><span data-stu-id="b866f-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="b866f-165">請連絡 [Workday 客戶支援小組](https://www.workday.com/en-us/partners-services/services/support.html)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="b866f-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get these values.</span></span> 
 

4. <span data-ttu-id="b866f-166">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b866f-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="b866f-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b866f-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b866f-170">在 [Workday 組態] 區段上，按一下 [設定 Workday] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="b866f-170">On the **Workday Configuration** section, click **Configure Workday** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b866f-171">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="b866f-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="b866f-172">![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="b866f-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="b866f-173">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Workday 公司網站。</span><span class="sxs-lookup"><span data-stu-id="b866f-173">In a different web browser window, log in to your Workday company site as an administrator.</span></span>

8. <span data-ttu-id="b866f-174">移至 [功能表] \> [Workbench]。</span><span class="sxs-lookup"><span data-stu-id="b866f-174">Go to **Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="b866f-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="b866f-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="b866f-176">移至 [帳戶管理] 。</span><span class="sxs-lookup"><span data-stu-id="b866f-176">Go to **Account Administration**.</span></span>
   
    <span data-ttu-id="b866f-177">![帳戶管理](./media/active-directory-saas-workday-tutorial/IC782924.png "帳戶管理")</span><span class="sxs-lookup"><span data-stu-id="b866f-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="b866f-178">移至 [編輯租用戶設定 – 安全性] 。</span><span class="sxs-lookup"><span data-stu-id="b866f-178">Go to **Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="b866f-179">![編輯租用戶安全性](./media/active-directory-saas-workday-tutorial/IC782925.png "編輯租用戶安全性")</span><span class="sxs-lookup"><span data-stu-id="b866f-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="b866f-180">在 [重新導向 URL]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b866f-180">In the **Redirection URLs** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b866f-181">![重新導向 URL](./media/active-directory-saas-workday-tutorial/IC7829581.png "重新導向 URL")</span><span class="sxs-lookup"><span data-stu-id="b866f-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="b866f-182">a.</span><span class="sxs-lookup"><span data-stu-id="b866f-182">a.</span></span> <span data-ttu-id="b866f-183">按一下 [加入資料列]。</span><span class="sxs-lookup"><span data-stu-id="b866f-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="b866f-184">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b866f-184">b.</span></span> <span data-ttu-id="b866f-185">在 [登入重新導向 URL] 文字方塊和 [行動裝置重新導向 URL] 文字方塊中，輸入您在 Azure 入口網站的 [Workday 網域與 URL] 區段上輸入的 [登入 URL]。</span><span class="sxs-lookup"><span data-stu-id="b866f-185">In the **Login Redirect URL** textbox and the **Mobile Redirect URL** textbox, type the **Sign-on URL** you have entered on the **Workday Domain and URLs** section of the Azure portal.</span></span>
   
    <span data-ttu-id="b866f-186">c.</span><span class="sxs-lookup"><span data-stu-id="b866f-186">c.</span></span> <span data-ttu-id="b866f-187">在 Azure 入口網站的 [設定登入] 視窗上，複製 [登出 URL]，然後將它貼至 [登出重新導向 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="b866f-187">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL**, and then paste it into the **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="b866f-188">d.</span><span class="sxs-lookup"><span data-stu-id="b866f-188">d.</span></span>  <span data-ttu-id="b866f-189">在 [環境] 文字方塊中輸入環境名稱。</span><span class="sxs-lookup"><span data-stu-id="b866f-189">In **Environment** textbox, type the environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="b866f-190">[環境] 屬性的值會繫結至租用戶 URL 的值：</span><span class="sxs-lookup"><span data-stu-id="b866f-190">The value of the Environment attribute is tied to the value of the tenant URL:</span></span>  
    ><span data-ttu-id="b866f-191">-如果 Workday 租用戶 URL 的網域名稱開頭為 impl (例如：*https://impl.workday.com/\<tenant\>/login-saml2.htmld*)，則 [環境] 屬性必須設為 [實作]。</span><span class="sxs-lookup"><span data-stu-id="b866f-191">-If the domain name of the Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), the **Environment** attribute must be set to Implementation.</span></span>  
    ><span data-ttu-id="b866f-192">-如果網域名稱的開頭是其他字元，您需要連絡 [Workday 客戶支援小組](https://www.workday.com/en-us/partners-services/services/support.html)以取得相符的 [環境] 值。</span><span class="sxs-lookup"><span data-stu-id="b866f-192">-If the domain name starts with something else, you need to contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) to get the matching **Environment** value.</span></span>

12. <span data-ttu-id="b866f-193">在 [SAML 設定]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b866f-193">In the **SAML Setup** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b866f-194">![SAML 設定](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="b866f-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="b866f-195">a.</span><span class="sxs-lookup"><span data-stu-id="b866f-195">a.</span></span>  <span data-ttu-id="b866f-196">按一下 [啟用 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="b866f-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="b866f-197">b.</span><span class="sxs-lookup"><span data-stu-id="b866f-197">b.</span></span>  <span data-ttu-id="b866f-198">按一下 [加入資料列]。</span><span class="sxs-lookup"><span data-stu-id="b866f-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="b866f-199">在 [SAML 身分識別提供者] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b866f-199">In the SAML Identity Providers section, perform the following steps:</span></span>
   
    <span data-ttu-id="b866f-200">![SAML 身分識別提供者](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML 身分識別提供者")</span><span class="sxs-lookup"><span data-stu-id="b866f-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="b866f-201">a.</span><span class="sxs-lookup"><span data-stu-id="b866f-201">a.</span></span> <span data-ttu-id="b866f-202">在 [身分識別提供者名稱] 文字方塊中，輸入提供者名稱 (例如：SPInitiatedSSO)。</span><span class="sxs-lookup"><span data-stu-id="b866f-202">In the Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="b866f-203">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b866f-203">b.</span></span> <span data-ttu-id="b866f-204">在 Azure 入口網站的 [設定登入] 視窗上，複製 [SAML 實體識別碼] 值，然後將它貼至 [簽發者] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="b866f-204">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Entity ID** value, and then paste it into the **Issuer** textbox.</span></span>
   
    <span data-ttu-id="b866f-205">c.</span><span class="sxs-lookup"><span data-stu-id="b866f-205">c.</span></span> <span data-ttu-id="b866f-206">選取 [啟用 Workday 啟始的登出]。</span><span class="sxs-lookup"><span data-stu-id="b866f-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="b866f-207">d.</span><span class="sxs-lookup"><span data-stu-id="b866f-207">d.</span></span> <span data-ttu-id="b866f-208">在 Azure 入口網站的 [設定登入] 視窗上，複製 [登出 URL] 值，然後將它貼至 [登出要求 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="b866f-208">In the Azure portal, on the **Configure sign-on** window, copy the **Sign-Out URL** value, and then paste it into the **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="b866f-209">e.</span><span class="sxs-lookup"><span data-stu-id="b866f-209">e.</span></span> <span data-ttu-id="b866f-210">按一下 [識別提供者公開金鑰憑證]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="b866f-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="b866f-211">![建立](./media/active-directory-saas-workday-tutorial/IC782928.png "建立")</span><span class="sxs-lookup"><span data-stu-id="b866f-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="b866f-212">f.</span><span class="sxs-lookup"><span data-stu-id="b866f-212">f.</span></span> <span data-ttu-id="b866f-213">按一下 [建立 x509 公開金鑰]。</span><span class="sxs-lookup"><span data-stu-id="b866f-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="b866f-214">![建立](./media/active-directory-saas-workday-tutorial/IC782929.png "建立")</span><span class="sxs-lookup"><span data-stu-id="b866f-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="b866f-215">在 [檢視 x509 公開金鑰]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b866f-215">In the **View x509 Public Key** section, perform the following steps:</span></span> 
   
    <span data-ttu-id="b866f-216">![檢視 x509 公開金鑰](./media/active-directory-saas-workday-tutorial/IC782930.png "檢視 x509 公開金鑰")</span><span class="sxs-lookup"><span data-stu-id="b866f-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="b866f-217">a.</span><span class="sxs-lookup"><span data-stu-id="b866f-217">a.</span></span> <span data-ttu-id="b866f-218">在 [名稱] 文字方塊中，輸入您的憑證名稱 (例如：PPE\_SP)。</span><span class="sxs-lookup"><span data-stu-id="b866f-218">In the **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="b866f-219">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b866f-219">b.</span></span> <span data-ttu-id="b866f-220">在 [有效開始日期] 文字方塊中輸入憑證屬性值的有效開始日期。</span><span class="sxs-lookup"><span data-stu-id="b866f-220">In the **Valid From** textbox, type the valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="b866f-221">c.</span><span class="sxs-lookup"><span data-stu-id="b866f-221">c.</span></span>  <span data-ttu-id="b866f-222">在 [有效結束日期] 文字方塊中輸入憑證屬性值的有效結束日期。</span><span class="sxs-lookup"><span data-stu-id="b866f-222">In the **Valid To** textbox, type the valid to attribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="b866f-223">按兩下所下載的憑證，即可取得有效開始日期和有效結束日期。</span><span class="sxs-lookup"><span data-stu-id="b866f-223">You can get the valid from date and the valid to date from the downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="b866f-224">這些日期會列在 [詳細資料]  索引標籤之下。</span><span class="sxs-lookup"><span data-stu-id="b866f-224">The dates are listed under the **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="b866f-225">d.</span><span class="sxs-lookup"><span data-stu-id="b866f-225">d.</span></span>  <span data-ttu-id="b866f-226">在記事本中開啟 base-64 編碼的憑證，然後複製其內容。</span><span class="sxs-lookup"><span data-stu-id="b866f-226">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   
    <span data-ttu-id="b866f-227">e.</span><span class="sxs-lookup"><span data-stu-id="b866f-227">e.</span></span>  <span data-ttu-id="b866f-228">在 [憑證] 文字方塊中貼上剪貼簿的內容。</span><span class="sxs-lookup"><span data-stu-id="b866f-228">In the **Certificate** textbox, paste the content of your clipboard.</span></span>
   
    <span data-ttu-id="b866f-229">f.</span><span class="sxs-lookup"><span data-stu-id="b866f-229">f.</span></span>  <span data-ttu-id="b866f-230">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b866f-230">Click **OK**.</span></span>

15. <span data-ttu-id="b866f-231">執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b866f-231">Perform the following steps:</span></span> 
   
    <span data-ttu-id="b866f-232">![SSO 組態](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO 組態")</span><span class="sxs-lookup"><span data-stu-id="b866f-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="b866f-233">a.</span><span class="sxs-lookup"><span data-stu-id="b866f-233">a.</span></span>  <span data-ttu-id="b866f-234">啟用 [x509 私密金鑰組]。</span><span class="sxs-lookup"><span data-stu-id="b866f-234">Enable the **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="b866f-235">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b866f-235">b.</span></span>  <span data-ttu-id="b866f-236">在 [服務提供者識別碼] 文字方塊中，輸入 **http://www.workday.com**。</span><span class="sxs-lookup"><span data-stu-id="b866f-236">In the **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="b866f-237">c.</span><span class="sxs-lookup"><span data-stu-id="b866f-237">c.</span></span>  <span data-ttu-id="b866f-238">選取 [啟用 SP 啟始的 SAML 驗證]。</span><span class="sxs-lookup"><span data-stu-id="b866f-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="b866f-239">d.</span><span class="sxs-lookup"><span data-stu-id="b866f-239">d.</span></span>  <span data-ttu-id="b866f-240">在 Azure 入口網站的 [設定登入] 視窗上，複製 [SAML 單一登入服務 URL] 值，然後將它貼至 [IdP SSO 服務 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="b866f-240">In the Azure portal, on the **Configure sign-on** window, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="b866f-241">e.</span><span class="sxs-lookup"><span data-stu-id="b866f-241">e.</span></span> <span data-ttu-id="b866f-242">選取 [不要壓縮 SP 起始的驗證要求]。</span><span class="sxs-lookup"><span data-stu-id="b866f-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="b866f-243">f.</span><span class="sxs-lookup"><span data-stu-id="b866f-243">f.</span></span> <span data-ttu-id="b866f-244">選取 **SHA256** 做為 [驗證要求簽章方法]。</span><span class="sxs-lookup"><span data-stu-id="b866f-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="b866f-245">![驗證要求簽章方法](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "驗證要求簽章方法")</span><span class="sxs-lookup"><span data-stu-id="b866f-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="b866f-246">g.</span><span class="sxs-lookup"><span data-stu-id="b866f-246">g.</span></span> <span data-ttu-id="b866f-247">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b866f-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="b866f-248">![確定](./media/active-directory-saas-workday-tutorial/IC782933.png "確定")
<CE></span><span class="sxs-lookup"><span data-stu-id="b866f-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="b866f-249">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="b866f-249">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b866f-250">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="b866f-250">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b866f-251">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b866f-251">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b866f-252">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b866f-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="b866f-253">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b866f-253">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b866f-255">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b866f-255">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b866f-256">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b866f-256">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b866f-258">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b866f-258">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b866f-260">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b866f-260">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b866f-262">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b866f-262">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b866f-264">a.</span><span class="sxs-lookup"><span data-stu-id="b866f-264">a.</span></span> <span data-ttu-id="b866f-265">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b866f-265">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b866f-266">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b866f-266">b.</span></span> <span data-ttu-id="b866f-267">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="b866f-267">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b866f-268">c.</span><span class="sxs-lookup"><span data-stu-id="b866f-268">c.</span></span> <span data-ttu-id="b866f-269">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="b866f-269">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b866f-270">d.</span><span class="sxs-lookup"><span data-stu-id="b866f-270">d.</span></span> <span data-ttu-id="b866f-271">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b866f-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="b866f-272">建立 Workday 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b866f-272">Creating a Workday test user</span></span>

<span data-ttu-id="b866f-273">若要讓測試使用者佈建到 Workday 中，您需要連絡 [Workday 客戶支援小組](https://www.workday.com/en-us/partners-services/services/support.html)。</span><span class="sxs-lookup"><span data-stu-id="b866f-273">To get a test user provisioned into Workday, you need to contact the [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="b866f-274">[Workday 客戶支援小組](https://www.workday.com/en-us/partners-services/services/support.html)會為您建立此使用者。</span><span class="sxs-lookup"><span data-stu-id="b866f-274">The [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates the user for you.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b866f-275">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b866f-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b866f-276">在本節中，您會將 Workday 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b866f-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workday.</span></span>

![指派使用者][200] 

<span data-ttu-id="b866f-278">**若要將 Britta Simon 指派給 Workday，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b866f-278">**To assign Britta Simon to Workday, perform the following steps:**</span></span>

1. <span data-ttu-id="b866f-279">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b866f-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b866f-281">在應用程式清單中，選取 [Workday]。</span><span class="sxs-lookup"><span data-stu-id="b866f-281">In the applications list, select **Workday**.</span></span>

    ![設定單一登入](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="b866f-283">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b866f-283">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b866f-285">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b866f-285">Click **Add** button.</span></span> <span data-ttu-id="b866f-286">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b866f-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b866f-288">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="b866f-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b866f-289">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b866f-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b866f-290">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b866f-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b866f-291">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b866f-291">Testing single sign-on</span></span>

<span data-ttu-id="b866f-292">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="b866f-292">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b866f-293">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b866f-293">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b866f-294">其他資源</span><span class="sxs-lookup"><span data-stu-id="b866f-294">Additional resources</span></span>

* [<span data-ttu-id="b866f-295">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b866f-295">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b866f-296">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b866f-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b866f-297">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="b866f-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

