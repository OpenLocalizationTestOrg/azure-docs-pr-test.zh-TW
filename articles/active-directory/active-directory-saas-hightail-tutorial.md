---
title: "教學課程：Azure Active Directory 與 Hightail 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Hightail 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: ba55f9b62d274aa3eb91723c62b53f54de0891b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a><span data-ttu-id="d1eb8-103">教學課程：Azure Active Directory 與 Hightail 整合</span><span class="sxs-lookup"><span data-stu-id="d1eb8-103">Tutorial: Azure Active Directory integration with Hightail</span></span>

<span data-ttu-id="d1eb8-104">在本教學課程中，您將了解如何整合 Hightail 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-104">In this tutorial, you learn how to integrate Hightail with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1eb8-105">Hightail 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d1eb8-105">Integrating Hightail with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d1eb8-106">您可以在 Azure AD 中控制可存取 Hightail 的人員</span><span class="sxs-lookup"><span data-stu-id="d1eb8-106">You can control in Azure AD who has access to Hightail</span></span>
- <span data-ttu-id="d1eb8-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Hightail (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d1eb8-107">You can enable your users to automatically get signed-on to Hightail (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d1eb8-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d1eb8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d1eb8-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1eb8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d1eb8-110">Prerequisites</span></span>

<span data-ttu-id="d1eb8-111">若要設定與 Hightail 的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d1eb8-111">To configure Azure AD integration with Hightail, you need the following items:</span></span>

- <span data-ttu-id="d1eb8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d1eb8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1eb8-113">已啟用 Hightail 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d1eb8-113">A Hightail single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1eb8-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1eb8-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d1eb8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1eb8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d1eb8-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1eb8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d1eb8-118">Scenario description</span></span>
<span data-ttu-id="d1eb8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1eb8-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d1eb8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1eb8-121">從資源庫加入 Hightail</span><span class="sxs-lookup"><span data-stu-id="d1eb8-121">Adding Hightail from the gallery</span></span>
2. <span data-ttu-id="d1eb8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d1eb8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hightail-from-the-gallery"></a><span data-ttu-id="d1eb8-123">從資源庫加入 Hightail</span><span class="sxs-lookup"><span data-stu-id="d1eb8-123">Adding Hightail from the gallery</span></span>
<span data-ttu-id="d1eb8-124">若要設定 Hightail 與 Azure AD 整合，您需要從資源庫將 Hightail 加入受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-124">To configure the integration of Hightail into Azure AD, you need to add Hightail from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d1eb8-125">**若要從資源庫加入 Hightail，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d1eb8-125">**To add Hightail from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d1eb8-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d1eb8-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d1eb8-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d1eb8-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d1eb8-133">在搜尋方塊中，輸入 **Hightail**。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-133">In the search box, type **Hightail**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. <span data-ttu-id="d1eb8-135">在結果窗格中，選取 [Hightail]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-135">In the results panel, select **Hightail**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d1eb8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d1eb8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d1eb8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Hightail 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-138">In this section, you configure and test Azure AD single sign-on with Hightail based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1eb8-139">若要讓單一登入運作，Azure AD 必須知道 Hightail 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hightail is to a user in Azure AD.</span></span> <span data-ttu-id="d1eb8-140">換句話說，必須在 Azure AD 使用者和 Hightail 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-140">In other words, a link relationship between an Azure AD user and the related user in Hightail needs to be established.</span></span>

<span data-ttu-id="d1eb8-141">在 Hightail 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-141">In Hightail, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d1eb8-142">若要設定及測試對 Hightail 的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d1eb8-142">To configure and test Azure AD single sign-on with Hightail, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d1eb8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d1eb8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1eb8-145">**[建立 Hightail 測試使用者](#creating-a-hightail-test-user)** - 在 Hightail 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-145">**[Creating a Hightail test user](#creating-a-hightail-test-user)** - to have a counterpart of Britta Simon in Hightail that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d1eb8-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1eb8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d1eb8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d1eb8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d1eb8-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Hightail 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hightail application.</span></span>

<span data-ttu-id="d1eb8-150">**若要使用 Hightail 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d1eb8-150">**To configure Azure AD single sign-on with Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="d1eb8-151">在 Azure 入口網站的 [Hightail] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-151">In the Azure portal, on the **Hightail** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d1eb8-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. <span data-ttu-id="d1eb8-155">在 [Hightail 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1eb8-155">On the **Hightail Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     <span data-ttu-id="d1eb8-157">在 [回覆 URL] 文字方塊中，輸入 URL：`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span><span class="sxs-lookup"><span data-stu-id="d1eb8-157">In the **Reply URL** textbox, type the URL as: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d1eb8-158">上述值並非真正的值。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-158">The preceding value is not real value.</span></span> <span data-ttu-id="d1eb8-159">您將會使用實際的「回覆 URL」來更新值，稍後會在本教學課程中說明。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-159">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="d1eb8-160">在 [Hightail 網域和 URL] 區段中，如果您想要在 [SP 起始模式] 中設定應用程式，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1eb8-160">On the **Hightail Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    <span data-ttu-id="d1eb8-162">a.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-162">a.</span></span> <span data-ttu-id="d1eb8-163">按一下 [顯示進階 URL 設定]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-163">Click the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="d1eb8-164">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-164">b.</span></span> <span data-ttu-id="d1eb8-165">在 [登入 URL] 文字方塊中，輸入 URL：`https://www.hightail.com/loginSSO`</span><span class="sxs-lookup"><span data-stu-id="d1eb8-165">In the **Sign On URL** textbox, type the URL as: `https://www.hightail.com/loginSSO`</span></span>

4. <span data-ttu-id="d1eb8-166">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-166">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. <span data-ttu-id="d1eb8-168">Hightail 應用程式需要特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-168">Hightail application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="d1eb8-169">請設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-169">Please configure the following claims for this application.</span></span> <span data-ttu-id="d1eb8-170">您可以從應用程式的 [屬性]  索引標籤來管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-170">You can manage the values of these attributes from the **"Atrribute"** tab of the application.</span></span> <span data-ttu-id="d1eb8-171">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-171">The following screenshot shows an example for this.</span></span> 

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. <span data-ttu-id="d1eb8-173">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1eb8-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="d1eb8-174">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="d1eb8-174">Attribute Name</span></span> | <span data-ttu-id="d1eb8-175">屬性值</span><span class="sxs-lookup"><span data-stu-id="d1eb8-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="d1eb8-176">名字</span><span class="sxs-lookup"><span data-stu-id="d1eb8-176">FirstName</span></span> | <span data-ttu-id="d1eb8-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="d1eb8-177">user.givenname</span></span> |
    | <span data-ttu-id="d1eb8-178">姓氏</span><span class="sxs-lookup"><span data-stu-id="d1eb8-178">LastName</span></span> | <span data-ttu-id="d1eb8-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="d1eb8-179">user.surname</span></span> |
    | <span data-ttu-id="d1eb8-180">電子郵件</span><span class="sxs-lookup"><span data-stu-id="d1eb8-180">Email</span></span> | <span data-ttu-id="d1eb8-181">user.mail</span><span class="sxs-lookup"><span data-stu-id="d1eb8-181">user.mail</span></span> |    
    | <span data-ttu-id="d1eb8-182">UserIdentity</span><span class="sxs-lookup"><span data-stu-id="d1eb8-182">UserIdentity</span></span> | <span data-ttu-id="d1eb8-183">user.mail</span><span class="sxs-lookup"><span data-stu-id="d1eb8-183">user.mail</span></span> |
    
    <span data-ttu-id="d1eb8-184">a.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-184">a.</span></span> <span data-ttu-id="d1eb8-185">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-185">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="d1eb8-188">b.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-188">b.</span></span> <span data-ttu-id="d1eb8-189">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-189">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="d1eb8-190">c.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-190">c.</span></span> <span data-ttu-id="d1eb8-191">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-191">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="d1eb8-192">d.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-192">d.</span></span> <span data-ttu-id="d1eb8-193">讓 [命名空間] 保持空白。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-193">Leave the **Namespace** blank.</span></span>
    
    <span data-ttu-id="d1eb8-194">e.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-194">e.</span></span> <span data-ttu-id="d1eb8-195">按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-195">Click **Ok**.</span></span>

7. <span data-ttu-id="d1eb8-196">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-196">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d1eb8-198">在 [Hightail 組態] 區段上，按一下 [設定 Hightail] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-198">On the **Hightail Configuration** section, click **Configure Hightail** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d1eb8-199">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-199">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    ><span data-ttu-id="d1eb8-201">在 Hightail 應用程式設定單一登入之前，請透過 Hightail 小組將您的電子郵件網域列入白名單，以便使用此網域的所有使用者都可以使用單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-201">Before configuring the Single Sign On at Hightail app, please white list your email domain with Hightail team so that all the users who are using this domain can use Single Sign On functionality.</span></span>


9. <span data-ttu-id="d1eb8-202">若要取得為應用程式設定的 SSO，您必須以系統管理員身分登入 Hightail 租用戶。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-202">To get SSO configured for your application, you need to sign-on to your Hightail tenant as an administrator.</span></span>
   
    <span data-ttu-id="d1eb8-203">a.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-203">a.</span></span> <span data-ttu-id="d1eb8-204">在頂端功能表中，按一下 [帳戶] 索引標籤並選取 [設定 SAML]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-204">In the menu on the top, click the **Account** tab and select **Configure SAML**.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    <span data-ttu-id="d1eb8-206">b.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-206">b.</span></span> <span data-ttu-id="d1eb8-207">選取 [啟用 SAML 驗證] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-207">Select the checkbox of **Enable SAML Authentication**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    <span data-ttu-id="d1eb8-209">c.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-209">c.</span></span> <span data-ttu-id="d1eb8-210">在從 Azure 入口網站下載的記事本中開啟您的 base-64 編碼的憑證，將它的內容複製到您的剪貼簿，然後在 [SAML 權杖簽署憑證] 文字方塊貼上。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-210">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **SAML Token Signing Certificate** textbox.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    <span data-ttu-id="d1eb8-212">d.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-212">d.</span></span> <span data-ttu-id="d1eb8-213">在 [SAML 授權單位 (識別提供者)/] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-213">In the **SAML Authority (Identity Provider)** textbox, paste the value of **SAML Single Sign-On Service URL** copied from Azure portal.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    <span data-ttu-id="d1eb8-215">e.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-215">e.</span></span> <span data-ttu-id="d1eb8-216">如果您想要以 **IDP 起始模式**設定應用程式，請選取 [識別提供者 (IdP) 起始登入]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-216">If you wish to configure the application in **IDP initiated mode** select **"Identity Provider (IdP) initiated log in"**.</span></span> <span data-ttu-id="d1eb8-217">若為 **SP 起始模式**，請選取 [服務提供者 (SP) 起始登入]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-217">If **SP initiated mode** select **"Service Provider (SP) initiated log in"**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    <span data-ttu-id="d1eb8-219">f.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-219">f.</span></span> <span data-ttu-id="d1eb8-220">複製執行個體的 SAML 取用者 URL，並將其貼在 Azure 入口網站上 [Hightail 網域與 URL] 區段的 [回覆 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-220">Copy the SAML consumer URL for your instance and paste it in **Reply URL** textbox in **Hightail Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="d1eb8-221">g.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-221">g.</span></span> <span data-ttu-id="d1eb8-222">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-222">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d1eb8-223">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="d1eb8-223">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d1eb8-224">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-224">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d1eb8-225">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d1eb8-225">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d1eb8-226">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d1eb8-226">Creating an Azure AD test user</span></span>
<span data-ttu-id="d1eb8-227">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-227">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d1eb8-229">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d1eb8-229">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d1eb8-230">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-230">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d1eb8-232">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-232">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d1eb8-234">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-234">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d1eb8-236">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d1eb8-236">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d1eb8-238">a.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-238">a.</span></span> <span data-ttu-id="d1eb8-239">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-239">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1eb8-240">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-240">b.</span></span> <span data-ttu-id="d1eb8-241">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-241">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d1eb8-242">c.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-242">c.</span></span> <span data-ttu-id="d1eb8-243">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-243">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d1eb8-244">d.</span><span class="sxs-lookup"><span data-stu-id="d1eb8-244">d.</span></span> <span data-ttu-id="d1eb8-245">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-245">Click **Create**.</span></span>
 
### <a name="creating-a-hightail-test-user"></a><span data-ttu-id="d1eb8-246">建立 Hightail 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d1eb8-246">Creating a Hightail test user</span></span>

<span data-ttu-id="d1eb8-247">本節目標是在 Hightail 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-247">The objective of this section is to create a user called Britta Simon in Hightail.</span></span> 

<span data-ttu-id="d1eb8-248">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-248">There is no action item for you in this section.</span></span> <span data-ttu-id="d1eb8-249">Hightail 支援以自訂宣告為基礎的 just-in-time 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-249">Hightail supports just-in-time user provisioning based on the custom claims.</span></span> <span data-ttu-id="d1eb8-250">如果您已如上方 **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** 一節中所示設定自訂宣告，會在尚未存在使用者的應用程式中自動建立使用者。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-250">If you have configured the custom claims as shown in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** above, a user is automatically created in the application it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="d1eb8-251">如果您需要手動建立使用者，您必須透過 [Hightail 支援小組](mailto:support@hightail.com)。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-251">If you need to create a user manually, you need to contact the [Hightail support team](mailto:support@hightail.com).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d1eb8-252">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d1eb8-252">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d1eb8-253">在本節中，您會將 Hightail 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-253">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hightail.</span></span>

![指派使用者][200] 

<span data-ttu-id="d1eb8-255">**若要將 Britta Simon 指派給 Hightail，請執行以下步驟：**</span><span class="sxs-lookup"><span data-stu-id="d1eb8-255">**To assign Britta Simon to Hightail, perform the following steps:**</span></span>

1. <span data-ttu-id="d1eb8-256">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-256">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d1eb8-258">在應用程式清單中，選取 [Hightail] 。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-258">In the applications list, select **Hightail**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. <span data-ttu-id="d1eb8-260">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-260">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d1eb8-262">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-262">Click **Add** button.</span></span> <span data-ttu-id="d1eb8-263">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-263">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d1eb8-265">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-265">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d1eb8-266">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-266">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1eb8-267">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-267">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d1eb8-268">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d1eb8-268">Testing single sign-on</span></span>

<span data-ttu-id="d1eb8-269">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-269">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d1eb8-270">當您在存取面板中按一下 [Hightail] 圖格時，應該會自動登入您的 Hightail 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1eb8-270">When you click the Hightail tile in the Access Panel, you should get automatically signed-on to your Hightail application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d1eb8-271">其他資源</span><span class="sxs-lookup"><span data-stu-id="d1eb8-271">Additional resources</span></span>

* [<span data-ttu-id="d1eb8-272">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d1eb8-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1eb8-273">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d1eb8-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

