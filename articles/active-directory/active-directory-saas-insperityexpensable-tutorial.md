---
title: "教學課程：Azure Active Directory 與 Insperity ExpensAble 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Insperity ExpensAble 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: b50e10be54b1fc413be10bee5b58631790629335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="9ebd4-103">教學課程：Azure Active Directory 與 Insperity ExpensAble 整合</span><span class="sxs-lookup"><span data-stu-id="9ebd4-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="9ebd4-104">在本教學課程中，您將了解如何整合 Insperity ExpensAble 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-104">In this tutorial, you learn how to integrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ebd4-105">Insperity ExpensAble 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="9ebd4-105">Integrating Insperity ExpensAble with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9ebd4-106">您可以在 Azure AD 中控制可存取 Insperity ExpensAble 的人員</span><span class="sxs-lookup"><span data-stu-id="9ebd4-106">You can control in Azure AD who has access to Insperity ExpensAble</span></span>
- <span data-ttu-id="9ebd4-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Insperity ExpensAble (單一登入)</span><span class="sxs-lookup"><span data-stu-id="9ebd4-107">You can enable your users to automatically get signed-on to Insperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9ebd4-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="9ebd4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9ebd4-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ebd4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9ebd4-110">Prerequisites</span></span>

<span data-ttu-id="9ebd4-111">若要設定 Azure AD 與 Insperity ExpensAble 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="9ebd4-111">To configure Azure AD integration with Insperity ExpensAble, you need the following items:</span></span>

- <span data-ttu-id="9ebd4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9ebd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9ebd4-113">啟用 Insperity ExpensAble 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9ebd4-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9ebd4-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9ebd4-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9ebd4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9ebd4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9ebd4-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ebd4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9ebd4-118">Scenario description</span></span>
<span data-ttu-id="9ebd4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ebd4-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="9ebd4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ebd4-121">從資源庫新增 Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="9ebd4-121">Adding Insperity ExpensAble from the gallery</span></span>
2. <span data-ttu-id="9ebd4-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9ebd4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-the-gallery"></a><span data-ttu-id="9ebd4-123">從資源庫新增 Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="9ebd4-123">Adding Insperity ExpensAble from the gallery</span></span>
<span data-ttu-id="9ebd4-124">若要設定將 Insperity ExpensAble 整合到 Azure AD 中，您需要從資源庫將 Insperity ExpensAble 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-124">To configure the integration of Insperity ExpensAble into Azure AD, you need to add Insperity ExpensAble from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9ebd4-125">**若要從資源庫新增 Insperity ExpensAble，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9ebd4-125">**To add Insperity ExpensAble from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9ebd4-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9ebd4-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9ebd4-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="9ebd4-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="9ebd4-133">在搜尋方塊中，輸入 **Insperity ExpensAble**。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-133">In the search box, type **Insperity ExpensAble**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="9ebd4-135">在結果窗格中，選取 [Insperity ExpensAble]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-135">In the results panel, select **Insperity ExpensAble**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9ebd4-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9ebd4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9ebd4-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Insperity ExpensAble 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ebd4-139">若要讓單一登入運作，Azure AD 必須知道 Insperity ExpensAble 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Insperity ExpensAble is to a user in Azure AD.</span></span> <span data-ttu-id="9ebd4-140">換句話說，必須在 Azure AD 使用者和 Insperity ExpensAble 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-140">In other words, a link relationship between an Azure AD user and the related user in Insperity ExpensAble needs to be established.</span></span>

<span data-ttu-id="9ebd4-141">在 Insperity ExpensAble 中，將 [使用者名稱] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-141">In Insperity ExpensAble, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9ebd4-142">若要設定及測試與 Insperity ExpensAble 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="9ebd4-142">To configure and test Azure AD single sign-on with Insperity ExpensAble, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9ebd4-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9ebd4-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ebd4-145">**[建立 Insperity ExpensAble 測試使用者](#creating-an-insperity-expensable-test-user)** - 使 Insperity ExpensAble 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - to have a counterpart of Britta Simon in Insperity ExpensAble that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ebd4-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ebd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9ebd4-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9ebd4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9ebd4-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Insperity ExpensAble 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="9ebd4-150">**若要使用 Insperity ExpensAble 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9ebd4-150">**To configure Azure AD single sign-on with Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="9ebd4-151">在 Azure 入口網站的 [Insperity ExpensAble] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-151">In the Azure portal, on the **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9ebd4-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="9ebd4-155">在 [Insperity ExpensAble 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9ebd4-155">On the **Insperity ExpensAble Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="9ebd4-157">a.</span><span class="sxs-lookup"><span data-stu-id="9ebd4-157">a.</span></span> <span data-ttu-id="9ebd4-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="9ebd4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9ebd4-159">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-159">This value is not real.</span></span> <span data-ttu-id="9ebd4-160">使用實際的登入 URL 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="9ebd4-161">請連絡 [Insperity ExpensAble 用戶端支援小組](http://expensable.com/support/support-overview)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) to get this value.</span></span> 
 
4. <span data-ttu-id="9ebd4-162">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="9ebd4-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-164">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9ebd4-166">在 [Insperity ExpensAble 組態] 區段中，按一下 [設定 Insperity ExpensAble] 開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-166">On the **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9ebd4-167">從 [快速參考] 區段中複製 **SAML 實體識別碼和 SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-167">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="9ebd4-169">若要在 **Insperity ExpensAble** 這一端設定單一登入，您需要將所下載的**「中繼資料 XML」**、**「SAML 單一登入服務 URL」**和**「SAML 實體識別碼」**傳送給 [Insperity ExpensAble 支援小組](http://expensable.com/support/support-overview)。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-169">To configure single sign-on on **Insperity ExpensAble** side, you need to send the downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="9ebd4-170">他們會進行此設定，讓兩端的 SAML SSO 連線都設定正確。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="9ebd4-171">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="9ebd4-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9ebd4-172">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9ebd4-173">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9ebd4-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9ebd4-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9ebd4-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="9ebd4-175">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="9ebd4-177">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="9ebd4-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9ebd4-178">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ebd4-180">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ebd4-182">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ebd4-184">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9ebd4-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ebd4-186">a.</span><span class="sxs-lookup"><span data-stu-id="9ebd4-186">a.</span></span> <span data-ttu-id="9ebd4-187">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ebd4-188">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-188">b.</span></span> <span data-ttu-id="9ebd4-189">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ebd4-190">c.</span><span class="sxs-lookup"><span data-stu-id="9ebd4-190">c.</span></span> <span data-ttu-id="9ebd4-191">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9ebd4-192">d.</span><span class="sxs-lookup"><span data-stu-id="9ebd4-192">d.</span></span> <span data-ttu-id="9ebd4-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="9ebd4-194">建立 Insperity ExpensAble 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9ebd4-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="9ebd4-195">本節的目標是在 Insperity ExpensAble 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-195">The objective of this section is to create a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="9ebd4-196">請與 [Insperity ExpensAble 支援小組](http://expensable.com/support/support-overview)合作，在 Insperity ExpensAble 帳戶中加入使用者。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) to add the users in the Insperity ExpensAble account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9ebd4-197">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9ebd4-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9ebd4-198">在本節中，您會把 Insperity ExpensAble 的存取權授予 Britta Simon，讓 Britta Simon 能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Insperity ExpensAble.</span></span>

![指派使用者][200] 

<span data-ttu-id="9ebd4-200">**若要將 Britta Simon 指派到 Insperity ExpensAble，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="9ebd4-200">**To assign Britta Simon to Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="9ebd4-201">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9ebd4-203">在應用程式清單中，選取 [Insperity ExpensAble] 。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-203">In the applications list, select **Insperity ExpensAble**.</span></span>

    ![設定單一登入](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="9ebd4-205">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-205">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="9ebd4-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-207">Click **Add** button.</span></span> <span data-ttu-id="9ebd4-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="9ebd4-210">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9ebd4-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9ebd4-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9ebd4-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9ebd4-213">Testing single sign-on</span></span>

<span data-ttu-id="9ebd4-214">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9ebd4-215">當您在存取面板中按一下 [Insperity ExpensAble] 圖格時，應該會自動登入您的 Insperity ExpensAble 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-215">When you click the Insperity ExpensAble tile in the Access Panel, you should get automatically signed-on to your Insperity ExpensAble application.</span></span>
<span data-ttu-id="9ebd4-216">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="9ebd4-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ebd4-217">其他資源</span><span class="sxs-lookup"><span data-stu-id="9ebd4-217">Additional resources</span></span>

* [<span data-ttu-id="9ebd4-218">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="9ebd4-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ebd4-219">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9ebd4-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

