---
title: "教學課程：Azure Active Directory 與 Mozy Enterprise 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Mozy Enterprise 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: ac73aadcb8205f24f9d2dbce5af76f53bbcb9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="ebd0a-103">教學課程：Azure Active Directory 與 Mozy Enterprise 整合</span><span class="sxs-lookup"><span data-stu-id="ebd0a-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="ebd0a-104">在本教學課程中，您會了解如何將 Mozy Enterprise 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ebd0a-105">Mozy Enterprise 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ebd0a-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ebd0a-106">您可以在 Azure AD 中控制可存取 Mozy Enterprise 的人員</span><span class="sxs-lookup"><span data-stu-id="ebd0a-106">You can control in Azure AD who has access to Mozy Enterprise</span></span>
- <span data-ttu-id="ebd0a-107">您可以讓使用者使用其 Azure AD 帳戶自動登入 Mozy Enterprise (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ebd0a-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ebd0a-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ebd0a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ebd0a-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebd0a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ebd0a-110">Prerequisites</span></span>

<span data-ttu-id="ebd0a-111">若要設定 Azure AD 與 Mozy Enterprise 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ebd0a-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span></span>

- <span data-ttu-id="ebd0a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ebd0a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ebd0a-113">已啟用 Mozy Enterprise 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ebd0a-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ebd0a-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ebd0a-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ebd0a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ebd0a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ebd0a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ebd0a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ebd0a-118">Scenario description</span></span>
<span data-ttu-id="ebd0a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ebd0a-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ebd0a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ebd0a-121">從資源庫新增 Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="ebd0a-121">Adding Mozy Enterprise from the gallery</span></span>
2. <span data-ttu-id="ebd0a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ebd0a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-the-gallery"></a><span data-ttu-id="ebd0a-123">從資源庫新增 Mozy Enterprise</span><span class="sxs-lookup"><span data-stu-id="ebd0a-123">Adding Mozy Enterprise from the gallery</span></span>
<span data-ttu-id="ebd0a-124">若要設定將 Mozy Enterprise 整合到 Azure AD 中，您需要從資源庫將 Mozy Enterprise 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ebd0a-125">**若要從資源庫新增 Mozy Enterprise，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ebd0a-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ebd0a-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ebd0a-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ebd0a-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ebd0a-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ebd0a-133">在搜尋方塊中，輸入 **Mozy Enterprise**。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-133">In the search box, type **Mozy Enterprise**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="ebd0a-135">在結果窗格中，選取 [Mozy Enterprise]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ebd0a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ebd0a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ebd0a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Mozy Enterprise 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ebd0a-139">若要讓單一登入運作，Azure AD 必須知道 Mozy Enterprise 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="ebd0a-140">換句話說，必須建立 Azure AD 使用者和 Mozy Enterprise 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span></span>

<span data-ttu-id="ebd0a-141">在 Mozy Enterprise 中，將**使用者名稱**的值指派為 Azure AD 中**使用者名稱**的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ebd0a-142">若要設定及測試與 Mozy Enterprise 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ebd0a-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ebd0a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ebd0a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ebd0a-145">**[建立 Mozy Enterprise 測試使用者](#creating-a-mozy-enterprise-test-user)** - 使 Mozy Enterprise 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ebd0a-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ebd0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ebd0a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ebd0a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ebd0a-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Mozy Enterprise 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="ebd0a-150">**若要使用 Mozy Enterprise 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ebd0a-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="ebd0a-151">在 Azure 入口網站的 [Mozy Enterprise] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ebd0a-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="ebd0a-155">在 [Mozy Enterprise 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ebd0a-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="ebd0a-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="ebd0a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ebd0a-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-158">This value is not real.</span></span> <span data-ttu-id="ebd0a-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ebd0a-160">請連絡 [Mozy Enterprise 客戶支援小組](http://support.mozy.com/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span></span>

4. <span data-ttu-id="ebd0a-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="ebd0a-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ebd0a-165">在 [Mozy Enterprise 組態] 區段上，按一下 [設定 Mozy Enterprise] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ebd0a-166">從 [快速參考] 區段中複製 [SAML 實體 ID 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="ebd0a-168">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Mozy Enterprise 公司網站。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="ebd0a-169">在 [組態] 區段中，按一下 [驗證原則]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-169">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="ebd0a-170">![驗證原則](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "驗證原則")</span><span class="sxs-lookup"><span data-stu-id="ebd0a-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="ebd0a-171">在 [驗證原則]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ebd0a-171">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="ebd0a-172">![驗證原則](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "驗證原則")</span><span class="sxs-lookup"><span data-stu-id="ebd0a-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="ebd0a-173">a.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-173">a.</span></span> <span data-ttu-id="ebd0a-174">選取 [目錄服務] 做為**提供者**。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="ebd0a-175">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-175">b.</span></span> <span data-ttu-id="ebd0a-176">選取 [使用 LDAP 推送] 。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="ebd0a-177">c.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-177">c.</span></span> <span data-ttu-id="ebd0a-178">按一下 [SAML 驗證]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-178">Click the **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="ebd0a-179">d.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-179">d.</span></span> <span data-ttu-id="ebd0a-180">將您從 Azure 入口網站複製的「SAML 單一登入服務 URL」貼到 [驗證 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="ebd0a-181">e.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-181">e.</span></span> <span data-ttu-id="ebd0a-182">將您從 Azure 入口網站複製的「SAML 實體識別碼」貼到 [SAML 端點] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="ebd0a-183">f.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-183">f.</span></span> <span data-ttu-id="ebd0a-184">在記事本中開啟您下載的 base-64 編碼的憑證，將它的內容複製到您的剪貼簿，然後將整個憑證貼至 [SAML 憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="ebd0a-185">g.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-185">g.</span></span> <span data-ttu-id="ebd0a-186">選取 [針對管理員啟用 SSO 以使用其網路認證登入] 。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-186">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   
   <span data-ttu-id="ebd0a-187">h.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-187">h.</span></span> <span data-ttu-id="ebd0a-188">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="ebd0a-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ebd0a-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ebd0a-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ebd0a-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ebd0a-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ebd0a-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ebd0a-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="ebd0a-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ebd0a-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ebd0a-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ebd0a-196">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ebd0a-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ebd0a-200">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ebd0a-202">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ebd0a-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ebd0a-204">a.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-204">a.</span></span> <span data-ttu-id="ebd0a-205">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ebd0a-206">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-206">b.</span></span> <span data-ttu-id="ebd0a-207">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ebd0a-208">c.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-208">c.</span></span> <span data-ttu-id="ebd0a-209">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ebd0a-210">d.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-210">d.</span></span> <span data-ttu-id="ebd0a-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="ebd0a-212">建立 Mozy Enterprise 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ebd0a-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="ebd0a-213">為了讓 Azure AD 使用者能夠登入 Mozy Enterprise，必須將他們佈建到 Mozy Enterprise 中。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="ebd0a-214">在 Mozy Enterprise 的情況下，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-214">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="ebd0a-215">您可以使用任何其他的 Mozy Enterprise 使用者帳戶建立工具或 Mozy Enterprise 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>

<span data-ttu-id="ebd0a-216">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ebd0a-216">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="ebd0a-217">登入您的 **Mozy Enterprise** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-217">Log in to your **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="ebd0a-218">按一下 [使用者]，然後按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="ebd0a-219">![使用者](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="ebd0a-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="ebd0a-220">只有在 [驗證原則] 底下選取 [Mozy] 做為提供者時，才會顯示 [新增使用者] 選項。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="ebd0a-221">如果已設定 SAML 驗證，則會在使用者透過單一登入第一次登入時自動新增他們。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="ebd0a-222">在 [新增使用者] 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ebd0a-222">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="ebd0a-223">![新增使用者](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="ebd0a-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="ebd0a-224">a.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-224">a.</span></span> <span data-ttu-id="ebd0a-225">從 [選擇群組]  清單中選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-225">From the **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="ebd0a-226">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-226">b.</span></span> <span data-ttu-id="ebd0a-227">從 [使用者類型]  清單中選取一種類型。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-227">From the **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="ebd0a-228">c.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-228">c.</span></span> <span data-ttu-id="ebd0a-229">在 [使用者名稱]  文字方塊中，輸入 Azure AD 使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-229">In the **Username** textbox, type the name of the Azure AD user.</span></span>
   
   <span data-ttu-id="ebd0a-230">d.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-230">d.</span></span> <span data-ttu-id="ebd0a-231">在 [電子郵件]  文字方塊中，輸入 Azure AD 使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-231">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
   
   <span data-ttu-id="ebd0a-232">e.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-232">e.</span></span> <span data-ttu-id="ebd0a-233">選取 [傳送使用者指示電子郵件] 。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="ebd0a-234">f.</span><span class="sxs-lookup"><span data-stu-id="ebd0a-234">f.</span></span> <span data-ttu-id="ebd0a-235">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="ebd0a-236">建立使用者之後，會寄送一封電子郵件給 Azure AD 使用者，其中包含在帳戶變成作用中之前確認帳戶的連結。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ebd0a-237">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ebd0a-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ebd0a-238">在本節中，您會將 Mozy Enterprise 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span></span>

![指派使用者][200] 

<span data-ttu-id="ebd0a-240">**若要將 Britta Simon 指派給 Mozy Enterprise，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ebd0a-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="ebd0a-241">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ebd0a-243">在應用程式清單中，選取 [Mozy Enterprise]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-243">In the applications list, select **Mozy Enterprise**.</span></span>

    ![設定單一登入](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="ebd0a-245">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-245">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ebd0a-247">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-247">Click **Add** button.</span></span> <span data-ttu-id="ebd0a-248">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ebd0a-250">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ebd0a-251">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ebd0a-252">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ebd0a-253">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ebd0a-253">Testing single sign-on</span></span>

<span data-ttu-id="ebd0a-254">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ebd0a-255">當您按一下存取面板中的 [Mozy Enterprise] 圖格時，您應該會看到 Mozy Enterprise 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="ebd0a-256">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ebd0a-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ebd0a-257">其他資源</span><span class="sxs-lookup"><span data-stu-id="ebd0a-257">Additional resources</span></span>

* [<span data-ttu-id="ebd0a-258">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ebd0a-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ebd0a-259">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ebd0a-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

