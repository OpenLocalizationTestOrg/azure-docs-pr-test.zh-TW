---
title: "教學課程：Azure Active Directory 與 TalentLMS 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 TalentLMS 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="fa2b8-103">教學課程：Azure Active Directory 與 TalentLMS 整合</span><span class="sxs-lookup"><span data-stu-id="fa2b8-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="fa2b8-104">在本教學課程中，您將了解如何整合 TalentLMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fa2b8-105">TalentLMS 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fa2b8-106">您可以在 Azure AD 中控制可存取 TalentLMS 的人員</span><span class="sxs-lookup"><span data-stu-id="fa2b8-106">You can control in Azure AD who has access to TalentLMS</span></span>
- <span data-ttu-id="fa2b8-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 TalentLMS (單一登入)</span><span class="sxs-lookup"><span data-stu-id="fa2b8-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fa2b8-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="fa2b8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fa2b8-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa2b8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="fa2b8-110">Prerequisites</span></span>

<span data-ttu-id="fa2b8-111">如要設定 Azure AD 與 TalentLMS 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-111">To configure Azure AD integration with TalentLMS, you need the following items:</span></span>

- <span data-ttu-id="fa2b8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fa2b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fa2b8-113">已啟用 TalentLMS 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fa2b8-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fa2b8-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fa2b8-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fa2b8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fa2b8-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fa2b8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="fa2b8-118">Scenario description</span></span>
<span data-ttu-id="fa2b8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fa2b8-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fa2b8-121">從資源庫新增 TalentLMS</span><span class="sxs-lookup"><span data-stu-id="fa2b8-121">Adding TalentLMS from the gallery</span></span>
2. <span data-ttu-id="fa2b8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fa2b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-the-gallery"></a><span data-ttu-id="fa2b8-123">從資源庫新增 TalentLMS</span><span class="sxs-lookup"><span data-stu-id="fa2b8-123">Adding TalentLMS from the gallery</span></span>
<span data-ttu-id="fa2b8-124">若要設定將 TalentLMS 整合到 Azure AD 中，您需要從資源庫將 TalentLMS 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fa2b8-125">**若要從資源庫新增 TalentLMS，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fa2b8-125">**To add TalentLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fa2b8-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fa2b8-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fa2b8-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="fa2b8-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="fa2b8-133">在搜尋方塊中，輸入 **TalentLMS**。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-133">In the search box, type **TalentLMS**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="fa2b8-135">在結果窗格中，選取 [TalentLMS]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fa2b8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fa2b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fa2b8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 TalentLMS 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fa2b8-139">若要讓單一登入能夠運作，Azure AD 必須知道 TalentLMS 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span></span> <span data-ttu-id="fa2b8-140">換句話說，必須建立 Azure AD 使用者和 TalentLMS 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span></span>

<span data-ttu-id="fa2b8-141">在 TalentLMS 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fa2b8-142">若要設定及測試與 TalentLMS 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fa2b8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fa2b8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fa2b8-145">**[建立 TalentLMS 測試使用者](#creating-a-talentlms-test-user)** - 使 TalentLMS 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fa2b8-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fa2b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fa2b8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fa2b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fa2b8-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 TalentLMS 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="fa2b8-150">**若要使用 TalentLMS 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fa2b8-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="fa2b8-151">在 Azure 入口網站的 [TalentLMS] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="fa2b8-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="fa2b8-155">在 [TalentLMS 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="fa2b8-157">a.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-157">a.</span></span> <span data-ttu-id="fa2b8-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="fa2b8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="fa2b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-159">b.</span></span> <span data-ttu-id="fa2b8-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="fa2b8-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fa2b8-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-161">These values are not real.</span></span> <span data-ttu-id="fa2b8-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="fa2b8-163">請連絡 [TalentLMS 客戶支援小組](https://www.talentlms.com/contact)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="fa2b8-164">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="fa2b8-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fa2b8-168">在 [TalentLMS 組態] 區段上，按一下 [設定 TalentLMS] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fa2b8-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="fa2b8-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 TalentLMS 公司網站。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="fa2b8-172">在 [帳戶和設定] 區段中，按一下 [使用者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-172">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="fa2b8-173">![帳戶和設定](./media/active-directory-saas-talentlms-tutorial/IC777296.png "帳戶和設定")</span><span class="sxs-lookup"><span data-stu-id="fa2b8-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="fa2b8-174">按一下 [單一登入 (SSO)] 。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="fa2b8-175">在 [單一登入] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-175">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="fa2b8-176">![單一登入](./media/active-directory-saas-talentlms-tutorial/IC777297.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="fa2b8-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="fa2b8-177">a.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-177">a.</span></span> <span data-ttu-id="fa2b8-178">從 [SSO 整合類型] 清單中，選取 [SAML 2.0]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-178">From the **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="fa2b8-179">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-179">b.</span></span> <span data-ttu-id="fa2b8-180">在 [識別提供者]\(IdP\) 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="fa2b8-181">c.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-181">c.</span></span> <span data-ttu-id="fa2b8-182">將 Azure 入口網站的 [指紋] 值貼至 [憑證指紋] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="fa2b8-183">d.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-183">d.</span></span>  <span data-ttu-id="fa2b8-184">在 [遠端登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的**「SAML 單一登入服務 URL」**值。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="fa2b8-185">e.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-185">e.</span></span> <span data-ttu-id="fa2b8-186">在 [遠端登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fa2b8-187">f.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-187">f.</span></span> <span data-ttu-id="fa2b8-188">填寫下列各項：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-188">Fill in the following:</span></span> 

    * <span data-ttu-id="fa2b8-189">在 [TargetedID] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span><span class="sxs-lookup"><span data-stu-id="fa2b8-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="fa2b8-190">在 [名字] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span><span class="sxs-lookup"><span data-stu-id="fa2b8-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="fa2b8-191">在 [姓氏] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span><span class="sxs-lookup"><span data-stu-id="fa2b8-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="fa2b8-192">在 [電子郵件] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="fa2b8-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="fa2b8-193">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="fa2b8-194">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="fa2b8-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fa2b8-195">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fa2b8-196">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fa2b8-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fa2b8-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fa2b8-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="fa2b8-198">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="fa2b8-200">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fa2b8-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fa2b8-201">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fa2b8-203">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fa2b8-205">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fa2b8-207">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fa2b8-209">a.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-209">a.</span></span> <span data-ttu-id="fa2b8-210">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fa2b8-211">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-211">b.</span></span> <span data-ttu-id="fa2b8-212">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fa2b8-213">c.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-213">c.</span></span> <span data-ttu-id="fa2b8-214">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fa2b8-215">d.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-215">d.</span></span> <span data-ttu-id="fa2b8-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="fa2b8-217">建立 TalentLMS 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fa2b8-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="fa2b8-218">若要讓 Azure AD 使用者可以登入 TalentLMS，則必須將他們佈建到 TalentLMS。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="fa2b8-219">TalentLMS 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-219">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="fa2b8-220">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fa2b8-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="fa2b8-221">登入您的 **TalentLMS** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-221">Log in to your **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="fa2b8-222">按一下 [使用者]，然後按一下 [加入使用者]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="fa2b8-223">在 [加入使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fa2b8-223">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="fa2b8-224">![新增使用者](./media/active-directory-saas-talentlms-tutorial/IC777299.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="fa2b8-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="fa2b8-225">a.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-225">a.</span></span> <span data-ttu-id="fa2b8-226">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-226">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="fa2b8-227">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-227">b.</span></span> <span data-ttu-id="fa2b8-228">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="fa2b8-229">c.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-229">c.</span></span> <span data-ttu-id="fa2b8-230">在 [電子郵件地址] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="fa2b8-231">d.</span><span class="sxs-lookup"><span data-stu-id="fa2b8-231">d.</span></span> <span data-ttu-id="fa2b8-232">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="fa2b8-233">您可以使用任何其他的 TalentLMS 使用者帳戶建立工具或 TalentLMS 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fa2b8-234">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fa2b8-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fa2b8-235">在本節中，您會將 TalentLMS 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span></span>

![指派使用者][200] 

<span data-ttu-id="fa2b8-237">**若要將 Britta Simon 指派給 TalentLMS，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="fa2b8-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="fa2b8-238">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="fa2b8-240">在應用程式清單中，選取 [TalentLMS]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-240">In the applications list, select **TalentLMS**.</span></span>

    ![設定單一登入](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="fa2b8-242">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-242">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="fa2b8-244">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-244">Click **Add** button.</span></span> <span data-ttu-id="fa2b8-245">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="fa2b8-247">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fa2b8-248">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fa2b8-249">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fa2b8-250">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="fa2b8-250">Testing single sign-on</span></span>

<span data-ttu-id="fa2b8-251">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="fa2b8-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fa2b8-252">當您在存取面板中按一下 [TalentLMS] 圖格時，應該會自動登入您的 TalentLMS 應用程式</span><span class="sxs-lookup"><span data-stu-id="fa2b8-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fa2b8-253">其他資源</span><span class="sxs-lookup"><span data-stu-id="fa2b8-253">Additional resources</span></span>

* [<span data-ttu-id="fa2b8-254">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="fa2b8-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fa2b8-255">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="fa2b8-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

