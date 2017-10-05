---
title: "教學課程：Azure Active Directory 與 Optimizely 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Optimizely 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 4d6f6da6bace09fbd6ab105530a1162653675c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="0a5b1-103">教學課程：Azure Active Directory 與 Optimizely 整合</span><span class="sxs-lookup"><span data-stu-id="0a5b1-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="0a5b1-104">在本教學課程中，您會了解如何整合 Optimizely 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a5b1-105">Optimizely 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="0a5b1-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a5b1-106">您可以在 Azure AD 中控制可存取 Optimizely 的人員</span><span class="sxs-lookup"><span data-stu-id="0a5b1-106">You can control in Azure AD who has access to Optimizely</span></span>
- <span data-ttu-id="0a5b1-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Optimizely (單一登入)</span><span class="sxs-lookup"><span data-stu-id="0a5b1-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a5b1-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="0a5b1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a5b1-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a5b1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a5b1-110">Prerequisites</span></span>

<span data-ttu-id="0a5b1-111">若要設定 Optimizely 與 Azure AD 的整合作業，需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0a5b1-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

- <span data-ttu-id="0a5b1-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0a5b1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a5b1-113">啟用 Optimizely 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0a5b1-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a5b1-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a5b1-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0a5b1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a5b1-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a5b1-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a5b1-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0a5b1-118">Scenario description</span></span>
<span data-ttu-id="0a5b1-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a5b1-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="0a5b1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a5b1-121">從資源庫中新增 Optimizely</span><span class="sxs-lookup"><span data-stu-id="0a5b1-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="0a5b1-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0a5b1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-the-gallery"></a><span data-ttu-id="0a5b1-123">從資源庫中新增 Optimizely</span><span class="sxs-lookup"><span data-stu-id="0a5b1-123">Adding Optimizely from the gallery</span></span>
<span data-ttu-id="0a5b1-124">若要設定將 Optimizely 整合到 Azure AD 中，您需要從資源庫將 Optimizely 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a5b1-125">**若要從資源庫新增 Optimizely，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0a5b1-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5b1-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a5b1-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a5b1-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0a5b1-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0a5b1-133">在搜尋方塊中，輸入 **Optimizely**。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-133">In the search box, type **Optimizely**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="0a5b1-135">在結果窗格中，選取 [Optimizely]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a5b1-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0a5b1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a5b1-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Optimizely 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a5b1-139">若要讓單一登入運作，Azure AD 必須知道 Optimizely 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="0a5b1-140">換句話說，必須在 Azure AD 使用者與 Optimizely 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="0a5b1-141">建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值指定為 Optimizely 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="0a5b1-142">若要設定及測試與 Optimizely 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="0a5b1-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a5b1-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a5b1-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a5b1-145">**[建立 Optimizely 測試使用者](#creating-an-optimizely-test-user)** - 使 Optimizely 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a5b1-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a5b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a5b1-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0a5b1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a5b1-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Optimizely 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="0a5b1-150">**若要設定與 Optimizely 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0a5b1-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5b1-151">在 Azure 入口網站的 [Optimizely] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0a5b1-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="0a5b1-155">在 [Optimizely 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0a5b1-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="0a5b1-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a5b1-157">a.</span></span> <span data-ttu-id="0a5b1-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="0a5b1-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="0a5b1-159">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-159">b.</span></span> <span data-ttu-id="0a5b1-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="0a5b1-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a5b1-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-161">These values are not the real.</span></span> <span data-ttu-id="0a5b1-162">您將會使用實際的「登入 URL」與「識別碼」來更新值，稍後會在本教學課程中說明。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="0a5b1-163">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="0a5b1-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-165">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0a5b1-167">在 [Optimizely 組態] 區段上，按一下 [設定 Optimizely] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-167">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0a5b1-168">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="0a5b1-170">若要在 **Optimizely** 端設定單一登入，請連絡您的 Optimizely Account Manager 並提供已下載的**憑證 (Base64)**與**SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-170">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="0a5b1-171">Optimizely 會回應您的電子郵件，提供單一登入 URL (SP 啟始的 SSO) 和識別碼 (服務提供者的實體識別碼) 的值。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-171">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="0a5b1-172">a.</span><span class="sxs-lookup"><span data-stu-id="0a5b1-172">a.</span></span> <span data-ttu-id="0a5b1-173">複製 Optimizely 提供的**SP 啟始的 SSO URL**，並貼到 Azure 入口網站上 [Optimizely 網域及 URL] 區段的 [登入 URL] 文字方塊</span><span class="sxs-lookup"><span data-stu-id="0a5b1-173">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="0a5b1-174">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-174">b.</span></span> <span data-ttu-id="0a5b1-175">複製 Optimizely 提供的**服務提供者的實體識別碼**，並貼到 Azure 入口網站上 [Optimizely 網域及 URL] 區段的 [識別碼] 文字方塊</span><span class="sxs-lookup"><span data-stu-id="0a5b1-175">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="0a5b1-176">在不同的瀏覽器視窗中，登入您的 Optimizely 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-176">In a different browser window, sign-on to your Optimizely application.</span></span>

10. <span data-ttu-id="0a5b1-177">按一下您在右上角的帳戶名稱，然後按 [帳戶設定] 。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-177">Click you account name in the top right corner and then **Account Settings**.</span></span>
   
    ![Azure AD 單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="0a5b1-179">在 [帳戶] 索引標籤的 [概觀] 區段中，選取 [單一登入] 下的 [啟用 SSO] 方塊。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-179">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
   
    ![Azure AD 單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="0a5b1-181">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="0a5b1-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="0a5b1-182">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="0a5b1-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a5b1-183">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a5b1-184">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a5b1-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a5b1-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0a5b1-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a5b1-186">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0a5b1-188">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0a5b1-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5b1-189">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a5b1-191">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a5b1-193">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a5b1-195">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0a5b1-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a5b1-197">a.</span><span class="sxs-lookup"><span data-stu-id="0a5b1-197">a.</span></span> <span data-ttu-id="0a5b1-198">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a5b1-199">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-199">b.</span></span> <span data-ttu-id="0a5b1-200">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="0a5b1-201">c.</span><span class="sxs-lookup"><span data-stu-id="0a5b1-201">c.</span></span> <span data-ttu-id="0a5b1-202">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a5b1-203">d.</span><span class="sxs-lookup"><span data-stu-id="0a5b1-203">d.</span></span> <span data-ttu-id="0a5b1-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="0a5b1-205">建立 Optimizely 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0a5b1-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="0a5b1-206">在本節中，您會在 Optimizely 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="0a5b1-207">在首頁上，選取 [Collaborators] \(共同作業者) 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-207">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="0a5b1-208">若要將新的共同作業者加入專案，請按一下 [新增共同作業者]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-208">To add new collaborator to the project, click **New Collaborator**.</span></span>
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="0a5b1-210">填寫電子郵件地址，並為其指派角色。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-210">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="0a5b1-211">按一下 [邀請] 。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-211">Click **Invite**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="0a5b1-213">這些人員會收到一封電子郵件邀請。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-213">They receive an email invite.</span></span> <span data-ttu-id="0a5b1-214">他們必須使用該電子郵件地址來登入 Optimizely。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-214">Using the email address, they have to log in to Optimizely.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a5b1-215">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0a5b1-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a5b1-216">在本節中，您會把 Optimizely 的存取權授與 Britta Simon，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span></span>

![指派使用者][200] 

<span data-ttu-id="0a5b1-218">**若要將 Britta Simon 指派給 Optimizely，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0a5b1-218">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="0a5b1-219">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0a5b1-221">在應用程式清單中，選取 [Optimizely] 。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-221">In the applications list, select **Optimizely**.</span></span>

    ![設定單一登入](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="0a5b1-223">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-223">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0a5b1-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-225">Click **Add** button.</span></span> <span data-ttu-id="0a5b1-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0a5b1-228">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a5b1-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a5b1-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a5b1-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0a5b1-231">Testing single sign-on</span></span>

<span data-ttu-id="0a5b1-232">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0a5b1-233">當您在存取面板中按一下 Optimizely 磚時，應該會自動登入 Optimizely 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a5b1-233">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0a5b1-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="0a5b1-234">Additional resources</span></span>

* [<span data-ttu-id="0a5b1-235">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="0a5b1-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a5b1-236">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0a5b1-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

