---
title: "教學課程：Azure Active Directory 與 SkyDesk Email 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SkyDesk Email 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 0ffcca4161fc836192fc9c9871a905f36ea76b32
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="8aa3f-103">教學課程：Azure Active Directory 與 SkyDesk Email 整合</span><span class="sxs-lookup"><span data-stu-id="8aa3f-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="8aa3f-104">在本教學課程中，您將了解如何整合 SkyDesk Email 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-104">In this tutorial, you learn how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8aa3f-105">SkyDesk Email 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="8aa3f-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8aa3f-106">您可以在 Azure AD 中控制可存取 SkyDesk Email 的人員</span><span class="sxs-lookup"><span data-stu-id="8aa3f-106">You can control in Azure AD who has access to SkyDesk Email</span></span>
- <span data-ttu-id="8aa3f-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SkyDesk Email (單一登入)</span><span class="sxs-lookup"><span data-stu-id="8aa3f-107">You can enable your users to automatically get signed-on to SkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8aa3f-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="8aa3f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8aa3f-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8aa3f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8aa3f-110">Prerequisites</span></span>

<span data-ttu-id="8aa3f-111">若要設定與 SkyDesk Email 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="8aa3f-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span></span>

- <span data-ttu-id="8aa3f-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8aa3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8aa3f-113">已啟用 Skydesk Email 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8aa3f-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8aa3f-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8aa3f-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8aa3f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8aa3f-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8aa3f-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8aa3f-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8aa3f-118">Scenario description</span></span>
<span data-ttu-id="8aa3f-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8aa3f-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="8aa3f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8aa3f-121">從資源庫加入 SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="8aa3f-121">Adding SkyDesk Email from the gallery</span></span>
2. <span data-ttu-id="8aa3f-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8aa3f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-the-gallery"></a><span data-ttu-id="8aa3f-123">從資源庫加入 SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="8aa3f-123">Adding SkyDesk Email from the gallery</span></span>
<span data-ttu-id="8aa3f-124">若要設定 SkyDesk Email 與 Azure AD 整合，您需要從資源庫將 SkyDesk Email 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8aa3f-125">**若要從資源庫加入 SkyDesk Email，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8aa3f-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8aa3f-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8aa3f-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8aa3f-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8aa3f-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8aa3f-133">在搜尋方塊中，輸入 **SkyDesk Email**。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-133">In the search box, type **SkyDesk Email**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="8aa3f-135">在結果窗格中，選取 [SkyDesk Email]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-135">In the results panel, select **SkyDesk Email**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8aa3f-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8aa3f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8aa3f-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SkyDesk Email 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8aa3f-139">若要讓單一登入運作，Azure AD 必須知道 SkyDesk Email 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SkyDesk Email is to a user in Azure AD.</span></span> <span data-ttu-id="8aa3f-140">換句話說，必須在 Azure AD 使用者與 SkyDesk Email 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-140">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span></span>

<span data-ttu-id="8aa3f-141">在 SkyDesk Email 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-141">In SkyDesk Email, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8aa3f-142">若要設定及測試對 SkyDesk Email 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8aa3f-142">To configure and test Azure AD single sign-on with SkyDesk Email, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8aa3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8aa3f-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8aa3f-145">**[建立 SkyDesk Email 測試使用者](#creating-a-skydesk-email-test-user)** - 使 SkyDesk Email 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8aa3f-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8aa3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8aa3f-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8aa3f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8aa3f-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 SkyDesk Email 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="8aa3f-150">**若要使用 SkyDesk Email 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8aa3f-150">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="8aa3f-151">在 Azure 入口網站的 [SkyDesk Email] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-151">In the Azure portal, on the **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8aa3f-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="8aa3f-155">在 [SkyDesk Email 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8aa3f-155">On the **SkyDesk Email Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="8aa3f-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8aa3f-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8aa3f-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-158">The value is not real.</span></span> <span data-ttu-id="8aa3f-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="8aa3f-160">請連絡 [SkyDesk Email 客戶支援小組](https://www.skydesk.sg/support/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) to get the value.</span></span> 
 
4. <span data-ttu-id="8aa3f-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="8aa3f-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8aa3f-165">在 [SkyDesk Email 組態] 區段上，按一下 [設定 SkyDesk Email] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-165">On the **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8aa3f-166">從 [快速參考] 區段中複製 [登入 URL] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="8aa3f-168">若要在 **SkyDesk Email**中啟用 SSO，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8aa3f-168">To enable SSO in **SkyDesk Email**, perform the following steps:</span></span>

    <span data-ttu-id="8aa3f-169">a.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-169">a.</span></span> <span data-ttu-id="8aa3f-170">以系統管理員身分登入 SkyDesk Email 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-170">Sign-on to your SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="8aa3f-171">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-171">b.</span></span> <span data-ttu-id="8aa3f-172">在頂端的功能表中，按一下 [設定]，然後選取 [組織]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-172">In the menu on the top, click **Setup**, and select **Org**.</span></span> 
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="8aa3f-174">c.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-174">c.</span></span> <span data-ttu-id="8aa3f-175">按一下左面板中的 [網域]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-175">Click on **Domains** from the left panel.</span></span>
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="8aa3f-177">d.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-177">d.</span></span> <span data-ttu-id="8aa3f-178">按一下 [加入網域]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-178">Click on **Add Domain**.</span></span>
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="8aa3f-180">e.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-180">e.</span></span> <span data-ttu-id="8aa3f-181">輸入您的網域名稱，然後驗證網域。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-181">Enter your Domain name, and then verify the Domain.</span></span>
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="8aa3f-183">f.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-183">f.</span></span> <span data-ttu-id="8aa3f-184">從左方面板按一下 [SAML 驗證]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-184">Click on **SAML Authentication** from the left panel.</span></span>
    
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="8aa3f-186">在 [SAML 驗證]  對話方塊頁面上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8aa3f-186">On the **SAML Authentication** dialog page, perform the following steps:</span></span>
   
      ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="8aa3f-188">若要使用 SAML 驗證，您應該已經設定**驗證網域**或**入口網站 URL**。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-188">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="8aa3f-189">您可以使用唯一名稱設定入口網站 URL。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-189">You can set the portal URL with the unique name.</span></span>
    > 
    > 
   
    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="8aa3f-191">a.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-191">a.</span></span> <span data-ttu-id="8aa3f-192">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-192">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="8aa3f-193">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-193">b.</span></span> <span data-ttu-id="8aa3f-194">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-194">In the **Logout** URL textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8aa3f-195">c.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-195">c.</span></span> <span data-ttu-id="8aa3f-196">[變更密碼 URL] 是選擇性的，將它保留為空白。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="8aa3f-197">d.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-197">d.</span></span> <span data-ttu-id="8aa3f-198">按一下 [從檔案取得金鑰] 以從 Azure 入口網站選取您下載的憑證，然後按一下 [開啟] 以上傳憑證。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-198">Click on **Get Key From File** to select your downloaded certificate from Azure portal, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="8aa3f-199">e.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-199">e.</span></span> <span data-ttu-id="8aa3f-200">選取 [RSA] 做為 [演算法]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="8aa3f-201">f.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-201">f.</span></span> <span data-ttu-id="8aa3f-202">按一下 [確定] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-202">Click **Ok** to save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="8aa3f-203">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="8aa3f-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8aa3f-204">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8aa3f-205">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8aa3f-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8aa3f-206">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8aa3f-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="8aa3f-207">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8aa3f-209">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8aa3f-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8aa3f-210">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8aa3f-212">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8aa3f-214">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8aa3f-216">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8aa3f-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8aa3f-218">a.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-218">a.</span></span> <span data-ttu-id="8aa3f-219">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8aa3f-220">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-220">b.</span></span> <span data-ttu-id="8aa3f-221">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8aa3f-222">c.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-222">c.</span></span> <span data-ttu-id="8aa3f-223">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8aa3f-224">d.</span><span class="sxs-lookup"><span data-stu-id="8aa3f-224">d.</span></span> <span data-ttu-id="8aa3f-225">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="8aa3f-226">建立 SkyDesk Email 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8aa3f-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="8aa3f-227">在本節中，您要在 SkyDesk Email 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="8aa3f-228">在 SkyDesk Email 中按一下左方面板的 [使用者存取]，然後輸入您的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-228">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span></span> 

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="8aa3f-230">如果您需要建立大量使用者，您需要連絡 [SkyDesk Email 客戶支援小組](https://www.skydesk.sg/support/)。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-230">If you need to create bulk users, you need to contact the [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8aa3f-231">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8aa3f-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8aa3f-232">在本節中，您會將 SkyDesk Email 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SkyDesk Email.</span></span>

![指派使用者][200] 

<span data-ttu-id="8aa3f-234">**若要將 Britta Simon 指派到 SkyDesk Email，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="8aa3f-234">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="8aa3f-235">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8aa3f-237">在應用程式清單中，選取 [SkyDesk Email] 。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-237">In the applications list, select **SkyDesk Email**.</span></span>

    ![設定單一登入](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="8aa3f-239">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-239">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8aa3f-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-241">Click **Add** button.</span></span> <span data-ttu-id="8aa3f-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8aa3f-244">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8aa3f-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8aa3f-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8aa3f-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8aa3f-247">Testing single sign-on</span></span>

<span data-ttu-id="8aa3f-248">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="8aa3f-249">當您在存取面板中按一下 [SkyDesk Email] 圖格時，應該會自動登入您的 SkyDesk Email 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8aa3f-249">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8aa3f-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="8aa3f-250">Additional resources</span></span>

* [<span data-ttu-id="8aa3f-251">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="8aa3f-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8aa3f-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8aa3f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

