---
title: "教學課程：Azure Active Directory 與 123ContactForm 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 123ContactForm 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3a99f0841c3e0d973168991f5dbee40e54c1d054
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="e5fc5-103">教學課程：Azure Active Directory 與 123ContactForm 整合</span><span class="sxs-lookup"><span data-stu-id="e5fc5-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="e5fc5-104">在本教學課程中，您會了解如何將 123ContactForm 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e5fc5-105">將 123ContactForm 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e5fc5-106">您可以在 Azure AD 中控制可存取 123ContactForm 的人員</span><span class="sxs-lookup"><span data-stu-id="e5fc5-106">You can control in Azure AD who has access to 123ContactForm</span></span>
- <span data-ttu-id="e5fc5-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 123ContactForm (單一登入)</span><span class="sxs-lookup"><span data-stu-id="e5fc5-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e5fc5-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="e5fc5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e5fc5-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5fc5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e5fc5-110">Prerequisites</span></span>

<span data-ttu-id="e5fc5-111">若要設定 Azure AD 與 123ContactForm 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span></span>

- <span data-ttu-id="e5fc5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e5fc5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e5fc5-113">已啟用 123ContactForm 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e5fc5-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e5fc5-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e5fc5-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e5fc5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e5fc5-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e5fc5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e5fc5-118">Scenario description</span></span>
<span data-ttu-id="e5fc5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e5fc5-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e5fc5-121">從資源庫新增 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="e5fc5-121">Adding 123ContactForm from the gallery</span></span>
2. <span data-ttu-id="e5fc5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e5fc5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-the-gallery"></a><span data-ttu-id="e5fc5-123">從資源庫新增 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="e5fc5-123">Adding 123ContactForm from the gallery</span></span>
<span data-ttu-id="e5fc5-124">若要設定將 123ContactForm 整合到 Azure AD 中，您需要從資源庫將 123ContactForm 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e5fc5-125">**若要從資源庫新增 123ContactForm，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e5fc5-125">**To add 123ContactForm from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e5fc5-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e5fc5-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e5fc5-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="e5fc5-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="e5fc5-133">在搜尋方塊中，輸入 **123ContactForm**。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-133">In the search box, type **123ContactForm**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="e5fc5-135">在結果面板中，選取 [123ContactForm]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e5fc5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e5fc5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e5fc5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 123ContactForm 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e5fc5-139">若要讓單一登入能夠運作，Azure AD 必須知道 123ContactForm 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span></span> <span data-ttu-id="e5fc5-140">換句話說，必須在 Azure AD 使用者與 123ContactForm 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span></span>

<span data-ttu-id="e5fc5-141">在 123ContactForm 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e5fc5-142">若要設定及測試與 123ContactForm 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e5fc5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e5fc5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e5fc5-145">**[建立 123ContactForm 測試使用者](#creating-a-123contactform-test-user)** - 在 123ContactForm 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e5fc5-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e5fc5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e5fc5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e5fc5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e5fc5-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 123ContactForm 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="e5fc5-150">**若要設定與 123ContactForm 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e5fc5-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="e5fc5-151">在 Azure 入口網站的 [123ContactForm] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="e5fc5-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="e5fc5-155">如果您想要以「IDP 起始模式」設定應用程式，請在 [123ContactForm 網域及 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="e5fc5-157">a.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-157">a.</span></span> <span data-ttu-id="e5fc5-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="e5fc5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="e5fc5-159">b.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-159">b.</span></span> <span data-ttu-id="e5fc5-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="e5fc5-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="e5fc5-161">如果您想要以「SP 起始模式」起始模式設定應用程式，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="e5fc5-163">a.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-163">a.</span></span> <span data-ttu-id="e5fc5-164">按一下 [顯示進階 URL 設定] 選項</span><span class="sxs-lookup"><span data-stu-id="e5fc5-164">Click the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="e5fc5-165">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-165">b.</span></span> <span data-ttu-id="e5fc5-166">在 [登入 URL] 文字方塊中輸入 URL，例如：`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="e5fc5-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e5fc5-167">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-167">These values are not real.</span></span> <span data-ttu-id="e5fc5-168">您將從實際的 URL 和識別碼更新這些值，本教學課程稍後將會說明。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span></span>
    
5. <span data-ttu-id="e5fc5-169">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="e5fc5-171">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-171">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e5fc5-173">若要在 **123ContactForm** 端設定單一登入，請移至 [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/)，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="e5fc5-175">a.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-175">a.</span></span> <span data-ttu-id="e5fc5-176">在 [電子郵件] 文字方塊中，輸入使用者的電子郵件，亦即</span><span class="sxs-lookup"><span data-stu-id="e5fc5-176">In the **Email** textbox, type the email of the user i.e</span></span> <span data-ttu-id="e5fc5-177">**BrittaSimon@Contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="e5fc5-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-178">b.</span></span> <span data-ttu-id="e5fc5-179">按一下 [上傳]，然後瀏覽您已從 Azure 入口網站下載的「中繼資料 XML」檔案。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="e5fc5-180">c.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-180">c.</span></span> <span data-ttu-id="e5fc5-181">按一下 [送出表單]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="e5fc5-182">在 [Microsoft Azure AD] > [單一登入] > [設定應用程式設定] 上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="e5fc5-184">a.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-184">a.</span></span> <span data-ttu-id="e5fc5-185">如果您想要以「IDP 起始模式」設定應用程式，請複製執行個體的 [識別碼] 值，然後將它貼到 Azure 入口網站上 [123ContactForm 網域及 URL] 區段中的 [識別碼] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="e5fc5-186">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-186">b.</span></span> <span data-ttu-id="e5fc5-187">如果您想要以「IDP 起始模式」設定應用程式，請複製執行個體的 [回覆 URL] 值，然後將它貼到 Azure 入口網站上 [123ContactForm 網域及 URL] 區段中的 [回覆 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="e5fc5-188">c.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-188">c.</span></span> <span data-ttu-id="e5fc5-189">如果您想要以「SP 起始模式」設定應用程式，請複製執行個體的 [登入 URL] 值，然後將它貼到 Azure 入口網站上 [123ContactForm 網域及 URL] 區段中的 [登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="e5fc5-190">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="e5fc5-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e5fc5-191">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e5fc5-192">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e5fc5-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e5fc5-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e5fc5-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="e5fc5-194">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="e5fc5-196">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e5fc5-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e5fc5-197">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e5fc5-199">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e5fc5-201">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e5fc5-203">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e5fc5-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e5fc5-205">a.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-205">a.</span></span> <span data-ttu-id="e5fc5-206">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e5fc5-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-207">b.</span></span> <span data-ttu-id="e5fc5-208">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e5fc5-209">c.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-209">c.</span></span> <span data-ttu-id="e5fc5-210">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e5fc5-211">d.</span><span class="sxs-lookup"><span data-stu-id="e5fc5-211">d.</span></span> <span data-ttu-id="e5fc5-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="e5fc5-213">建立 123ContactForm 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e5fc5-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="e5fc5-214">應用程式支援及時 (Just In Time) 使用者佈建，而在驗證之後，則會在應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e5fc5-215">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e5fc5-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e5fc5-216">在本節中，您會將 123ContactForm 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span></span>

![指派使用者][200] 

<span data-ttu-id="e5fc5-218">**若要將 Britta Simon 指派給 123ContactForm，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="e5fc5-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="e5fc5-219">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e5fc5-221">在應用程式清單中，選取 [123ContactForm]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-221">In the applications list, select **123ContactForm**.</span></span>

    ![設定單一登入](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="e5fc5-223">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-223">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="e5fc5-225">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-225">Click **Add** button.</span></span> <span data-ttu-id="e5fc5-226">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="e5fc5-228">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e5fc5-229">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e5fc5-230">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e5fc5-231">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e5fc5-231">Testing single sign-on</span></span>

<span data-ttu-id="e5fc5-232">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e5fc5-233">當您在「存取面板」中按一下 [123ContactForm] 圖格時，應該會自動登入您的 123ContactForm 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span></span>
<span data-ttu-id="e5fc5-234">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e5fc5-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e5fc5-235">其他資源</span><span class="sxs-lookup"><span data-stu-id="e5fc5-235">Additional resources</span></span>

* [<span data-ttu-id="e5fc5-236">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="e5fc5-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e5fc5-237">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e5fc5-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png
