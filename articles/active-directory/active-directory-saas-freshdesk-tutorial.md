---
title: "教學課程：Azure Active Directory 與 FreshDesk 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 FreshDesk 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: f4b47e345a40b64f69ad8a4618564662b4a6c879
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="6eb35-103">教學課程：Azure Active Directory 與 FreshDesk 整合</span><span class="sxs-lookup"><span data-stu-id="6eb35-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="6eb35-104">在本教學課程中，您會了解如何整合 FreshDesk 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6eb35-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6eb35-105">FreshDesk 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="6eb35-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6eb35-106">您可以在 Azure AD 中控制可存取 FreshDesk 的人員</span><span class="sxs-lookup"><span data-stu-id="6eb35-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="6eb35-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 FreshDesk (單一登入)</span><span class="sxs-lookup"><span data-stu-id="6eb35-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6eb35-108">您可以在 Azure 管理入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="6eb35-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="6eb35-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6eb35-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6eb35-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6eb35-110">Prerequisites</span></span>

<span data-ttu-id="6eb35-111">若要設定與 FreshDesk 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6eb35-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="6eb35-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6eb35-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6eb35-113">啟用 FreshDesk 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6eb35-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6eb35-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6eb35-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6eb35-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6eb35-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6eb35-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="6eb35-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6eb35-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="6eb35-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6eb35-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6eb35-118">Scenario description</span></span>
<span data-ttu-id="6eb35-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6eb35-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6eb35-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="6eb35-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6eb35-121">從資源庫新增 FreshDesk</span><span class="sxs-lookup"><span data-stu-id="6eb35-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="6eb35-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6eb35-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="6eb35-123">從資源庫新增 FreshDesk</span><span class="sxs-lookup"><span data-stu-id="6eb35-123">Adding FreshDesk from the gallery</span></span>
<span data-ttu-id="6eb35-124">若要設定 FreshDesk 與 Azure AD 整合，您需要從資源庫將 FreshDesk 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="6eb35-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6eb35-125">**若要從資源庫新增 FreshDesk，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6eb35-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6eb35-126">在 **[Azure 管理入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6eb35-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6eb35-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6eb35-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="6eb35-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6eb35-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="6eb35-133">在搜尋方塊中，輸入 **FreshDesk**。</span><span class="sxs-lookup"><span data-stu-id="6eb35-133">In the search box, type **FreshDesk**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="6eb35-135">在結果窗格中，選取 [FreshDesk]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eb35-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6eb35-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6eb35-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6eb35-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FreshDesk 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6eb35-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6eb35-139">若要讓單一登入運作，Azure AD 必須知道 FreshDesk 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="6eb35-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="6eb35-140">換句話說，必須建立 Azure AD 使用者和 FreshDesk 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6eb35-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="6eb35-141">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值指定為 FreshDesk 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="6eb35-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="6eb35-142">若要設定及測試與 FreshDesk 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6eb35-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6eb35-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="6eb35-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6eb35-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6eb35-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6eb35-145">**[建立 FreshDesk 測試使用者](#creating-a-freshdesk-test-user)** - 讓 FreshDesk 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="6eb35-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6eb35-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6eb35-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6eb35-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="6eb35-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6eb35-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6eb35-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6eb35-149">在本節中，您會在 Azure 管理入口網站中啟用 Azure AD 單一登入，並在您的 FreshDesk 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6eb35-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="6eb35-150">**若要設定與 FreshDesk 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6eb35-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="6eb35-151">在 Azure 管理入口網站的 [FreshDesk] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="6eb35-153">在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6eb35-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="6eb35-155">在 [FreshDesk 網域和 URL] 區段中，請將**登入 URL** 輸入為：`https://<tenant-name>.freshdesk.com`，或者 Freshdesk 建議的其他任何值。</span><span class="sxs-lookup"><span data-stu-id="6eb35-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="6eb35-157">請注意，這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="6eb35-157">Please note that this is not the real value.</span></span> <span data-ttu-id="6eb35-158">您必須使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="6eb35-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="6eb35-159">請連絡 [FreshDesk 用戶端支援小組](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="6eb35-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="6eb35-160">在 [SAML 簽署憑證] 區段上，按一下 [憑證]，然後將憑證儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6eb35-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="6eb35-162">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6eb35-162">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6eb35-164">在 [FreshDesk 組態] 區段上，按一下 [設定 FreshDesk] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6eb35-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="6eb35-165">從 [快速參考]區段中複製 [SAML 單一登入服務 URL 和登出 URL]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="6eb35-167">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Freshdesk 公司網站。</span><span class="sxs-lookup"><span data-stu-id="6eb35-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="6eb35-168">在頂端的功能表中，按一下 [系統管理員] 。</span><span class="sxs-lookup"><span data-stu-id="6eb35-168">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="6eb35-169">![管理](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "管理")</span><span class="sxs-lookup"><span data-stu-id="6eb35-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="6eb35-170">在 [一般設定] 索引標籤上，按一下 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-170">In the **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="6eb35-171">![安全性](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="6eb35-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="6eb35-172">在 [安全性]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6eb35-172">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="6eb35-173">![單一登入](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="6eb35-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="6eb35-174">a.</span><span class="sxs-lookup"><span data-stu-id="6eb35-174">a.</span></span> <span data-ttu-id="6eb35-175">針對 [單一登入 (SSO)] 選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="6eb35-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eb35-176">b.</span></span> <span data-ttu-id="6eb35-177">選取 [SAML SSO] 。</span><span class="sxs-lookup"><span data-stu-id="6eb35-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="6eb35-178">c.</span><span class="sxs-lookup"><span data-stu-id="6eb35-178">c.</span></span> <span data-ttu-id="6eb35-179">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 輸入到 [SAML 登入 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6eb35-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="6eb35-180">d.</span><span class="sxs-lookup"><span data-stu-id="6eb35-180">d.</span></span> <span data-ttu-id="6eb35-181">將您從 Azure 入口網站複製的 [登出 URL] 輸入到 [登出 URL] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6eb35-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="6eb35-182">e.</span><span class="sxs-lookup"><span data-stu-id="6eb35-182">e.</span></span> <span data-ttu-id="6eb35-183">從 Azure 入口網站的已下載憑證複製**指紋**值，然後將它貼入 [安全性憑證指紋] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="6eb35-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="6eb35-184">如需詳細資訊，請參閱[如何抓取憑證的指紋值](http://youtu.be/YKQF266SAxI)。</span><span class="sxs-lookup"><span data-stu-id="6eb35-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="6eb35-185">f.</span><span class="sxs-lookup"><span data-stu-id="6eb35-185">f.</span></span> <span data-ttu-id="6eb35-186">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6eb35-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6eb35-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6eb35-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="6eb35-188">本節目標是在 Azure 管理入口網站中建立名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6eb35-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="6eb35-190">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6eb35-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6eb35-191">在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6eb35-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6eb35-193">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="6eb35-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6eb35-195">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6eb35-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6eb35-197">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6eb35-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6eb35-199">a.</span><span class="sxs-lookup"><span data-stu-id="6eb35-199">a.</span></span> <span data-ttu-id="6eb35-200">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6eb35-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6eb35-201">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eb35-201">b.</span></span> <span data-ttu-id="6eb35-202">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="6eb35-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6eb35-203">c.</span><span class="sxs-lookup"><span data-stu-id="6eb35-203">c.</span></span> <span data-ttu-id="6eb35-204">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="6eb35-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6eb35-205">d.</span><span class="sxs-lookup"><span data-stu-id="6eb35-205">d.</span></span> <span data-ttu-id="6eb35-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6eb35-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="6eb35-207">建立 FreshDesk 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6eb35-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="6eb35-208">若要讓 Azure AD 使用者可以登入 FreshDesk，則必須將他們佈建到 FreshDesk。</span><span class="sxs-lookup"><span data-stu-id="6eb35-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="6eb35-209">FreshDesk 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="6eb35-209">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="6eb35-210">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6eb35-210">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="6eb35-211">登入您的 **Freshdesk** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="6eb35-211">Log in to your **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="6eb35-212">在頂端的功能表中，按一下 [系統管理員] 。</span><span class="sxs-lookup"><span data-stu-id="6eb35-212">In the menu on the top, click **Admin**.</span></span>
   
   <span data-ttu-id="6eb35-213">![管理](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "管理")</span><span class="sxs-lookup"><span data-stu-id="6eb35-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="6eb35-214">在 [一般設定] 索引標籤上，按一下 [代理程式]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-214">In the **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="6eb35-215">![代理程式](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "代理程式")</span><span class="sxs-lookup"><span data-stu-id="6eb35-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="6eb35-216">按一下 [新增代理程式] 。</span><span class="sxs-lookup"><span data-stu-id="6eb35-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="6eb35-217">![新代理程式](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "新代理程式")</span><span class="sxs-lookup"><span data-stu-id="6eb35-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="6eb35-218">在 [代理程式資訊] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6eb35-218">On the Agent Information dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="6eb35-219">![代理程式資訊](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "代理程式資訊")</span><span class="sxs-lookup"><span data-stu-id="6eb35-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="6eb35-220">a.</span><span class="sxs-lookup"><span data-stu-id="6eb35-220">a.</span></span> <span data-ttu-id="6eb35-221">在 [全名]  文字方塊中，輸入您要佈建的 Azure AD 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6eb35-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="6eb35-222">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eb35-222">b.</span></span> <span data-ttu-id="6eb35-223">在 [電子郵件]  文字方塊中，輸入您要佈建的 Azure AD 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="6eb35-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="6eb35-224">c.</span><span class="sxs-lookup"><span data-stu-id="6eb35-224">c.</span></span> <span data-ttu-id="6eb35-225">在 [職稱]  文字方塊中，輸入您要佈建的 Azure AD 帳戶的職稱。</span><span class="sxs-lookup"><span data-stu-id="6eb35-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="6eb35-226">d.</span><span class="sxs-lookup"><span data-stu-id="6eb35-226">d.</span></span> <span data-ttu-id="6eb35-227">選取 [代理程式角色]，然後按一下 [指派]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="6eb35-228">e.</span><span class="sxs-lookup"><span data-stu-id="6eb35-228">e.</span></span> <span data-ttu-id="6eb35-229">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6eb35-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="6eb35-230">Azure AD 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="6eb35-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="6eb35-231">您可以使用任何其他的 Freshdesk 使用者帳戶建立工具或 Freshdesk 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="6eb35-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span> <span data-ttu-id="6eb35-232">至 FreshDesk。</span><span class="sxs-lookup"><span data-stu-id="6eb35-232">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6eb35-233">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6eb35-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6eb35-234">在本節中，您會將 FreshDesk 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6eb35-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![指派使用者][200] 

<span data-ttu-id="6eb35-236">**若要將 Britta Simon 指派到 FreshDesk，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="6eb35-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="6eb35-237">在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6eb35-239">在應用程式清單中，選取 [FreshDesk] 。</span><span class="sxs-lookup"><span data-stu-id="6eb35-239">In the applications list, select **FreshDesk**.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="6eb35-241">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-241">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="6eb35-243">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6eb35-243">Click **Add** button.</span></span> <span data-ttu-id="6eb35-244">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="6eb35-246">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="6eb35-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6eb35-247">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6eb35-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6eb35-248">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6eb35-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6eb35-249">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6eb35-249">Testing single sign-on</span></span>

<span data-ttu-id="6eb35-250">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="6eb35-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6eb35-251">當您在存取面板中按一下 FreshDesk 圖格時，您應該會進入登入頁面以便登入您的 FreshDesk 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eb35-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6eb35-252">其他資源</span><span class="sxs-lookup"><span data-stu-id="6eb35-252">Additional resources</span></span>

* [<span data-ttu-id="6eb35-253">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="6eb35-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6eb35-254">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6eb35-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

