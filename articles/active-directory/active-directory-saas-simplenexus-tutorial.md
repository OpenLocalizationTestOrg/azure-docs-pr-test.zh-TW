---
title: "教學課程：Azure Active Directory 與 SimpleNexus 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SimpleNexus 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bddd82b986039cf67827cb407f500edb2000964b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="78f7a-103">教學課程：Azure Active Directory 與 SimpleNexus 整合</span><span class="sxs-lookup"><span data-stu-id="78f7a-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>

<span data-ttu-id="78f7a-104">在本教學課程中，您將了解如何整合 SimpleNexus 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="78f7a-104">In this tutorial, you learn how to integrate SimpleNexus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="78f7a-105">SimpleNexus 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="78f7a-105">Integrating SimpleNexus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="78f7a-106">您可以在 Azure AD 中控制可存取 SimpleNexus 的人員</span><span class="sxs-lookup"><span data-stu-id="78f7a-106">You can control in Azure AD who has access to SimpleNexus</span></span>
- <span data-ttu-id="78f7a-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SimpleNexus (單一登入)</span><span class="sxs-lookup"><span data-stu-id="78f7a-107">You can enable your users to automatically get signed-on to SimpleNexus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="78f7a-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="78f7a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="78f7a-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="78f7a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78f7a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="78f7a-110">Prerequisites</span></span>

<span data-ttu-id="78f7a-111">若要設定 Azure AD 與 SimpleNexus 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="78f7a-111">To configure Azure AD integration with SimpleNexus, you need the following items:</span></span>

- <span data-ttu-id="78f7a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="78f7a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="78f7a-113">啟用 SimpleNexus 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="78f7a-113">A SimpleNexus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="78f7a-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="78f7a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="78f7a-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="78f7a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="78f7a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="78f7a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="78f7a-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="78f7a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="78f7a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="78f7a-118">Scenario description</span></span>
<span data-ttu-id="78f7a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78f7a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="78f7a-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="78f7a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="78f7a-121">從資源庫新增 SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="78f7a-121">Adding SimpleNexus from the gallery</span></span>
2. <span data-ttu-id="78f7a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="78f7a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-simplenexus-from-the-gallery"></a><span data-ttu-id="78f7a-123">從資源庫新增 SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="78f7a-123">Adding SimpleNexus from the gallery</span></span>
<span data-ttu-id="78f7a-124">若要設定將 SimpleNexus 整合到 Azure AD 中，您需要從資源庫將 SimpleNexus 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="78f7a-124">To configure the integration of SimpleNexus into Azure AD, you need to add SimpleNexus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="78f7a-125">**若要從資源庫新增 SimpleNexus，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="78f7a-125">**To add SimpleNexus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="78f7a-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="78f7a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="78f7a-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="78f7a-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="78f7a-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="78f7a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="78f7a-133">在搜尋方塊中，輸入 **SimpleNexus**。</span><span class="sxs-lookup"><span data-stu-id="78f7a-133">In the search box, type **SimpleNexus**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_search.png)

5. <span data-ttu-id="78f7a-135">在結果窗格中，選取 [SimpleNexus]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="78f7a-135">In the results panel, select **SimpleNexus**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="78f7a-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="78f7a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="78f7a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 SimpleNexus 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78f7a-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="78f7a-139">若要讓單一登入能夠運作，Azure AD 必須知道 SimpleNexus 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="78f7a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SimpleNexus is to a user in Azure AD.</span></span> <span data-ttu-id="78f7a-140">換句話說，必須在 Azure AD 使用者和 SimpleNexus 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="78f7a-140">In other words, a link relationship between an Azure AD user and the related user in SimpleNexus needs to be established.</span></span>

<span data-ttu-id="78f7a-141">在 SimpleNexus 中，將 Azure AD 中 [使用者名稱]的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="78f7a-141">In SimpleNexus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="78f7a-142">若要使用 SimpleNexus 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="78f7a-142">To configure and test Azure AD single sign-on with SimpleNexus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="78f7a-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="78f7a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="78f7a-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78f7a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="78f7a-145">**[建立 SimpleNexus 測試使用者](#creating-a-simplenexus-test-user)** - 使 SimpleNexus 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="78f7a-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - to have a counterpart of Britta Simon in SimpleNexus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="78f7a-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78f7a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="78f7a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="78f7a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="78f7a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="78f7a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="78f7a-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 SimpleNexus 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="78f7a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SimpleNexus application.</span></span>

<span data-ttu-id="78f7a-150">**若要使用 SimpleNexus 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="78f7a-150">**To configure Azure AD single sign-on with SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="78f7a-151">在 Azure 入口網站的 [SimpleNexus] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-151">In the Azure portal, on the **SimpleNexus** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="78f7a-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="78f7a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_samlbase.png)

3. <span data-ttu-id="78f7a-155">在 [SimpleNexus 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="78f7a-155">On the **SimpleNexus Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_url.png)

    <span data-ttu-id="78f7a-157">a.</span><span class="sxs-lookup"><span data-stu-id="78f7a-157">a.</span></span> <span data-ttu-id="78f7a-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://simplenexus.com/<companyname>_login`</span><span class="sxs-lookup"><span data-stu-id="78f7a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>_login`</span></span>

    <span data-ttu-id="78f7a-159">b.</span><span class="sxs-lookup"><span data-stu-id="78f7a-159">b.</span></span> <span data-ttu-id="78f7a-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://simplenexus.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="78f7a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="78f7a-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="78f7a-161">These values are not real.</span></span> <span data-ttu-id="78f7a-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="78f7a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="78f7a-163">請連絡 [SimpleNexus 客戶支援小組](https://simplenexus.com/site/contact)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="78f7a-163">Contact [SimpleNexus Client support team](https://simplenexus.com/site/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="78f7a-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="78f7a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_certificate.png) 

5. <span data-ttu-id="78f7a-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="78f7a-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-simplenexus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="78f7a-168">若要在 **SimpleNexus** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [SimpleNexus 支援小組](https://simplenexus.com/site/contact)。</span><span class="sxs-lookup"><span data-stu-id="78f7a-168">To configure single sign-on on **SimpleNexus** side, you need to send the downloaded **Metadata XML** to [SimpleNexus support team](https://simplenexus.com/site/contact).</span></span> <span data-ttu-id="78f7a-169">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="78f7a-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="78f7a-170">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="78f7a-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="78f7a-171">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="78f7a-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="78f7a-172">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="78f7a-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="78f7a-173">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="78f7a-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="78f7a-174">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="78f7a-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="78f7a-176">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="78f7a-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="78f7a-177">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="78f7a-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="78f7a-179">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="78f7a-181">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="78f7a-183">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="78f7a-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="78f7a-185">a.</span><span class="sxs-lookup"><span data-stu-id="78f7a-185">a.</span></span> <span data-ttu-id="78f7a-186">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="78f7a-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="78f7a-187">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="78f7a-187">b.</span></span> <span data-ttu-id="78f7a-188">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="78f7a-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="78f7a-189">c.</span><span class="sxs-lookup"><span data-stu-id="78f7a-189">c.</span></span> <span data-ttu-id="78f7a-190">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="78f7a-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="78f7a-191">d.</span><span class="sxs-lookup"><span data-stu-id="78f7a-191">d.</span></span> <span data-ttu-id="78f7a-192">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="78f7a-192">Click **Create**.</span></span>
 
### <a name="creating-a-simplenexus-test-user"></a><span data-ttu-id="78f7a-193">建立 SimpleNexus 測試使用者</span><span class="sxs-lookup"><span data-stu-id="78f7a-193">Creating a SimpleNexus test user</span></span>

<span data-ttu-id="78f7a-194">若要讓 Azure AD 使用者能夠登入 SimpleNexus，必須將他們佈建到 SimpleNexus。</span><span class="sxs-lookup"><span data-stu-id="78f7a-194">In order to enable Azure AD users to log in to SimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="78f7a-195">SimpleNexus 須由租用戶系統管理員手動執行佈建工作。</span><span class="sxs-lookup"><span data-stu-id="78f7a-195">In the case of SimpleNexus, provisioning is a manual task performed by the tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="78f7a-196">您可以使用任何其他的 SimpleNexus 使用者帳戶建立工具或 SimpleNexus 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="78f7a-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="78f7a-197">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="78f7a-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="78f7a-198">在本節中，您會將 SimpleNexus 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="78f7a-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SimpleNexus.</span></span>

![指派使用者][200] 

<span data-ttu-id="78f7a-200">**若要將 Britta Simon 指派給 SimpleNexus，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="78f7a-200">**To assign Britta Simon to SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="78f7a-201">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="78f7a-203">在應用程式清單中，選取 [SimpleNexus]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-203">In the applications list, select **SimpleNexus**.</span></span>

    ![設定單一登入](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_app.png) 

3. <span data-ttu-id="78f7a-205">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-205">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="78f7a-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="78f7a-207">Click **Add** button.</span></span> <span data-ttu-id="78f7a-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="78f7a-210">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="78f7a-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="78f7a-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="78f7a-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="78f7a-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="78f7a-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="78f7a-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="78f7a-213">Testing single sign-on</span></span>

<span data-ttu-id="78f7a-214">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="78f7a-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="78f7a-215">當您在存取面板中按一下 [SimpleNexus] 圖格時，應該會自動登入您的 SimpleNexus 應用程式。</span><span class="sxs-lookup"><span data-stu-id="78f7a-215">When you click the SimpleNexus tile in the Access Panel, you should get automatically signed-on to your SimpleNexus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="78f7a-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="78f7a-216">Additional resources</span></span>

* [<span data-ttu-id="78f7a-217">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="78f7a-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="78f7a-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="78f7a-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_203.png

