---
title: "教學課程：Azure Active Directory 與 Veritas Enterprise Vault.cloud SSO 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Veritas Enterprise Vault.cloud SSO 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 1f8c7fd97021f320a23bc78466a7b61f2d7e513e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veritas-enterprise-vaultcloud-sso"></a><span data-ttu-id="ff4a8-103">教學課程：Azure Active Directory 與 Veritas Enterprise Vault.cloud SSO 整合</span><span class="sxs-lookup"><span data-stu-id="ff4a8-103">Tutorial: Azure Active Directory integration with Veritas Enterprise Vault.cloud SSO</span></span>

<span data-ttu-id="ff4a8-104">在本教學課程中，您會了解如何整合 Veritas Enterprise Vault.cloud SSO 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-104">In this tutorial, you learn how to integrate Veritas Enterprise Vault.cloud SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff4a8-105">Veritas Enterprise Vault.cloud SSO 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ff4a8-105">Integrating Veritas Enterprise Vault.cloud SSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ff4a8-106">您可以在 Azure AD 中控制可存取 Veritas Enterprise Vault.cloud SSO 的人員</span><span class="sxs-lookup"><span data-stu-id="ff4a8-106">You can control in Azure AD who has access to Veritas Enterprise Vault.cloud SSO</span></span>
- <span data-ttu-id="ff4a8-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Veritas Enterprise Vault.cloud SSO (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ff4a8-107">You can enable your users to automatically get signed-on to Veritas Enterprise Vault.cloud SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff4a8-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ff4a8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ff4a8-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff4a8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ff4a8-110">Prerequisites</span></span>

<span data-ttu-id="ff4a8-111">若要設定 Azure AD 與 Veritas Enterprise Vault.cloud SSO 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ff4a8-111">To configure Azure AD integration with Veritas Enterprise Vault.cloud SSO, you need the following items:</span></span>

- <span data-ttu-id="ff4a8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ff4a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff4a8-113">已啟用 Veritas Enterprise Vault.cloud SSO 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ff4a8-113">A Veritas Enterprise Vault.cloud SSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff4a8-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff4a8-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ff4a8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff4a8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff4a8-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff4a8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ff4a8-118">Scenario description</span></span>
<span data-ttu-id="ff4a8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff4a8-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ff4a8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff4a8-121">從資源庫新增 Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="ff4a8-121">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span></span>
2. <span data-ttu-id="ff4a8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ff4a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-veritas-enterprise-vaultcloud-sso-from-the-gallery"></a><span data-ttu-id="ff4a8-123">從資源庫新增 Veritas Enterprise Vault.cloud SSO</span><span class="sxs-lookup"><span data-stu-id="ff4a8-123">Adding Veritas Enterprise Vault.cloud SSO from the gallery</span></span>
<span data-ttu-id="ff4a8-124">若要設定 Veritas Enterprise Vault.cloud SSO 與 Azure AD 的整合，您需要從資源庫將 Veritas Enterprise Vault.cloud SSO 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-124">To configure the integration of Veritas Enterprise Vault.cloud SSO into Azure AD, you need to add Veritas Enterprise Vault.cloud SSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff4a8-125">**若要從資源庫新增 Veritas Enterprise Vault.cloud SSO，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ff4a8-125">**To add Veritas Enterprise Vault.cloud SSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff4a8-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ff4a8-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff4a8-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ff4a8-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ff4a8-133">在搜尋方塊中，輸入 **Veritas Enterprise Vault.cloud SSO**。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-133">In the search box, type **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_search.png)

5. <span data-ttu-id="ff4a8-135">在結果窗格中，選取 [Veritas Enterprise Vault.cloud SSO]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-135">In the results panel, select **Veritas Enterprise Vault.cloud SSO**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff4a8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ff4a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff4a8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Veritas Enterprise Vault.cloud SSO 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-138">In this section, you configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff4a8-139">若要讓單一登入運作，Azure AD 必須知道 Veritas Enterprise Vault.cloud SSO 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Veritas Enterprise Vault.cloud SSO is to a user in Azure AD.</span></span> <span data-ttu-id="ff4a8-140">換句話說，必須建立 Azure AD 使用者和 Veritas Enterprise Vault.cloud SSO 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-140">In other words, a link relationship between an Azure AD user and the related user in Veritas Enterprise Vault.cloud SSO needs to be established.</span></span>

<span data-ttu-id="ff4a8-141">在 Veritas Enterprise Vault.cloud SSO 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-141">In Veritas Enterprise Vault.cloud SSO, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ff4a8-142">若要設定及測試與 Veritas Enterprise Vault.cloud SSO 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="ff4a8-142">To configure and test Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff4a8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff4a8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff4a8-145">**[建立 Veritas Enterprise Vault.cloud SSO 測試使用者](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)** - 使 Veritas Enterprise Vault.cloud SSO 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-145">**[Creating a Veritas Enterprise Vault.cloud SSO test user](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)** - to have a counterpart of Britta Simon in Veritas Enterprise Vault.cloud SSO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ff4a8-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff4a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff4a8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ff4a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff4a8-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Veritas Enterprise Vault.cloud SSO 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Veritas Enterprise Vault.cloud SSO application.</span></span>

<span data-ttu-id="ff4a8-150">**若要使用 Veritas Enterprise Vault.cloud SSO 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ff4a8-150">**To configure Azure AD single sign-on with Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="ff4a8-151">在 Azure 入口網站的 [Veritas Enterprise Vault.cloud SSO] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-151">In the Azure portal, on the **Veritas Enterprise Vault.cloud SSO** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ff4a8-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_samlbase.png)

3. <span data-ttu-id="ff4a8-155">在 [Veritas Enterprise Vault.cloud SSO 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ff4a8-155">On the **Veritas Enterprise Vault.cloud SSO Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_url.png)

    <span data-ttu-id="ff4a8-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span><span class="sxs-lookup"><span data-stu-id="ff4a8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ff4a8-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-158">This value is not real.</span></span> <span data-ttu-id="ff4a8-159">請使用實際的登入 URL 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ff4a8-160">請連絡 [Veritas Enterprise Vault.cloud SSO 客戶支援小組](https://www.veritas.com/support/.html)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-160">Contact [Veritas Enterprise Vault.cloud SSO Client support team](https://www.veritas.com/support/.html) to get this value.</span></span> 

4. <span data-ttu-id="ff4a8-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_certificate.png) 

5. <span data-ttu-id="ff4a8-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-veritas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ff4a8-165">在 [Veritas Enterprise Vault.cloud SSO 組態] 區段中，按一下 [設定 Veritas Enterprise Vault.cloud SSO ] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-165">On the **Veritas Enterprise Vault.cloud SSO Configuration** section, click **Configure Veritas Enterprise Vault.cloud SSO** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ff4a8-166">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_configure.png) 

7. <span data-ttu-id="ff4a8-168">若要在 **Veritas Enterprise Vault.cloud SSO** 端設定單一登入，您必須將已下載的**憑證(Base64)** 和 **SAML 單一登入服務 URL** 傳送給 [Veritas Enterprise Vault.cloud SSO 支援小組](https://www.veritas.com/support/.html)。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-168">To configure single sign-on on **Veritas Enterprise Vault.cloud SSO** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html).</span></span>

> [!TIP]
> <span data-ttu-id="ff4a8-169">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ff4a8-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ff4a8-170">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ff4a8-171">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ff4a8-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff4a8-172">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ff4a8-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff4a8-173">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ff4a8-175">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ff4a8-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff4a8-176">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-veritas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff4a8-178">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-veritas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff4a8-180">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-veritas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff4a8-182">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ff4a8-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-veritas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff4a8-184">a.</span><span class="sxs-lookup"><span data-stu-id="ff4a8-184">a.</span></span> <span data-ttu-id="ff4a8-185">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff4a8-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-186">b.</span></span> <span data-ttu-id="ff4a8-187">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff4a8-188">c.</span><span class="sxs-lookup"><span data-stu-id="ff4a8-188">c.</span></span> <span data-ttu-id="ff4a8-189">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ff4a8-190">d.</span><span class="sxs-lookup"><span data-stu-id="ff4a8-190">d.</span></span> <span data-ttu-id="ff4a8-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-191">Click **Create**.</span></span>
 
### <a name="creating-a-veritas-enterprise-vaultcloud-sso-test-user"></a><span data-ttu-id="ff4a8-192">建立 Veritas Enterprise Vault.cloud SSO 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ff4a8-192">Creating a Veritas Enterprise Vault.cloud SSO test user</span></span>

<span data-ttu-id="ff4a8-193">在本節中，您要在 Enterprise Vault.cloud SSO 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-193">In this section, you create a user called Britta Simon in Enterprise Vault.cloud SSO.</span></span> <span data-ttu-id="ff4a8-194">請與 [Veritas Enterprise Vault.cloud SSO 支援小組](https://www.veritas.com/support/.html)合作，以將使用者新增到 Enterprise Vault.cloud SSO 平台。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-194">Work with [Veritas Enterprise Vault.cloud SSO support team](https://www.veritas.com/support/.html) to add the users in the Enterprise Vault.cloud SSO platform.</span></span> <span data-ttu-id="ff4a8-195">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-195">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff4a8-196">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ff4a8-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ff4a8-197">在本節中，您會將 Veritas Enterprise Vault.cloud SSO 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Veritas Enterprise Vault.cloud SSO.</span></span>

![指派使用者][200] 

<span data-ttu-id="ff4a8-199">**若要將 Britta Simon 指派給 Veritas Enterprise Vault.cloud SSO，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ff4a8-199">**To assign Britta Simon to Veritas Enterprise Vault.cloud SSO, perform the following steps:**</span></span>

1. <span data-ttu-id="ff4a8-200">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ff4a8-202">在應用程式清單中，選取 [Veritas Enterprise Vault.cloud SSO]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-202">In the applications list, select **Veritas Enterprise Vault.cloud SSO**.</span></span>

    ![設定單一登入](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_app.png) 

3. <span data-ttu-id="ff4a8-204">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-204">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ff4a8-206">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-206">Click **Add** button.</span></span> <span data-ttu-id="ff4a8-207">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ff4a8-209">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ff4a8-210">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff4a8-211">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ff4a8-212">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ff4a8-212">Testing single sign-on</span></span>

<span data-ttu-id="ff4a8-213">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ff4a8-214">當您在 [存取面板] 中按一下 [Veritas Enterprise Vault.cloud SSO] 圖格時，應該會自動登入您的 Veritas Enterprise Vault.cloud SSO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff4a8-214">When you click the Veritas Enterprise Vault.cloud SSO tile in the Access Panel, you should get automatically signed-on to your Veritas Enterprise Vault.cloud SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff4a8-215">其他資源</span><span class="sxs-lookup"><span data-stu-id="ff4a8-215">Additional resources</span></span>

* [<span data-ttu-id="ff4a8-216">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ff4a8-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff4a8-217">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ff4a8-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_203.png

