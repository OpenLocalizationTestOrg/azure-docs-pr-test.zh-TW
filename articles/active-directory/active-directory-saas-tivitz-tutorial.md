---
title: "教學課程：Azure Active Directory 與 TiViTz 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 TiViTz 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b97ed88f-7888-4185-be22-41d1f62cbbf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: b1b27918bb5fcff1d19f4711ea70fe46a5697933
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tivitz"></a><span data-ttu-id="75fdf-103">教學課程：Azure Active Directory 與 TiViTz 整合</span><span class="sxs-lookup"><span data-stu-id="75fdf-103">Tutorial: Azure Active Directory integration with TiViTz</span></span>

<span data-ttu-id="75fdf-104">在本教學課程中，您將了解如何整合 TiViTz 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="75fdf-104">In this tutorial, you learn how to integrate TiViTz with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="75fdf-105">TiViTz 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="75fdf-105">Integrating TiViTz with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="75fdf-106">您可以在 Azure AD 中控制可存取 TiViTz 的人員</span><span class="sxs-lookup"><span data-stu-id="75fdf-106">You can control in Azure AD who has access to TiViTz</span></span>
- <span data-ttu-id="75fdf-107">您可以讓使用者利用 Azure AD 帳戶來自動登入 TiViTz (單一登入)</span><span class="sxs-lookup"><span data-stu-id="75fdf-107">You can enable your users to automatically get signed-on to TiViTz (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="75fdf-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="75fdf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="75fdf-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="75fdf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75fdf-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="75fdf-110">Prerequisites</span></span>

<span data-ttu-id="75fdf-111">若要設定 Azure AD 與 TiViTz 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="75fdf-111">To configure Azure AD integration with TiViTz, you need the following items:</span></span>

- <span data-ttu-id="75fdf-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="75fdf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="75fdf-113">已啟用 TiViTz 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="75fdf-113">A TiViTz single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="75fdf-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="75fdf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="75fdf-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="75fdf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="75fdf-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="75fdf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="75fdf-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="75fdf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="75fdf-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="75fdf-118">Scenario description</span></span>
<span data-ttu-id="75fdf-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="75fdf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="75fdf-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="75fdf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="75fdf-121">從資源庫新增 TiViTz</span><span class="sxs-lookup"><span data-stu-id="75fdf-121">Adding TiViTz from the gallery</span></span>
2. <span data-ttu-id="75fdf-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="75fdf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tivitz-from-the-gallery"></a><span data-ttu-id="75fdf-123">從資源庫新增 TiViTz</span><span class="sxs-lookup"><span data-stu-id="75fdf-123">Adding TiViTz from the gallery</span></span>
<span data-ttu-id="75fdf-124">若要設定 TiViTz 與 Azure AD 的整合，您需要從資源庫將 TiViTz 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="75fdf-124">To configure the integration of TiViTz into Azure AD, you need to add TiViTz from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="75fdf-125">**若要從資源庫新增 TiViTz，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="75fdf-125">**To add TiViTz from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="75fdf-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="75fdf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="75fdf-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="75fdf-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="75fdf-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="75fdf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="75fdf-133">在搜尋方塊中，輸入 **TiViTz**。</span><span class="sxs-lookup"><span data-stu-id="75fdf-133">In the search box, type **TiViTz**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_search.png)

5. <span data-ttu-id="75fdf-135">在結果窗格中，選取 [TiViTz]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fdf-135">In the results panel, select **TiViTz**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="75fdf-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="75fdf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="75fdf-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 TiViTz 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="75fdf-138">In this section, you configure and test Azure AD single sign-on with TiViTz based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="75fdf-139">若要讓單一登入能夠運作，Azure AD 必須知道 TiViTz 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="75fdf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TiViTz is to a user in Azure AD.</span></span> <span data-ttu-id="75fdf-140">換句話說，必須在 Azure AD 使用者和 TiViTz 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="75fdf-140">In other words, a link relationship between an Azure AD user and the related user in TiViTz needs to be established.</span></span>

<span data-ttu-id="75fdf-141">在 TiViTz 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="75fdf-141">In TiViTz, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="75fdf-142">若要設定及測試與 TiViTz 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="75fdf-142">To configure and test Azure AD single sign-on with TiViTz, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="75fdf-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="75fdf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="75fdf-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="75fdf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="75fdf-145">**[建立 TiViTz 測試使用者](#creating-a-tivitz-test-user)** - 在 TiViTz 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="75fdf-145">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - to have a counterpart of Britta Simon in TiViTz that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="75fdf-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="75fdf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="75fdf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="75fdf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="75fdf-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="75fdf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="75fdf-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 TiViTz 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="75fdf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TiViTz application.</span></span>

<span data-ttu-id="75fdf-150">**若要使用 TiViTz 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="75fdf-150">**To configure Azure AD single sign-on with TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="75fdf-151">在 Azure 入口網站的 [TiViTz] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-151">In the Azure portal, on the **TiViTz** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="75fdf-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="75fdf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_samlbase.png)

3. <span data-ttu-id="75fdf-155">在 [TiViTz 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="75fdf-155">On the **TiViTz Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_url.png)

    <span data-ttu-id="75fdf-157">a.</span><span class="sxs-lookup"><span data-stu-id="75fdf-157">a.</span></span> <span data-ttu-id="75fdf-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="75fdf-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    <span data-ttu-id="75fdf-159">b.</span><span class="sxs-lookup"><span data-stu-id="75fdf-159">b.</span></span> <span data-ttu-id="75fdf-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="75fdf-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="75fdf-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="75fdf-161">These values are not real.</span></span> <span data-ttu-id="75fdf-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="75fdf-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="75fdf-163">請連絡 [TiViTz 客戶支援小組](mailto:info@tivitz.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="75fdf-163">Contact [TiViTz Client support team](mailto:info@tivitz.com) to get these values.</span></span> 

4. <span data-ttu-id="75fdf-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="75fdf-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_certificate.png) 

5. <span data-ttu-id="75fdf-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="75fdf-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-tivitz-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="75fdf-168">若要在 **TiViTz** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [TiViTz 支援小組](mailto:info@tivitz.com)。</span><span class="sxs-lookup"><span data-stu-id="75fdf-168">To configure single sign-on on **TiViTz** side, you need to send the downloaded **Metadata XML** to [TiViTz support team](mailto:info@tivitz.com).</span></span>

> [!TIP]
> <span data-ttu-id="75fdf-169">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="75fdf-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="75fdf-170">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="75fdf-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="75fdf-171">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="75fdf-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="75fdf-172">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="75fdf-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="75fdf-173">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="75fdf-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="75fdf-175">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="75fdf-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="75fdf-176">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="75fdf-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tivitz-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="75fdf-178">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tivitz-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="75fdf-180">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tivitz-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="75fdf-182">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="75fdf-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tivitz-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="75fdf-184">a.</span><span class="sxs-lookup"><span data-stu-id="75fdf-184">a.</span></span> <span data-ttu-id="75fdf-185">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="75fdf-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="75fdf-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fdf-186">b.</span></span> <span data-ttu-id="75fdf-187">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="75fdf-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="75fdf-188">c.</span><span class="sxs-lookup"><span data-stu-id="75fdf-188">c.</span></span> <span data-ttu-id="75fdf-189">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="75fdf-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="75fdf-190">d.</span><span class="sxs-lookup"><span data-stu-id="75fdf-190">d.</span></span> <span data-ttu-id="75fdf-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="75fdf-191">Click **Create**.</span></span>
 
### <a name="creating-a-tivitz-test-user"></a><span data-ttu-id="75fdf-192">建立 TiViTz 測試使用者</span><span class="sxs-lookup"><span data-stu-id="75fdf-192">Creating a TiViTz test user</span></span>

<span data-ttu-id="75fdf-193">本節目標是在 TiViTz 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="75fdf-193">The objective of this section is to create a user called Britta Simon in TiViTz.</span></span> <span data-ttu-id="75fdf-194">TiViTz 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="75fdf-194">TiViTz supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="75fdf-195">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="75fdf-195">There is no action item for you in this section.</span></span> <span data-ttu-id="75fdf-196">當您嘗試存取 TiViTz 時，如果 TiViTz 還沒有使用者，它就會建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="75fdf-196">A new user is created during an attempt to access TiViTz if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="75fdf-197">如果您需要手動建立使用者，就必須連絡 [TiViTz 支援小組](mailto:info@tivitz.com)。</span><span class="sxs-lookup"><span data-stu-id="75fdf-197">If you need to create an user manually, you need to contact [TiViTz support team](mailto:info@tivitz.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="75fdf-198">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="75fdf-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="75fdf-199">在本節中，您會將 TiViTz 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="75fdf-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TiViTz.</span></span>

![指派使用者][200] 

<span data-ttu-id="75fdf-201">**若要將 Britta Simon 指派到 TiViTz，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="75fdf-201">**To assign Britta Simon to TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="75fdf-202">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="75fdf-204">在應用程式清單中，選取 [TiViTz]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-204">In the applications list, select **TiViTz**.</span></span>

    ![設定單一登入](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_app.png) 

3. <span data-ttu-id="75fdf-206">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-206">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="75fdf-208">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="75fdf-208">Click **Add** button.</span></span> <span data-ttu-id="75fdf-209">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="75fdf-211">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="75fdf-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="75fdf-212">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="75fdf-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="75fdf-213">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="75fdf-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="75fdf-214">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="75fdf-214">Testing single sign-on</span></span>

<span data-ttu-id="75fdf-215">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="75fdf-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="75fdf-216">當您在存取面板中按一下 TiViTz 圖格時，應該會自動登入您的 TiViTz 應用程式。</span><span class="sxs-lookup"><span data-stu-id="75fdf-216">When you click the TiViTz tile in the Access Panel, you should get automatically signed-on to your TiViTz application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="75fdf-217">其他資源</span><span class="sxs-lookup"><span data-stu-id="75fdf-217">Additional resources</span></span>

* [<span data-ttu-id="75fdf-218">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="75fdf-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="75fdf-219">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="75fdf-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_203.png
