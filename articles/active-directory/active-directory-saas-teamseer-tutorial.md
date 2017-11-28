---
title: "教學課程：Azure Active Directory 與 TeamSeer 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 TeamSeer 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a5e8f6d1443681c43db95da5cef0b7f2ef92291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="d9110-103">教學課程：Azure Active Directory 與 TeamSeer 整合</span><span class="sxs-lookup"><span data-stu-id="d9110-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="d9110-104">在本教學課程中，您將了解如何整合 TeamSeer 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d9110-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9110-105">TeamSeer 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d9110-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d9110-106">您可以在 Azure AD 中控制可存取 TeamSeer 的人員</span><span class="sxs-lookup"><span data-stu-id="d9110-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="d9110-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 TeamSeer (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d9110-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9110-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d9110-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d9110-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d9110-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9110-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d9110-110">Prerequisites</span></span>

<span data-ttu-id="d9110-111">若要設定 Azure AD 與 TeamSeer 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d9110-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="d9110-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d9110-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9110-113">已啟用 TeamSeer 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d9110-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9110-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d9110-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9110-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d9110-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9110-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d9110-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9110-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d9110-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9110-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d9110-118">Scenario description</span></span>
<span data-ttu-id="d9110-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9110-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9110-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d9110-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9110-121">從資源庫新增 TeamSeer</span><span class="sxs-lookup"><span data-stu-id="d9110-121">Adding TeamSeer from the gallery</span></span>
2. <span data-ttu-id="d9110-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d9110-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="d9110-123">從資源庫新增 TeamSeer</span><span class="sxs-lookup"><span data-stu-id="d9110-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="d9110-124">若要設定 TeamSeer 與 Azure AD 整合，您需要從資源庫將 TeamSeer 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d9110-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d9110-125">**若要從資源庫新增 TeamSeer，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9110-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d9110-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d9110-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d9110-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d9110-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d9110-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d9110-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d9110-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9110-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d9110-133">在搜尋方塊中，輸入 **TeamSeer**。</span><span class="sxs-lookup"><span data-stu-id="d9110-133">In the search box, type **TeamSeer**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="d9110-135">在結果窗格中，選取 [TeamSeer]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9110-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9110-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d9110-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9110-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 TeamSeer 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9110-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9110-139">若要讓單一登入運作，Azure AD 必須知道 TeamSeer 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d9110-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="d9110-140">換句話說，必須在 Azure AD 使用者和 TeamSeer 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d9110-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="d9110-141">在 TeamSeer 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d9110-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d9110-142">若要設定及測試與 TeamSeer 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d9110-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d9110-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d9110-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d9110-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9110-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9110-145">**[建立 TeamSeer 測試使用者](#creating-a-teamseer-test-user)** - 使 TeamSeer 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="d9110-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9110-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9110-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9110-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d9110-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9110-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d9110-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9110-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 TeamSeer 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9110-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="d9110-150">**若要設定與 TeamSeer 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9110-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="d9110-151">在 Azure 入口網站的 [TeamSeer] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d9110-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d9110-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9110-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="d9110-155">在 [TeamSeer 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9110-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="d9110-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="d9110-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9110-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="d9110-158">The value is not real.</span></span> <span data-ttu-id="d9110-159">使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="d9110-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="d9110-160">請連絡 [TeamSeer 客戶支援小組](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="d9110-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
4. <span data-ttu-id="d9110-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d9110-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="d9110-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9110-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d9110-165">在 [TeamSeer 組態] 區段上，按一下 [設定 TeamSeer] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d9110-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d9110-166">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="d9110-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="d9110-168">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 TeamSeer 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d9110-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="d9110-169">移至 [HR 管理] 。</span><span class="sxs-lookup"><span data-stu-id="d9110-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="d9110-170">![HR 管理](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR 管理")</span><span class="sxs-lookup"><span data-stu-id="d9110-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="d9110-171">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="d9110-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="d9110-172">![設定](./media/active-directory-saas-teamseer-tutorial/ic789635.png "設定")</span><span class="sxs-lookup"><span data-stu-id="d9110-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="d9110-173">按一下 [設定 SAML 提供者詳細資料] 。</span><span class="sxs-lookup"><span data-stu-id="d9110-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="d9110-174">![SAML 設定](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="d9110-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="d9110-175">在 [SAML 提供者詳細資料] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9110-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="d9110-176">![SAML 設定](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="d9110-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="d9110-177">a.</span><span class="sxs-lookup"><span data-stu-id="d9110-177">a.</span></span> <span data-ttu-id="d9110-178">將 [單一登入服務 URL] 的值貼到 [URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="d9110-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="d9110-179">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9110-179">b.</span></span> <span data-ttu-id="d9110-180">在記事本中開啟 Base-64 編碼的憑證，將其內容複製到剪貼簿，然後貼到 [IdP 公開憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="d9110-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="d9110-181">若要完成 SAML 提供者的設定，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9110-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="d9110-182">![SAML 設定](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="d9110-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="d9110-183">a.</span><span class="sxs-lookup"><span data-stu-id="d9110-183">a.</span></span> <span data-ttu-id="d9110-184">在 [測試電子郵件地址] 中輸入測試使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="d9110-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="d9110-185">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9110-185">b.</span></span> <span data-ttu-id="d9110-186">在 [簽發者]  文字方塊中輸入服務提供者的簽發者 URL。</span><span class="sxs-lookup"><span data-stu-id="d9110-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="d9110-187">c.</span><span class="sxs-lookup"><span data-stu-id="d9110-187">c.</span></span> <span data-ttu-id="d9110-188">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d9110-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d9110-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="d9110-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d9110-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d9110-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d9110-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9110-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9110-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9110-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9110-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d9110-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d9110-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9110-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d9110-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d9110-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d9110-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d9110-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9110-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d9110-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9110-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9110-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9110-204">a.</span><span class="sxs-lookup"><span data-stu-id="d9110-204">a.</span></span> <span data-ttu-id="d9110-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d9110-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9110-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9110-206">b.</span></span> <span data-ttu-id="d9110-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d9110-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9110-208">c.</span><span class="sxs-lookup"><span data-stu-id="d9110-208">c.</span></span> <span data-ttu-id="d9110-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d9110-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d9110-210">d.</span><span class="sxs-lookup"><span data-stu-id="d9110-210">d.</span></span> <span data-ttu-id="d9110-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d9110-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="d9110-212">建立 TeamSeer 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9110-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="d9110-213">若要讓 Azure AD 使用者可以登入 TeamSeer，則必須將他們佈建到 ShiftPlanning。</span><span class="sxs-lookup"><span data-stu-id="d9110-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="d9110-214">TeamSeer 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="d9110-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="d9110-215">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9110-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d9110-216">以系統管理員身分登入您的 **TeamSeer** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d9110-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="d9110-217">執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9110-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="d9110-218">![HR 管理](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR 管理")</span><span class="sxs-lookup"><span data-stu-id="d9110-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="d9110-219">a.</span><span class="sxs-lookup"><span data-stu-id="d9110-219">a.</span></span> <span data-ttu-id="d9110-220">移至 [HR 管理] \> [使用者]。</span><span class="sxs-lookup"><span data-stu-id="d9110-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="d9110-221">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9110-221">b.</span></span> <span data-ttu-id="d9110-222">按一下 [執行新增使用者精靈] 。</span><span class="sxs-lookup"><span data-stu-id="d9110-222">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="d9110-223">在 [使用者詳細資料]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d9110-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="d9110-224">![使用者詳細資料](./media/active-directory-saas-teamseer-tutorial/ic789641.png "使用者詳細資料")</span><span class="sxs-lookup"><span data-stu-id="d9110-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="d9110-225">a.</span><span class="sxs-lookup"><span data-stu-id="d9110-225">a.</span></span> <span data-ttu-id="d9110-226">在相關的文字方塊中，輸入您想要佈建之有效 AAD 帳戶的 [名字]、[姓氏] 和 [使用者名稱 (電子郵件地址)]。</span><span class="sxs-lookup"><span data-stu-id="d9110-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="d9110-227">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9110-227">b.</span></span> <span data-ttu-id="d9110-228">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d9110-228">Click **Next**.</span></span>

4. <span data-ttu-id="d9110-229">請遵循畫面上的指示來新增新使用者，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="d9110-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="d9110-230">您可以使用任何其他的 TeamSeer 使用者帳戶建立工具或 TeamSeer 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="d9110-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d9110-231">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d9110-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d9110-232">在本節中，您會將 TeamSeer 的存取權授與 Britta Simon，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d9110-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![指派使用者][200] 

<span data-ttu-id="d9110-234">**若要將 Britta Simon 指派給 TeamSeer，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d9110-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="d9110-235">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d9110-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d9110-237">在應用程式清單中，選取 [TeamSeer]。</span><span class="sxs-lookup"><span data-stu-id="d9110-237">In the applications list, select **TeamSeer**.</span></span>

    ![設定單一登入](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="d9110-239">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d9110-239">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d9110-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9110-241">Click **Add** button.</span></span> <span data-ttu-id="d9110-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d9110-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d9110-244">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d9110-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d9110-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9110-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9110-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d9110-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9110-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d9110-247">Testing single sign-on</span></span>

<span data-ttu-id="d9110-248">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="d9110-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d9110-249">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d9110-249">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9110-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="d9110-250">Additional resources</span></span>

* [<span data-ttu-id="d9110-251">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d9110-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9110-252">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d9110-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

