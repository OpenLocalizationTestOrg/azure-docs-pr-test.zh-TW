---
title: "教學課程：Azure Active Directory 與 Klue 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Klue 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c64417c136340b3ffa5d67c618c6fe037d2992b5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="1fbb1-103">教學課程：Azure Active Directory 與 Klue 整合</span><span class="sxs-lookup"><span data-stu-id="1fbb1-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="1fbb1-104">在本教學課程中，您會了解如何整合 Klue 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-104">In this tutorial, you learn how to integrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1fbb1-105">Klue 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="1fbb1-105">Integrating Klue with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1fbb1-106">您可以在 Azure AD 中控制可存取 Klue 的人員</span><span class="sxs-lookup"><span data-stu-id="1fbb1-106">You can control in Azure AD who has access to Klue</span></span>
- <span data-ttu-id="1fbb1-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Klue (單一登入)</span><span class="sxs-lookup"><span data-stu-id="1fbb1-107">You can enable your users to automatically get signed-on to Klue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1fbb1-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="1fbb1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1fbb1-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fbb1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1fbb1-110">Prerequisites</span></span>

<span data-ttu-id="1fbb1-111">若要設定 Azure AD 與 Klue 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1fbb1-111">To configure Azure AD integration with Klue, you need the following items:</span></span>

- <span data-ttu-id="1fbb1-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1fbb1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1fbb1-113">啟用 Klue 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1fbb1-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1fbb1-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1fbb1-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1fbb1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1fbb1-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1fbb1-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1fbb1-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1fbb1-118">Scenario description</span></span>
<span data-ttu-id="1fbb1-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1fbb1-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="1fbb1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1fbb1-121">從資源庫新增 Klue</span><span class="sxs-lookup"><span data-stu-id="1fbb1-121">Adding Klue from the gallery</span></span>
2. <span data-ttu-id="1fbb1-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1fbb1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-the-gallery"></a><span data-ttu-id="1fbb1-123">從資源庫新增 Klue</span><span class="sxs-lookup"><span data-stu-id="1fbb1-123">Adding Klue from the gallery</span></span>
<span data-ttu-id="1fbb1-124">若要設定將 Klue 整合到 Azure AD 中，您需要從資源庫將 Klue 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-124">To configure the integration of Klue into Azure AD, you need to add Klue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1fbb1-125">**若要從資源庫新增 Klue，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1fbb1-125">**To add Klue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1fbb1-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1fbb1-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1fbb1-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1fbb1-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1fbb1-133">在搜尋方塊中，輸入 **Klue**。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-133">In the search box, type **Klue**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="1fbb1-135">在結果面板中，選取 [Klue]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-135">In the results panel, select **Klue**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1fbb1-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1fbb1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1fbb1-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Klue 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1fbb1-139">若要讓單一登入運作，Azure AD 必須知道 Klue 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Klue is to a user in Azure AD.</span></span> <span data-ttu-id="1fbb1-140">換句話說，必須在 Azure AD 使用者和 Klue 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-140">In other words, a link relationship between an Azure AD user and the related user in Klue needs to be established.</span></span>

<span data-ttu-id="1fbb1-141">在 Klue 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-141">In Klue, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1fbb1-142">若要設定及測試與 Klue 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1fbb1-142">To configure and test Azure AD single sign-on with Klue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1fbb1-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1fbb1-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1fbb1-145">**[建立 Klue 測試使用者](#creating-a-klue-test-user)** - 使 Klue 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - to have a counterpart of Britta Simon in Klue that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1fbb1-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1fbb1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1fbb1-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1fbb1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1fbb1-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Klue 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="1fbb1-150">**若要設定與 Klue 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1fbb1-150">**To configure Azure AD single sign-on with Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="1fbb1-151">在 Azure 入口網站的 [Klue] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-151">In the Azure portal, on the **Klue** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1fbb1-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="1fbb1-155">如果您想要以 **IDP** 起始模式設定應用程式，請在 [Klue 網域及 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1fbb1-155">On the **Klue Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="1fbb1-157">a.</span><span class="sxs-lookup"><span data-stu-id="1fbb1-157">a.</span></span> <span data-ttu-id="1fbb1-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="1fbb1-158">In the **Identifier** textbox, type a URL using the following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="1fbb1-159">b.</span><span class="sxs-lookup"><span data-stu-id="1fbb1-159">b.</span></span> <span data-ttu-id="1fbb1-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="1fbb1-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="1fbb1-161">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="1fbb1-162">如果您想要以 **SP** 起始模式設定應用程式：</span><span class="sxs-lookup"><span data-stu-id="1fbb1-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="1fbb1-164">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="1fbb1-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1fbb1-165">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-165">These values are not real.</span></span> <span data-ttu-id="1fbb1-166">請使用實際的「回覆 URL」、「識別碼」及「登入 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-166">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="1fbb1-167">請連絡 [lue 客戶支援小組](mailto:support@klue.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-167">Contact [Klue Client support team](mailto:support@klue.com) to get these values.</span></span>

5. <span data-ttu-id="1fbb1-168">Klue 應用程式需要特定格式的 SAML 判斷提示，所以您必須將自訂屬性對應新增至 SAML 權杖屬性設定。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-168">The Klue application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="1fbb1-169">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-169">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![設定單一登入](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="1fbb1-171">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1fbb1-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="1fbb1-172">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="1fbb1-172">Attribute Name</span></span>      | <span data-ttu-id="1fbb1-173">屬性值</span><span class="sxs-lookup"><span data-stu-id="1fbb1-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="1fbb1-174">first_name</span><span class="sxs-lookup"><span data-stu-id="1fbb1-174">first_name</span></span>          | <span data-ttu-id="1fbb1-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="1fbb1-175">user.givenname</span></span> |
    | <span data-ttu-id="1fbb1-176">last_name</span><span class="sxs-lookup"><span data-stu-id="1fbb1-176">last_name</span></span>           | <span data-ttu-id="1fbb1-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="1fbb1-177">user.surname</span></span> |
    | <span data-ttu-id="1fbb1-178">電子郵件</span><span class="sxs-lookup"><span data-stu-id="1fbb1-178">email</span></span>               | <span data-ttu-id="1fbb1-179">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="1fbb1-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="1fbb1-180">a.</span><span class="sxs-lookup"><span data-stu-id="1fbb1-180">a.</span></span> <span data-ttu-id="1fbb1-181">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1fbb1-184">b.</span><span class="sxs-lookup"><span data-stu-id="1fbb1-184">b.</span></span> <span data-ttu-id="1fbb1-185">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-185">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="1fbb1-186">c.</span><span class="sxs-lookup"><span data-stu-id="1fbb1-186">c.</span></span> <span data-ttu-id="1fbb1-187">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-187">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1fbb1-188">d.</span><span class="sxs-lookup"><span data-stu-id="1fbb1-188">d.</span></span> <span data-ttu-id="1fbb1-189">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-189">Click **Ok**.</span></span>

7. <span data-ttu-id="1fbb1-190">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-190">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="1fbb1-192">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-192">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="1fbb1-194">在 [Klue 組態] 區段上，按一下 [設定 Klue] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-194">On the **Klue Configuration** section, click **Configure Klue** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1fbb1-195">從 [快速參考] 區段中複製 [SAML 實體 ID 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-195">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="1fbb1-197">若要在 **Klue** 端設定單一登入，您必須將已下載的**憑證(Base64)、SAML 單一登入服務 URL 和 SAML 實體識別碼**傳送給 [Klue 支援小組](mailto:support@klue.com)。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-197">To configure single sign-on on **Klue** side, you need to send the downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** to [Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="1fbb1-198">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="1fbb1-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1fbb1-199">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1fbb1-200">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1fbb1-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1fbb1-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1fbb1-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="1fbb1-202">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1fbb1-204">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1fbb1-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1fbb1-205">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1fbb1-207">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1fbb1-209">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1fbb1-211">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1fbb1-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1fbb1-213">a.</span><span class="sxs-lookup"><span data-stu-id="1fbb1-213">a.</span></span> <span data-ttu-id="1fbb1-214">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1fbb1-215">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-215">b.</span></span> <span data-ttu-id="1fbb1-216">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1fbb1-217">c.</span><span class="sxs-lookup"><span data-stu-id="1fbb1-217">c.</span></span> <span data-ttu-id="1fbb1-218">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1fbb1-219">d.</span><span class="sxs-lookup"><span data-stu-id="1fbb1-219">d.</span></span> <span data-ttu-id="1fbb1-220">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="1fbb1-221">建立 Klue 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1fbb1-221">Creating a Klue test user</span></span>

<span data-ttu-id="1fbb1-222">本節目標是在 Klue 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-222">The objective of this section is to create a user called Britta Simon in Klue.</span></span> <span data-ttu-id="1fbb1-223">Klue 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="1fbb1-224">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-224">There is no action item for you in this section.</span></span> <span data-ttu-id="1fbb1-225">嘗試存取 Klue 時若尚無使用者，則會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-225">A new user is created during an attempt to access Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="1fbb1-226">如果您需要手動建立使用者，請連絡 [Klue 支援小組](mailto:support@klue.com)。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-226">If you need to create a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1fbb1-227">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1fbb1-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1fbb1-228">在本節中，您會將 Klue 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Klue.</span></span>

![指派使用者][200] 

<span data-ttu-id="1fbb1-230">**若要將 Britta Simon 指派給 Klue，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1fbb1-230">**To assign Britta Simon to Klue, perform the following steps:**</span></span>

1. <span data-ttu-id="1fbb1-231">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1fbb1-233">在應用程式清單中，選取 [Klue]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-233">In the applications list, select **Klue**.</span></span>

    ![設定單一登入](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="1fbb1-235">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-235">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1fbb1-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-237">Click **Add** button.</span></span> <span data-ttu-id="1fbb1-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1fbb1-240">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1fbb1-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1fbb1-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1fbb1-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1fbb1-243">Testing single sign-on</span></span>

<span data-ttu-id="1fbb1-244">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1fbb1-245">當您在存取面板中按一下 Klue 圖格時，應該會自動登入您的 Klue 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-245">When you click the Klue tile in the Access Panel, you should get automatically signed-on to your Klue application.</span></span>
<span data-ttu-id="1fbb1-246">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1fbb1-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1fbb1-247">其他資源</span><span class="sxs-lookup"><span data-stu-id="1fbb1-247">Additional resources</span></span>

* [<span data-ttu-id="1fbb1-248">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="1fbb1-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1fbb1-249">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1fbb1-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

