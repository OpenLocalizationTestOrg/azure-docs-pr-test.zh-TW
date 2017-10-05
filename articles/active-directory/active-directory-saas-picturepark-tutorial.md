---
title: "教學課程：Azure Active Directory 與 Picturepark 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Picturepark 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 1c009aa1fdd3140a4466cf762b6c9687e74ce4c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="d64b7-103">教學課程：Azure Active Directory 與 Picturepark 整合</span><span class="sxs-lookup"><span data-stu-id="d64b7-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="d64b7-104">在本教學課程中，您會了解如何整合 Picturepark 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d64b7-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d64b7-105">Picturepark 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d64b7-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d64b7-106">您可以在 Azure AD 中控制可存取 Picturepark 的人員</span><span class="sxs-lookup"><span data-stu-id="d64b7-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="d64b7-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Picturepark (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d64b7-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d64b7-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d64b7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d64b7-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d64b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d64b7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d64b7-110">Prerequisites</span></span>

<span data-ttu-id="d64b7-111">若要設定 Azure AD 與 Picturepark 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d64b7-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="d64b7-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d64b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d64b7-113">啟用 Picturepark 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d64b7-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d64b7-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d64b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d64b7-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d64b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d64b7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d64b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d64b7-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d64b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d64b7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d64b7-118">Scenario description</span></span>
<span data-ttu-id="d64b7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d64b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d64b7-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d64b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d64b7-121">從資源庫新增 Picturepark</span><span class="sxs-lookup"><span data-stu-id="d64b7-121">Adding Picturepark from the gallery</span></span>
2. <span data-ttu-id="d64b7-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d64b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="d64b7-123">從資源庫新增 Picturepark</span><span class="sxs-lookup"><span data-stu-id="d64b7-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="d64b7-124">若要設定將 Picturepark 整合到 Azure AD 中，您需要從資源庫將 Picturepark 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d64b7-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d64b7-125">**若要從資源庫新增 Picturepark，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d64b7-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d64b7-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d64b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d64b7-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d64b7-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d64b7-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d64b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d64b7-133">在搜尋方塊中，輸入 **Picturepark**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-133">In the search box, type **Picturepark**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="d64b7-135">在結果面板中，選取 [Picturepark]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d64b7-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d64b7-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d64b7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d64b7-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Picturepark 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d64b7-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d64b7-139">若要讓單一登入運作，Azure AD 必須知道 Picturepark 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d64b7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="d64b7-140">換句話說，必須在 Azure AD 使用者和 Picturepark 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d64b7-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="d64b7-141">在 Picturepark 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d64b7-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d64b7-142">若要設定及測試與 Picturepark 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d64b7-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d64b7-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d64b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d64b7-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d64b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d64b7-145">**[建立 Picturepark 測試使用者](#creating-a-picturepark-test-user)** - 使 Picturepark 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="d64b7-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d64b7-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d64b7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d64b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d64b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d64b7-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d64b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d64b7-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Picturepark 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d64b7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="d64b7-150">**若要設定與 Picturepark 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d64b7-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="d64b7-151">在 Azure 入口網站的 [Picturepark] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d64b7-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d64b7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="d64b7-155">在 [Picturepark 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d64b7-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="d64b7-157">a.</span><span class="sxs-lookup"><span data-stu-id="d64b7-157">a.</span></span> <span data-ttu-id="d64b7-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="d64b7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="d64b7-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d64b7-159">b.</span></span> <span data-ttu-id="d64b7-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="d64b7-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="d64b7-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="d64b7-161">These values are not real.</span></span> <span data-ttu-id="d64b7-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="d64b7-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d64b7-163">請連絡 [Picturepark 客戶支援小組](https://picturepark.com/about/contact/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="d64b7-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="d64b7-164">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="d64b7-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="d64b7-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d64b7-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d64b7-168">在 [Picturepark 組態] 區段上，按一下 [設定 Picturepark] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d64b7-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d64b7-169">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="d64b7-171">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Picturepark 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d64b7-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="d64b7-172">在最上面的工具列中，按一下 [系統管理工具]，然後按一下 [管理主控台]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="d64b7-173">![管理主控台](./media/active-directory-saas-picturepark-tutorial/ic795062.png "管理主控台")</span><span class="sxs-lookup"><span data-stu-id="d64b7-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="d64b7-174">按一下 [驗證]，然後按一下 [識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="d64b7-175">![驗證](./media/active-directory-saas-picturepark-tutorial/ic795063.png "驗證")</span><span class="sxs-lookup"><span data-stu-id="d64b7-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="d64b7-176">在 [識別提供者組態]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d64b7-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d64b7-177">![識別提供者組態](./media/active-directory-saas-picturepark-tutorial/ic795064.png "識別提供者組態")</span><span class="sxs-lookup"><span data-stu-id="d64b7-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="d64b7-178">a.</span><span class="sxs-lookup"><span data-stu-id="d64b7-178">a.</span></span> <span data-ttu-id="d64b7-179">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="d64b7-179">Click **Add**.</span></span>
  
    <span data-ttu-id="d64b7-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d64b7-180">b.</span></span> <span data-ttu-id="d64b7-181">輸入組態的名稱。</span><span class="sxs-lookup"><span data-stu-id="d64b7-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="d64b7-182">c.</span><span class="sxs-lookup"><span data-stu-id="d64b7-182">c.</span></span> <span data-ttu-id="d64b7-183">選取 [設定為預設值] 。</span><span class="sxs-lookup"><span data-stu-id="d64b7-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="d64b7-184">d.</span><span class="sxs-lookup"><span data-stu-id="d64b7-184">d.</span></span> <span data-ttu-id="d64b7-185">在 [簽發者 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="d64b7-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="d64b7-186">e.</span><span class="sxs-lookup"><span data-stu-id="d64b7-186">e.</span></span> <span data-ttu-id="d64b7-187">在 [信任的簽發者指紋] 文字方塊中，貼上您從 [SAML 簽署憑證] 區段複製的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="d64b7-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="d64b7-188">按一下 [JoinDefaultUsersGroup] 。</span><span class="sxs-lookup"><span data-stu-id="d64b7-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="d64b7-189">若要在 [宣告] 文字方塊中設定 [Emailaddress] 屬性，請輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="d64b7-190">![組態](./media/active-directory-saas-picturepark-tutorial/ic795065.png "組態")</span><span class="sxs-lookup"><span data-stu-id="d64b7-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="d64b7-191">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="d64b7-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d64b7-192">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d64b7-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d64b7-193">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d64b7-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d64b7-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d64b7-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="d64b7-195">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d64b7-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d64b7-197">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d64b7-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d64b7-198">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d64b7-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d64b7-200">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d64b7-202">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d64b7-204">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d64b7-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d64b7-206">a.</span><span class="sxs-lookup"><span data-stu-id="d64b7-206">a.</span></span> <span data-ttu-id="d64b7-207">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d64b7-208">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d64b7-208">b.</span></span> <span data-ttu-id="d64b7-209">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d64b7-210">c.</span><span class="sxs-lookup"><span data-stu-id="d64b7-210">c.</span></span> <span data-ttu-id="d64b7-211">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d64b7-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d64b7-212">d.</span><span class="sxs-lookup"><span data-stu-id="d64b7-212">d.</span></span> <span data-ttu-id="d64b7-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d64b7-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="d64b7-214">建立 Picturepark 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d64b7-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="d64b7-215">若要讓 Azure AD 使用者能夠登入 Picturepark，必須將他們佈建到 Mindflash。</span><span class="sxs-lookup"><span data-stu-id="d64b7-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="d64b7-216">Picturepark 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="d64b7-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="d64b7-217">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d64b7-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d64b7-218">登入您的 **Picturepark** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="d64b7-218">Log in to your **Picturepark** tenant.</span></span>

2. <span data-ttu-id="d64b7-219">在最上面的工具列中，按一下 [系統管理工具]，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="d64b7-220">![使用者](./media/active-directory-saas-picturepark-tutorial/ic795067.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="d64b7-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="d64b7-221">在 [使用者總覽] 索引標籤中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="d64b7-222">![使用者管理](./media/active-directory-saas-picturepark-tutorial/ic795068.png "使用者管理")</span><span class="sxs-lookup"><span data-stu-id="d64b7-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="d64b7-223">在 [建立使用者] 對話方塊中，針對您想要佈建的有效 Azure Active Directory 使用者，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d64b7-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="d64b7-224">![建立使用者](./media/active-directory-saas-picturepark-tutorial/ic795069.png "建立使用者")</span><span class="sxs-lookup"><span data-stu-id="d64b7-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="d64b7-225">a.</span><span class="sxs-lookup"><span data-stu-id="d64b7-225">a.</span></span> <span data-ttu-id="d64b7-226">在 [電子郵件地址] 文字方塊中，輸入使用者的**電子郵件地址**：**BrittaSimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="d64b7-227">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d64b7-227">b.</span></span> <span data-ttu-id="d64b7-228">在 [密碼] 和 [確認密碼] 文字方塊中，輸入 BrittaSimon 的**密碼**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="d64b7-229">c.</span><span class="sxs-lookup"><span data-stu-id="d64b7-229">c.</span></span> <span data-ttu-id="d64b7-230">在 [名字] 文字方塊中，輸入使用者的**名字**：**Britta**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="d64b7-231">d.</span><span class="sxs-lookup"><span data-stu-id="d64b7-231">d.</span></span> <span data-ttu-id="d64b7-232">在 [姓氏] 文字方塊中，輸入使用者的**姓氏**：**Simon**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="d64b7-233">e.</span><span class="sxs-lookup"><span data-stu-id="d64b7-233">e.</span></span> <span data-ttu-id="d64b7-234">在 [公司] 文字方塊中，輸入使用者的**公司名稱**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="d64b7-235">f.</span><span class="sxs-lookup"><span data-stu-id="d64b7-235">f.</span></span> <span data-ttu-id="d64b7-236">在 [國家/地區] 文字方塊中，選取使用者的**國家/地區**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="d64b7-237">g.</span><span class="sxs-lookup"><span data-stu-id="d64b7-237">g.</span></span> <span data-ttu-id="d64b7-238">在 [ZIP] 文字方塊中，輸入縣/市的**郵遞區號**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="d64b7-239">h.</span><span class="sxs-lookup"><span data-stu-id="d64b7-239">h.</span></span> <span data-ttu-id="d64b7-240">在 [縣/市] 文字方塊中，輸入使用者的**縣/市名稱**。</span><span class="sxs-lookup"><span data-stu-id="d64b7-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="d64b7-241">i.</span><span class="sxs-lookup"><span data-stu-id="d64b7-241">i.</span></span> <span data-ttu-id="d64b7-242">選取 [語言] 。</span><span class="sxs-lookup"><span data-stu-id="d64b7-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="d64b7-243">j.</span><span class="sxs-lookup"><span data-stu-id="d64b7-243">j.</span></span> <span data-ttu-id="d64b7-244">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d64b7-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="d64b7-245">您可以使用任何其他的 Picturepark 使用者帳戶建立工具，或 Picturepark 提供的 API，以佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="d64b7-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d64b7-246">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d64b7-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d64b7-247">在本節中，您會將 Picturepark 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d64b7-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![指派使用者][200] 

<span data-ttu-id="d64b7-249">**若要將 Britta Simon 指派給 Picturepark，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d64b7-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="d64b7-250">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d64b7-252">在應用程式清單中，選取 [Picturepark]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-252">In the applications list, select **Picturepark**.</span></span>

    ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="d64b7-254">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-254">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d64b7-256">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d64b7-256">Click **Add** button.</span></span> <span data-ttu-id="d64b7-257">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d64b7-259">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d64b7-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d64b7-260">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d64b7-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d64b7-261">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d64b7-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d64b7-262">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d64b7-262">Testing single sign-on</span></span>

<span data-ttu-id="d64b7-263">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="d64b7-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d64b7-264">當您在存取面板中按一下 Picturepark 圖格時，應該會自動登入您的 Picturepark 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d64b7-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="d64b7-265">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d64b7-265">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d64b7-266">其他資源</span><span class="sxs-lookup"><span data-stu-id="d64b7-266">Additional resources</span></span>

* [<span data-ttu-id="d64b7-267">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d64b7-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d64b7-268">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d64b7-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

