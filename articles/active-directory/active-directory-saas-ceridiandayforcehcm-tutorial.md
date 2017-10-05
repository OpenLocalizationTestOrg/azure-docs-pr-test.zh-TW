---
title: "教學課程：Azure Active Directory 與 Ceridian Dayforce HCM 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Ceridian Dayforce HCM 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b2ea3d92f233dab5bd6814e4875f881117eac8e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a><span data-ttu-id="f36a2-103">教學課程：Azure Active Directory 與 Ceridian Dayforce HCM 整合</span><span class="sxs-lookup"><span data-stu-id="f36a2-103">Tutorial: Azure Active Directory integration with Ceridian Dayforce HCM</span></span>

<span data-ttu-id="f36a2-104">在本教學課程中，您將了解如何整合 Ceridian Dayforce HCM 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f36a2-104">In this tutorial, you learn how to integrate Ceridian Dayforce HCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f36a2-105">Ceridian Dayforce HCM 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f36a2-105">Integrating Ceridian Dayforce HCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f36a2-106">您可以在 Azure AD 中控制可存取 Ceridian Dayforce HCM 的人員。</span><span class="sxs-lookup"><span data-stu-id="f36a2-106">You can control in Azure AD who has access to Ceridian Dayforce HCM.</span></span>
- <span data-ttu-id="f36a2-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Ceridian Dayforce HCM (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="f36a2-107">You can enable your users to automatically get signed-on to Ceridian Dayforce HCM (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f36a2-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f36a2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f36a2-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f36a2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f36a2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f36a2-110">Prerequisites</span></span>

<span data-ttu-id="f36a2-111">若要設定 Azure AD 與 Ceridian Dayforce HCM 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f36a2-111">To configure Azure AD integration with Ceridian Dayforce HCM, you need the following items:</span></span>

- <span data-ttu-id="f36a2-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f36a2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f36a2-113">啟用 Ceridian Dayforce HCM 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f36a2-113">A Ceridian Dayforce HCM single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f36a2-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f36a2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f36a2-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f36a2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f36a2-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f36a2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f36a2-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="f36a2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f36a2-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f36a2-118">Scenario description</span></span>
<span data-ttu-id="f36a2-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f36a2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f36a2-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f36a2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f36a2-121">從資源庫新增 Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="f36a2-121">Adding Ceridian Dayforce HCM from the gallery</span></span>
2. <span data-ttu-id="f36a2-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f36a2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ceridian-dayforce-hcm-from-the-gallery"></a><span data-ttu-id="f36a2-123">從資源庫新增 Ceridian Dayforce HCM</span><span class="sxs-lookup"><span data-stu-id="f36a2-123">Adding Ceridian Dayforce HCM from the gallery</span></span>
<span data-ttu-id="f36a2-124">若要設定將 Ceridian Dayforce HCM 整合到 Azure AD 中，您需要從資源庫將 Ceridian Dayforce HCM 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="f36a2-124">To configure the integration of Ceridian Dayforce HCM into Azure AD, you need to add Ceridian Dayforce HCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f36a2-125">**若要從資源庫新增 Ceridian Dayforce HCM，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f36a2-125">**To add Ceridian Dayforce HCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f36a2-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f36a2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="f36a2-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f36a2-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="f36a2-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f36a2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="f36a2-133">在搜尋方塊中，輸入 **Ceridian Dayforce HCM**，從結果面板選取 [Ceridian Dayforce HCM]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f36a2-133">In the search box, type **Ceridian Dayforce HCM**, select **Ceridian Dayforce HCM** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f36a2-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f36a2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f36a2-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Ceridian Dayforce HCM 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f36a2-136">In this section, you configure and test Azure AD single sign-on with Ceridian Dayforce HCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f36a2-137">若要讓單一登入運作，Azure AD 必須知道 Ceridian Dayforce HCM 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f36a2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Ceridian Dayforce HCM is to a user in Azure AD.</span></span> <span data-ttu-id="f36a2-138">換句話說，必須在 Azure AD 使用者與 Ceridian Dayforce HCM 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f36a2-138">In other words, a link relationship between an Azure AD user and the related user in Ceridian Dayforce HCM needs to be established.</span></span>

<span data-ttu-id="f36a2-139">在 Ceridian Dayforce HCM 中，將 [Username] 的值指派為 Azure AD 中 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f36a2-139">In Ceridian Dayforce HCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f36a2-140">若要設定及測試與 Ceridian Dayforce HCM 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="f36a2-140">To configure and test Azure AD single sign-on with Ceridian Dayforce HCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f36a2-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f36a2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f36a2-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f36a2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f36a2-143">**[建立 Ceridian Dayforce HCM 測試使用者](#create-a-ceridian-dayforce-hcm-test-user)** - 在 Ceridian Dayforce HCM 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="f36a2-143">**[Create a Ceridian Dayforce HCM test user](#create-a-ceridian-dayforce-hcm-test-user)** - to have a counterpart of Britta Simon in Ceridian Dayforce HCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f36a2-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f36a2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f36a2-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f36a2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f36a2-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f36a2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f36a2-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Ceridian Dayforce HCM 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f36a2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ceridian Dayforce HCM application.</span></span>

<span data-ttu-id="f36a2-148">**若要設定與 Ceridian Dayforce HCM 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f36a2-148">**To configure Azure AD single sign-on with Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="f36a2-149">在 Azure 入口網站的 [Ceridian Dayforce HCM] 應用程式整合分頁上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-149">In the Azure portal, on the **Ceridian Dayforce HCM** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="f36a2-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f36a2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. <span data-ttu-id="f36a2-153">在 [Ceridian Dayforce HCM 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f36a2-153">On the **Ceridian Dayforce HCM Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    <span data-ttu-id="f36a2-155">a.</span><span class="sxs-lookup"><span data-stu-id="f36a2-155">a.</span></span> <span data-ttu-id="f36a2-156">在 [登入 URL] 文字方塊中，輸入使用者用來登入您 Ceridian Dayforce HCM 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="f36a2-156">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Ceridian Dayforce HCM application.</span></span>
    
    | <span data-ttu-id="f36a2-157">環境</span><span class="sxs-lookup"><span data-stu-id="f36a2-157">Environment</span></span> | <span data-ttu-id="f36a2-158">URL</span><span class="sxs-lookup"><span data-stu-id="f36a2-158">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="f36a2-159">針對生產環境</span><span class="sxs-lookup"><span data-stu-id="f36a2-159">For production</span></span> | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | <span data-ttu-id="f36a2-160">針對測試</span><span class="sxs-lookup"><span data-stu-id="f36a2-160">For test</span></span> | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    <span data-ttu-id="f36a2-161">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f36a2-161">b.</span></span> <span data-ttu-id="f36a2-162">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：</span><span class="sxs-lookup"><span data-stu-id="f36a2-162">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    
    | <span data-ttu-id="f36a2-163">環境</span><span class="sxs-lookup"><span data-stu-id="f36a2-163">Environment</span></span> | <span data-ttu-id="f36a2-164">URL</span><span class="sxs-lookup"><span data-stu-id="f36a2-164">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="f36a2-165">針對生產環境</span><span class="sxs-lookup"><span data-stu-id="f36a2-165">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp` |
    | <span data-ttu-id="f36a2-166">針對測試</span><span class="sxs-lookup"><span data-stu-id="f36a2-166">For test</span></span> | `https://fs-test.dayforcehcm.com/sp` |
    
    <span data-ttu-id="f36a2-167">c.</span><span class="sxs-lookup"><span data-stu-id="f36a2-167">c.</span></span> <span data-ttu-id="f36a2-168">在 [回覆 URL] 文字方塊中，輸入 Azure AD 用來公佈回應的 URL。</span><span class="sxs-lookup"><span data-stu-id="f36a2-168">In the **Reply URL** textbox, type the URL used by Azure AD to post the response.</span></span>
    
    | <span data-ttu-id="f36a2-169">環境</span><span class="sxs-lookup"><span data-stu-id="f36a2-169">Environment</span></span> | <span data-ttu-id="f36a2-170">URL</span><span class="sxs-lookup"><span data-stu-id="f36a2-170">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="f36a2-171">針對生產環境</span><span class="sxs-lookup"><span data-stu-id="f36a2-171">For production</span></span> | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | <span data-ttu-id="f36a2-172">針對測試</span><span class="sxs-lookup"><span data-stu-id="f36a2-172">For test</span></span> | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > <span data-ttu-id="f36a2-173">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f36a2-173">These values are not real.</span></span> <span data-ttu-id="f36a2-174">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="f36a2-174">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="f36a2-175">請連絡 [Ceridian Dayforce HCM 用戶端支援小組](https://www.ceridian.com/contact-us/index.html)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="f36a2-175">Contact [Ceridian Dayforce HCM Client support team](https://www.ceridian.com/contact-us/index.html) to get these values.</span></span>

4. <span data-ttu-id="f36a2-176">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f36a2-176">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. <span data-ttu-id="f36a2-178">Ceridian Dayforce HCM 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="f36a2-178">Your Ceridian Dayforce HCM application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="f36a2-179">請先與 [Ceridian Dayforce HCM 支援小組](https://www.ceridian.com/contact-us/index.html)合作來識別正確的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="f36a2-179">Work with [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) first to identify the correct user identifier.</span></span> <span data-ttu-id="f36a2-180">Microsoft 建議使用 **"name"** 屬性做為使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="f36a2-180">Microsoft recommends using the **"name"** attribute as user identifier.</span></span> <span data-ttu-id="f36a2-181">您可以在應用程式整合頁面的 [使用者屬性] 區段中，管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f36a2-181">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="f36a2-182">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="f36a2-182">The following screenshot shows an example for this.</span></span>  

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. <span data-ttu-id="f36a2-184">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f36a2-184">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="f36a2-185">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="f36a2-185">Attribute Name</span></span>  | <span data-ttu-id="f36a2-186">屬性值</span><span class="sxs-lookup"><span data-stu-id="f36a2-186">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="f36a2-187">名稱</span><span class="sxs-lookup"><span data-stu-id="f36a2-187">name</span></span>  | <span data-ttu-id="f36a2-188">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="f36a2-188">user.extensionattribute2</span></span> |    

    <span data-ttu-id="f36a2-189">a.</span><span class="sxs-lookup"><span data-stu-id="f36a2-189">a.</span></span> <span data-ttu-id="f36a2-190">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f36a2-190">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="f36a2-193">b.</span><span class="sxs-lookup"><span data-stu-id="f36a2-193">b.</span></span> <span data-ttu-id="f36a2-194">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="f36a2-194">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="f36a2-195">c.</span><span class="sxs-lookup"><span data-stu-id="f36a2-195">c.</span></span> <span data-ttu-id="f36a2-196">在 [值] 清單中，選取您想要用於實作的使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="f36a2-196">In the **Value** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="f36a2-197">例如，如果您想要使用 EmployeeID 為唯一的使用者識別碼，而且已在 ExtensionAttribute2 中儲存屬性值，則選取 [user.extensionattribute2]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-197">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select **user.extensionattribute2**.</span></span>
    
    <span data-ttu-id="f36a2-198">d.</span><span class="sxs-lookup"><span data-stu-id="f36a2-198">d.</span></span> <span data-ttu-id="f36a2-199">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f36a2-199">Click **Ok**.</span></span>

7. <span data-ttu-id="f36a2-200">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f36a2-200">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="f36a2-202">在 [Ceridian Dayforce HCM 設定] 區段中，按一下 [設定 Ceridian Dayforce HCM] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f36a2-202">On the **Ceridian Dayforce HCM Configuration** section, click **Configure Ceridian Dayforce HCM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f36a2-203">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-203">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Ceridian Dayforce HCM 設定](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. <span data-ttu-id="f36a2-205">若要在 **Ceridian Dayforce HCM** 這一端設定單一登入，您需要將所下載的**中繼資料 XML**、**登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL** 傳送給 [Ceridian Dayforce HCM 支援小組](https://www.ceridian.com/contact-us/index.html)。</span><span class="sxs-lookup"><span data-stu-id="f36a2-205">To configure single sign-on on **Ceridian Dayforce HCM** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html).</span></span>

> [!TIP]
> <span data-ttu-id="f36a2-206">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="f36a2-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f36a2-207">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="f36a2-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f36a2-208">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f36a2-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f36a2-209">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f36a2-209">Create an Azure AD test user</span></span>

<span data-ttu-id="f36a2-210">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f36a2-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="f36a2-212">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f36a2-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f36a2-213">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f36a2-213">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="f36a2-215">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-215">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="f36a2-217">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-217">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="f36a2-219">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f36a2-219">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f36a2-221">a.</span><span class="sxs-lookup"><span data-stu-id="f36a2-221">a.</span></span> <span data-ttu-id="f36a2-222">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f36a2-222">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f36a2-223">b.</span><span class="sxs-lookup"><span data-stu-id="f36a2-223">b.</span></span> <span data-ttu-id="f36a2-224">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="f36a2-224">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f36a2-225">c.</span><span class="sxs-lookup"><span data-stu-id="f36a2-225">c.</span></span> <span data-ttu-id="f36a2-226">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="f36a2-226">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f36a2-227">d.</span><span class="sxs-lookup"><span data-stu-id="f36a2-227">d.</span></span> <span data-ttu-id="f36a2-228">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f36a2-228">Click **Create**.</span></span>
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a><span data-ttu-id="f36a2-229">建立 Ceridian Dayforce HCM 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f36a2-229">Create a Ceridian Dayforce HCM test user</span></span>

<span data-ttu-id="f36a2-230">本節的目標是要在 Ceridian Dayforce HCM 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f36a2-230">The objective of this section is to create a user called Britta Simon in Ceridian Dayforce HCM.</span></span> <span data-ttu-id="f36a2-231">請與 [Ceridian Dayforce HCM 支援小組](https://www.ceridian.com/contact-us/index.html)合作，將使用者新增至您的 Ceridian Dayforce HCM 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f36a2-231">Work with the [Ceridian Dayforce HCM support team](https://www.ceridian.com/contact-us/index.html) to get users added in the Ceridian Dayforce HCM application.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f36a2-232">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f36a2-232">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f36a2-233">在本節中，您會將 Ceridian Dayforce HCM 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f36a2-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![指派使用者][200] 

<span data-ttu-id="f36a2-235">**若要將 Britta Simon 指派給 Ceridian Dayforce HCM，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f36a2-235">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="f36a2-236">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f36a2-238">在應用程式清單中，選取 [Ceridian Dayforce HCM] 。</span><span class="sxs-lookup"><span data-stu-id="f36a2-238">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. <span data-ttu-id="f36a2-240">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-240">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f36a2-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f36a2-242">Click **Add** button.</span></span> <span data-ttu-id="f36a2-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f36a2-245">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f36a2-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f36a2-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f36a2-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f36a2-247">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f36a2-248">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f36a2-248">Assign the Azure AD test user</span></span>

<span data-ttu-id="f36a2-249">在本節中，您會將 Ceridian Dayforce HCM 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f36a2-249">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ceridian Dayforce HCM.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="f36a2-251">**若要將 Britta Simon 指派給 Ceridian Dayforce HCM，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f36a2-251">**To assign Britta Simon to Ceridian Dayforce HCM, perform the following steps:**</span></span>

1. <span data-ttu-id="f36a2-252">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-252">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f36a2-254">在應用程式清單中，選取 [Ceridian Dayforce HCM] 。</span><span class="sxs-lookup"><span data-stu-id="f36a2-254">In the applications list, select **Ceridian Dayforce HCM**.</span></span>

    ![應用程式清單中的 Ceridian Dayforce HCM 連結](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. <span data-ttu-id="f36a2-256">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-256">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="f36a2-258">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f36a2-258">Click **Add** button.</span></span> <span data-ttu-id="f36a2-259">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="f36a2-261">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f36a2-261">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f36a2-262">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f36a2-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f36a2-263">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f36a2-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f36a2-264">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f36a2-264">Test single sign-on</span></span>

<span data-ttu-id="f36a2-265">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="f36a2-265">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f36a2-266">當您在存取面板中按一下 [Ceridian Dayforce HCM] 圖格時，應該會自動登入您的 Ceridian Dayforce HCM 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f36a2-266">When you click the Ceridian Dayforce HCM tile in the Access Panel, you should get automatically signed-on to your Ceridian Dayforce HCM application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f36a2-267">其他資源</span><span class="sxs-lookup"><span data-stu-id="f36a2-267">Additional resources</span></span>

* [<span data-ttu-id="f36a2-268">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f36a2-268">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f36a2-269">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f36a2-269">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

