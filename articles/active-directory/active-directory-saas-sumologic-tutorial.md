---
title: "教學課程：Azure Active Directory 與 SumoLogic 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SumoLogic 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e739106472ccf930b2942eb810dd844f2b1ade7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="84540-103">教學課程：Azure Active Directory 與 SumoLogic 整合</span><span class="sxs-lookup"><span data-stu-id="84540-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="84540-104">在本教學課程中，您會了解如何整合 SumoLogic 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="84540-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="84540-105">SumoLogic 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="84540-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="84540-106">您可以在 Azure AD 中管控可存取 SumoLogic 的人員</span><span class="sxs-lookup"><span data-stu-id="84540-106">You can control in Azure AD who has access to SumoLogic</span></span>
- <span data-ttu-id="84540-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SumoLogic (單一登入)</span><span class="sxs-lookup"><span data-stu-id="84540-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="84540-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="84540-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="84540-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="84540-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84540-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="84540-110">Prerequisites</span></span>

<span data-ttu-id="84540-111">若要設定 Azure AD 與 SumoLogic 的整合作業，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="84540-111">To configure Azure AD integration with SumoLogic, you need the following items:</span></span>

- <span data-ttu-id="84540-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84540-112">An Azure AD subscription</span></span>
- <span data-ttu-id="84540-113">已啟用 SumoLogic 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="84540-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="84540-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="84540-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="84540-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="84540-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="84540-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="84540-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="84540-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="84540-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="84540-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="84540-118">Scenario description</span></span>
<span data-ttu-id="84540-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84540-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="84540-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="84540-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="84540-121">從資源庫新增 SumoLogic</span><span class="sxs-lookup"><span data-stu-id="84540-121">Adding SumoLogic from the gallery</span></span>
2. <span data-ttu-id="84540-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84540-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-the-gallery"></a><span data-ttu-id="84540-123">從資源庫新增 SumoLogic</span><span class="sxs-lookup"><span data-stu-id="84540-123">Adding SumoLogic from the gallery</span></span>
<span data-ttu-id="84540-124">若要設定 SumoLogic 與 Azure AD 整合，您需要從資源庫將 SumoLogic 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="84540-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="84540-125">**若要從資源庫新增 SumoLogic，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84540-125">**To add SumoLogic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="84540-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="84540-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="84540-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84540-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="84540-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84540-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="84540-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84540-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="84540-133">在搜尋方塊中，輸入 **SumoLogic**。</span><span class="sxs-lookup"><span data-stu-id="84540-133">In the search box, type **SumoLogic**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="84540-135">在結果窗格中，選取 [SumoLogic]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="84540-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="84540-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84540-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="84540-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SumoLogic 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84540-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="84540-139">若要讓單一登入運作，Azure AD 必須知道 SumoLogic 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="84540-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span></span> <span data-ttu-id="84540-140">換句話說，必須在 Azure AD 使用者和 SumoLogic 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="84540-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span></span>

<span data-ttu-id="84540-141">在 SumoLogic 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="84540-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="84540-142">若要使用 SumoLogic 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="84540-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="84540-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="84540-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="84540-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84540-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="84540-145">**[建立 SumoLogic 測試使用者](#creating-a-sumologic-test-user)** - 使 SumoLogic 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="84540-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="84540-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84540-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="84540-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="84540-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="84540-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="84540-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="84540-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 SumoLogic 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="84540-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="84540-150">**若要使用 SumoLogic 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84540-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="84540-151">在 Azure 入口網站的 [SumoLogic] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="84540-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="84540-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="84540-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="84540-155">在 [SumoLogic 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84540-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="84540-157">a.</span><span class="sxs-lookup"><span data-stu-id="84540-157">a.</span></span> <span data-ttu-id="84540-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="84540-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="84540-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84540-159">b.</span></span> <span data-ttu-id="84540-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="84540-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="84540-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="84540-161">These values are not real.</span></span> <span data-ttu-id="84540-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="84540-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="84540-163">請連絡 [SumoLogic 客戶支援小組](https://www.sumologic.com/contact-us/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="84540-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="84540-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="84540-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="84540-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="84540-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="84540-168">在 [SumoLogic 組態] 區段上，按一下 [設定 SumoLogic] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="84540-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="84540-169">從 [快速參考] 區段中複製 [SAML 實體識別碼] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="84540-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="84540-171">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 SumoLogic 公司網站。</span><span class="sxs-lookup"><span data-stu-id="84540-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="84540-172">移至 [管理] \> [安全性]。</span><span class="sxs-lookup"><span data-stu-id="84540-172">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="84540-173">![管理](./media/active-directory-saas-sumologic-tutorial/ic778556.png "管理")</span><span class="sxs-lookup"><span data-stu-id="84540-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="84540-174">按一下 [SAML] 。</span><span class="sxs-lookup"><span data-stu-id="84540-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="84540-175">![全域安全性設定](./media/active-directory-saas-sumologic-tutorial/ic778557.png "全域安全性設定")</span><span class="sxs-lookup"><span data-stu-id="84540-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="84540-176">從 [選取組態或建立新的組態] 清單中選取 [Azure AD]，然後按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="84540-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="84540-177">![設定 SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "設定 SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="84540-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="84540-178">在 [設定 SAML 2.0]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84540-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="84540-179">![設定 SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "設定 SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="84540-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="84540-180">a.</span><span class="sxs-lookup"><span data-stu-id="84540-180">a.</span></span> <span data-ttu-id="84540-181">在 [組態名稱] 文字方塊中，輸入 **Azure AD**。</span><span class="sxs-lookup"><span data-stu-id="84540-181">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="84540-182">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84540-182">b.</span></span> <span data-ttu-id="84540-183">選取 [偵錯模式] 。</span><span class="sxs-lookup"><span data-stu-id="84540-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="84540-184">c.</span><span class="sxs-lookup"><span data-stu-id="84540-184">c.</span></span> <span data-ttu-id="84540-185">在 [簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="84540-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="84540-186">d.</span><span class="sxs-lookup"><span data-stu-id="84540-186">d.</span></span> <span data-ttu-id="84540-187">在 [驗證要求 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="84540-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="84540-188">e.</span><span class="sxs-lookup"><span data-stu-id="84540-188">e.</span></span> <span data-ttu-id="84540-189">在記事本中開啟您的 base-64 編碼的憑證，將它的內容複製到您的剪貼簿，然後將整個憑證貼到 [X.509 憑證]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="84540-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="84540-190">f.</span><span class="sxs-lookup"><span data-stu-id="84540-190">f.</span></span> <span data-ttu-id="84540-191">在 [電子郵件屬性] 選取 [使用 SAML 主體]。</span><span class="sxs-lookup"><span data-stu-id="84540-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="84540-192">g.</span><span class="sxs-lookup"><span data-stu-id="84540-192">g.</span></span> <span data-ttu-id="84540-193">選取 [服務提供者起始登入組態] 。</span><span class="sxs-lookup"><span data-stu-id="84540-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="84540-194">h.</span><span class="sxs-lookup"><span data-stu-id="84540-194">h.</span></span> <span data-ttu-id="84540-195">在 [登入路徑] 文字方塊中輸入 **Azure**，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="84540-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="84540-196">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="84540-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="84540-197">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="84540-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="84540-198">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="84540-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="84540-199">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84540-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="84540-200">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="84540-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="84540-202">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84540-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="84540-203">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="84540-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="84540-205">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="84540-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="84540-207">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="84540-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="84540-209">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84540-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="84540-211">a.</span><span class="sxs-lookup"><span data-stu-id="84540-211">a.</span></span> <span data-ttu-id="84540-212">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="84540-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="84540-213">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="84540-213">b.</span></span> <span data-ttu-id="84540-214">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="84540-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="84540-215">c.</span><span class="sxs-lookup"><span data-stu-id="84540-215">c.</span></span> <span data-ttu-id="84540-216">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="84540-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="84540-217">d.</span><span class="sxs-lookup"><span data-stu-id="84540-217">d.</span></span> <span data-ttu-id="84540-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="84540-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="84540-219">建立 SumoLogic 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84540-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="84540-220">若要讓 Azure AD 使用者能夠登入 SumoLogic，必須將他們佈建到 SumoLogic。</span><span class="sxs-lookup"><span data-stu-id="84540-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="84540-221">SumoLogic 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="84540-221">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="84540-222">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84540-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="84540-223">登入您的 **SumoLogic** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="84540-223">Log in to your **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="84540-224">移至 [管理] \> [使用者]。</span><span class="sxs-lookup"><span data-stu-id="84540-224">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="84540-225">![使用者](./media/active-directory-saas-sumologic-tutorial/ic778561.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="84540-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="84540-226">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="84540-226">Click **Add**.</span></span>
   
    <span data-ttu-id="84540-227">![使用者](./media/active-directory-saas-sumologic-tutorial/ic778562.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="84540-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="84540-228">在 [新增使用者]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="84540-228">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="84540-229">![新增使用者](./media/active-directory-saas-sumologic-tutorial/ic778563.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="84540-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="84540-230">a.</span><span class="sxs-lookup"><span data-stu-id="84540-230">a.</span></span> <span data-ttu-id="84540-231">在 [名字]、[姓氏] 和 [電子郵件] 文字方塊中，輸入您想要佈建之 Azure AD 帳戶的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="84540-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="84540-232">b.</span><span class="sxs-lookup"><span data-stu-id="84540-232">b.</span></span> <span data-ttu-id="84540-233">選取角色。</span><span class="sxs-lookup"><span data-stu-id="84540-233">Select a role.</span></span>
  
    <span data-ttu-id="84540-234">c.</span><span class="sxs-lookup"><span data-stu-id="84540-234">c.</span></span> <span data-ttu-id="84540-235">在 [狀態] 選取 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="84540-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="84540-236">d.</span><span class="sxs-lookup"><span data-stu-id="84540-236">d.</span></span> <span data-ttu-id="84540-237">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="84540-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="84540-238">您可以使用任何其他的 SumoLogic 使用者帳戶建立工具或 SumoLogic 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="84540-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="84540-239">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="84540-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="84540-240">在本節中，您會將 SumoLogic 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="84540-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span></span>

![指派使用者][200] 

<span data-ttu-id="84540-242">**若要將 Britta Simon 指派給 SumoLogic，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="84540-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="84540-243">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="84540-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="84540-245">在應用程式清單中，選取 [SumoLogic]。</span><span class="sxs-lookup"><span data-stu-id="84540-245">In the applications list, select **SumoLogic**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="84540-247">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="84540-247">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="84540-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84540-249">Click **Add** button.</span></span> <span data-ttu-id="84540-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="84540-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="84540-252">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="84540-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="84540-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84540-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="84540-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="84540-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="84540-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="84540-255">Testing single sign-on</span></span>

<span data-ttu-id="84540-256">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="84540-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="84540-257">當您在存取面板中按一下 [SumoLogic] 圖格時，應該會自動登入您的 SumoLogic 應用程式。</span><span class="sxs-lookup"><span data-stu-id="84540-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84540-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="84540-258">Additional resources</span></span>

* [<span data-ttu-id="84540-259">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="84540-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="84540-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="84540-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

