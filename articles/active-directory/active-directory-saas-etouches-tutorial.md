---
title: "教學課程：Azure Active Directory 與 etouches 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 etouches 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 3cd9e9d6aae924369065ca492b1f6380c0ddc5fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a><span data-ttu-id="86861-103">教學課程：Azure Active Directory 與 etouches 整合</span><span class="sxs-lookup"><span data-stu-id="86861-103">Tutorial: Azure Active Directory integration with etouches</span></span>

<span data-ttu-id="86861-104">在本教學課程中，您將了解如何整合 etouches 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="86861-104">In this tutorial, you learn how to integrate etouches with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86861-105">etouches 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="86861-105">Integrating etouches with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="86861-106">您可以在 Azure AD 中管控可存取 etouches 的人員</span><span class="sxs-lookup"><span data-stu-id="86861-106">You can control in Azure AD who has access to etouches</span></span>
- <span data-ttu-id="86861-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 etouches (單一登入)</span><span class="sxs-lookup"><span data-stu-id="86861-107">You can enable your users to automatically get signed-on to etouches (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86861-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="86861-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="86861-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="86861-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86861-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="86861-110">Prerequisites</span></span>

<span data-ttu-id="86861-111">若要設定 Azure AD 與 etouches 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="86861-111">To configure Azure AD integration with etouches, you need the following items:</span></span>

- <span data-ttu-id="86861-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="86861-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86861-113">啟用 etouches 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="86861-113">An etouches single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86861-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="86861-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86861-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="86861-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86861-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="86861-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86861-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="86861-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86861-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="86861-118">Scenario description</span></span>
<span data-ttu-id="86861-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="86861-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86861-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="86861-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86861-121">從資源庫新增 etouches</span><span class="sxs-lookup"><span data-stu-id="86861-121">Adding etouches from the gallery</span></span>
2. <span data-ttu-id="86861-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="86861-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-etouches-from-the-gallery"></a><span data-ttu-id="86861-123">從資源庫新增 etouches</span><span class="sxs-lookup"><span data-stu-id="86861-123">Adding etouches from the gallery</span></span>
<span data-ttu-id="86861-124">若要設定將 etouches 整合到 Azure AD 中，您需要從資源庫將 etouches 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="86861-124">To configure the integration of etouches into Azure AD, you need to add etouches from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="86861-125">**若要從資源庫新增 etouches，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="86861-125">**To add etouches from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="86861-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="86861-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="86861-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="86861-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="86861-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="86861-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="86861-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86861-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="86861-133">在搜尋方塊中，輸入 **etouches**，從結果面板中選取 [etouches]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="86861-133">In the search box, type **etouches**, select **etouches** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="86861-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="86861-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="86861-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 etouches 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="86861-136">In this section, you configure and test Azure AD single sign-on with etouches based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="86861-137">若要讓單一登入能夠運作，Azure AD 必須知道 etouches 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="86861-137">For single sign-on to work, Azure AD needs to know what the counterpart user in etouches is to a user in Azure AD.</span></span> <span data-ttu-id="86861-138">換句話說，必須在 Azure AD 使用者與 etouches 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="86861-138">In other words, a link relationship between an Azure AD user and the related user in etouches needs to be established.</span></span>

<span data-ttu-id="86861-139">在 etouches 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="86861-139">In etouches, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="86861-140">若要設定及測試與 etouches 搭配運作的 Azure AD 單一登入，您需要完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="86861-140">To configure and test Azure AD single sign-on with etouches, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="86861-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="86861-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="86861-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="86861-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86861-143">**[建立 etouches 測試使用者](#create-an-etouches-test-user)** - 在 etouches 中建立一個與 Azure AD 中代表使用者之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="86861-143">**[Create an etouches test user](#create-an-etouches-test-user)** - to have a counterpart of Britta Simon in etouches that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="86861-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="86861-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86861-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="86861-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="86861-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="86861-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="86861-147">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，然後在您的 etouches 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="86861-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your etouches application.</span></span>

<span data-ttu-id="86861-148">**若要使用 etouches 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="86861-148">**To configure Azure AD single sign-on with etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="86861-149">在 Azure 入口網站的 [etouches] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="86861-149">In the Azure portal, on the **etouches** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="86861-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="86861-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. <span data-ttu-id="86861-153">在 [etouches 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="86861-153">On the **etouches Domain and URLs** section, perform the following steps:</span></span>

    ![etouches 網域及 URL 單一登入資訊](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    <span data-ttu-id="86861-155">a.</span><span class="sxs-lookup"><span data-stu-id="86861-155">a.</span></span> <span data-ttu-id="86861-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="86861-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`</span></span>

    <span data-ttu-id="86861-157">b.</span><span class="sxs-lookup"><span data-stu-id="86861-157">b.</span></span> <span data-ttu-id="86861-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://www.eiseverywhere.com/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="86861-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.eiseverywhere.com/<instance name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="86861-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="86861-159">These values are not real.</span></span> <span data-ttu-id="86861-160">您將使用實際的「登入 URL」與「識別碼」來更新值，稍後會在本教學課程中說明。</span><span class="sxs-lookup"><span data-stu-id="86861-160">You update the value with the actual Sign on URL and Identifier, which is explained later in the tutorial.</span></span>
    > 

4. <span data-ttu-id="86861-161">etouches 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="86861-161">etouches application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="86861-162">設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="86861-162">Configure the following claims for this application.</span></span> <span data-ttu-id="86861-163">您可以從應用程式的 [使用者屬性] 管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="86861-163">You can manage the values of these attributes from the **User Attribute** of the application.</span></span> <span data-ttu-id="86861-164">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="86861-164">The following screenshot shows an example for this.</span></span> 

    ![使用者屬性](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. <span data-ttu-id="86861-166">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="86861-166">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="86861-167">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="86861-167">Attribute Name</span></span> | <span data-ttu-id="86861-168">屬性值</span><span class="sxs-lookup"><span data-stu-id="86861-168">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="86861-169">電子郵件</span><span class="sxs-lookup"><span data-stu-id="86861-169">Email</span></span> | <span data-ttu-id="86861-170">user.mail</span><span class="sxs-lookup"><span data-stu-id="86861-170">user.mail</span></span> |    
    
    <span data-ttu-id="86861-171">a.</span><span class="sxs-lookup"><span data-stu-id="86861-171">a.</span></span> <span data-ttu-id="86861-172">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="86861-172">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![新增屬性](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![[新增屬性] 對話方塊](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="86861-175">b.</span><span class="sxs-lookup"><span data-stu-id="86861-175">b.</span></span> <span data-ttu-id="86861-176">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="86861-176">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="86861-177">c.</span><span class="sxs-lookup"><span data-stu-id="86861-177">c.</span></span> <span data-ttu-id="86861-178">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="86861-178">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="86861-179">d.</span><span class="sxs-lookup"><span data-stu-id="86861-179">d.</span></span> <span data-ttu-id="86861-180">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="86861-180">Click **Ok**.</span></span> 

6. <span data-ttu-id="86861-181">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="86861-181">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. <span data-ttu-id="86861-183">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="86861-183">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="86861-185">為了設定應用程式的 SSO，請在 etouches 應用程式中執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="86861-185">To get SSO configured for your application, perform the following steps in the etouches application:</span></span> 

    ![etouches 組態](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    <span data-ttu-id="86861-187">a.</span><span class="sxs-lookup"><span data-stu-id="86861-187">a.</span></span> <span data-ttu-id="86861-188">使用系統管理員權限登入 **etouches** 應用程式。</span><span class="sxs-lookup"><span data-stu-id="86861-188">Login to **etouches** application using the Admin rights.</span></span>
   
    <span data-ttu-id="86861-189">b.</span><span class="sxs-lookup"><span data-stu-id="86861-189">b.</span></span> <span data-ttu-id="86861-190">移至 [SAML] 組態。</span><span class="sxs-lookup"><span data-stu-id="86861-190">Go to the **SAML** Configuration.</span></span>

    <span data-ttu-id="86861-191">c.</span><span class="sxs-lookup"><span data-stu-id="86861-191">c.</span></span> <span data-ttu-id="86861-192">在 [一般設定] 區段中，以記事本開啟從 Azure 入口網站下載的憑證並複製內容，然後貼至 [IDP 中繼資料] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="86861-192">In the **General Settings** section, open your downloaded certificate from Azure portal in notepad, copy the content, and then paste it into the IDP metadata textbox.</span></span> 

    <span data-ttu-id="86861-193">d.</span><span class="sxs-lookup"><span data-stu-id="86861-193">d.</span></span> <span data-ttu-id="86861-194">按一下 [儲存並留下] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86861-194">Click on the **Save & Stay** button.</span></span>
  
    <span data-ttu-id="86861-195">e.</span><span class="sxs-lookup"><span data-stu-id="86861-195">e.</span></span> <span data-ttu-id="86861-196">按一下 [SAML 中繼資料] 區段中的 [更新中繼資料] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86861-196">Click on the **Update Metadata** button in the SAML Metadata section.</span></span> 

    <span data-ttu-id="86861-197">f.</span><span class="sxs-lookup"><span data-stu-id="86861-197">f.</span></span> <span data-ttu-id="86861-198">這會開啟網頁，並執行 SSO。</span><span class="sxs-lookup"><span data-stu-id="86861-198">This opens the page and perform SSO.</span></span> <span data-ttu-id="86861-199">一旦 SSO 開始運作，您就可以設定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="86861-199">Once the SSO is working then you can set up the username.</span></span>

    <span data-ttu-id="86861-200">g.</span><span class="sxs-lookup"><span data-stu-id="86861-200">g.</span></span> <span data-ttu-id="86861-201">在 [使用者名稱] 欄位中選取**電子郵件地址**，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="86861-201">In the Username field, select the **emailaddress** as shown in the image below.</span></span> 

    <span data-ttu-id="86861-202">h.</span><span class="sxs-lookup"><span data-stu-id="86861-202">h.</span></span> <span data-ttu-id="86861-203">複製**預存程序實體識別碼**值，並將其貼至 [識別碼] 文字方塊中 (位於 Azure 入口網站的 [etouches 網域與 URL] 區段)。</span><span class="sxs-lookup"><span data-stu-id="86861-203">Copy the **SP entity ID** value and paste it into the **Identifier**  textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="86861-204">i.</span><span class="sxs-lookup"><span data-stu-id="86861-204">i.</span></span> <span data-ttu-id="86861-205">複製 **SSO URL / ACS** 值，並將其貼至 [單一登入 URL] 文字方塊中 (位於 Azure 入口網站的 [etouches 網域與 URL] 區段)。</span><span class="sxs-lookup"><span data-stu-id="86861-205">Copy the **SSO URL / ACS** value and paste it into the **Sign on URL** textbox, which is in **etouches Domain and URLs** section on Azure portal.</span></span>
   
> [!TIP]
> <span data-ttu-id="86861-206">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="86861-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="86861-207">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="86861-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="86861-208">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86861-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="86861-209">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="86861-209">Create an Azure AD test user</span></span>
<span data-ttu-id="86861-210">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="86861-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="86861-212">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="86861-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="86861-213">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="86861-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86861-215">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="86861-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86861-217">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="86861-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86861-219">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="86861-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86861-221">a.</span><span class="sxs-lookup"><span data-stu-id="86861-221">a.</span></span> <span data-ttu-id="86861-222">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="86861-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86861-223">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="86861-223">b.</span></span> <span data-ttu-id="86861-224">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="86861-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86861-225">c.</span><span class="sxs-lookup"><span data-stu-id="86861-225">c.</span></span> <span data-ttu-id="86861-226">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="86861-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="86861-227">d.</span><span class="sxs-lookup"><span data-stu-id="86861-227">d.</span></span> <span data-ttu-id="86861-228">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="86861-228">Click **Create**.</span></span>
 
### <a name="create-an-etouches-test-user"></a><span data-ttu-id="86861-229">建立 etouches 測試使用者</span><span class="sxs-lookup"><span data-stu-id="86861-229">Create an etouches test user</span></span>

<span data-ttu-id="86861-230">在本節中，您會於 etouches 建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="86861-230">In this section, you create a user called Britta Simon in etouches.</span></span> <span data-ttu-id="86861-231">與 [etouches 支援小組](https://www.etouches.com/event-software/support/customer-support/)合作，在 etouches 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="86861-231">Work with [etouches Client support team](https://www.etouches.com/event-software/support/customer-support/) to add the users in the etouches platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="86861-232">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="86861-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="86861-233">在本節中，您會將 etouches 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="86861-233">In this section, you enable Britta Simon to use Azure single sign-on by granting access to etouches.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="86861-235">**若要將 Britta Simon 指派給 etouches，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="86861-235">**To assign Britta Simon to etouches, perform the following steps:**</span></span>

1. <span data-ttu-id="86861-236">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="86861-236">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="86861-238">在應用程式清單中，選取 [etouches] 。</span><span class="sxs-lookup"><span data-stu-id="86861-238">In the applications list, select **etouches**.</span></span>

    ![應用程式清單中的 etouches 連結](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. <span data-ttu-id="86861-240">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="86861-240">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202] 

4. <span data-ttu-id="86861-242">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86861-242">Click **Add** button.</span></span> <span data-ttu-id="86861-243">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="86861-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="86861-245">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="86861-245">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="86861-246">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86861-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86861-247">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="86861-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="86861-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="86861-248">Test single sign-on</span></span>


<span data-ttu-id="86861-249">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="86861-249">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="86861-250">當您在「存取面板」中按一下 etouches 圖格時，應該會自動登入您的 etouches 應用程式。</span><span class="sxs-lookup"><span data-stu-id="86861-250">When you click the etouches tile in the Access Panel, you should get automatically signed-on to your etouches application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86861-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="86861-251">Additional resources</span></span>

* [<span data-ttu-id="86861-252">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="86861-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86861-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="86861-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

