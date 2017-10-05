---
title: "教學課程：Azure Active Directory 與 Amazon Web Services (AWS) 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Amazon Web Services (AWS) 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 0fb9c8f428368271b548e3f174726fa01ea910c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="f67c9-103">教學課程：Azure Active Directory 與 Amazon Web Services (AWS) 整合</span><span class="sxs-lookup"><span data-stu-id="f67c9-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="f67c9-104">在本教學課程中，您將了解如何整合 Amazon Web Services (AWS) 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f67c9-104">In this tutorial, you learn how to integrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f67c9-105">Amazon Web Services (AWS) 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f67c9-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f67c9-106">您可以在 Azure AD 中控制可存取 Amazon Web Services (AWS) 的人員</span><span class="sxs-lookup"><span data-stu-id="f67c9-106">You can control in Azure AD who has access to Amazon Web Services (AWS)</span></span>
- <span data-ttu-id="f67c9-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Amazon Web Services (AWS) (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f67c9-107">You can enable your users to automatically get signed-on to Amazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f67c9-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f67c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f67c9-109">若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f67c9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Amazon Web Services (AWS), it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="f67c9-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f67c9-110">Prerequisites</span></span>

<span data-ttu-id="f67c9-111">若要設定 Azure AD 與 Amazon Web Services (AWS) 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f67c9-111">To configure Azure AD integration with Amazon Web Services (AWS), you need the following items:</span></span>

- <span data-ttu-id="f67c9-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f67c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f67c9-113">已啟用 Amazon Web Services (AWS) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f67c9-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f67c9-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f67c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f67c9-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f67c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f67c9-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="f67c9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f67c9-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f67c9-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f67c9-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f67c9-118">Scenario description</span></span>
<span data-ttu-id="f67c9-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f67c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f67c9-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f67c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f67c9-121">從資源庫新增 Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="f67c9-121">Adding Amazon Web Services (AWS) from the gallery</span></span>
2. <span data-ttu-id="f67c9-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f67c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-the-gallery"></a><span data-ttu-id="f67c9-123">從資源庫新增 Amazon Web Services (AWS)</span><span class="sxs-lookup"><span data-stu-id="f67c9-123">Adding Amazon Web Services (AWS) from the gallery</span></span>
<span data-ttu-id="f67c9-124">若要設定 Amazon Web Services (AWS) 與 Azure AD 整合，您需要從資源庫將 Amazon Web Services (AWS) 新增到受管理的 SaaS App 清單。</span><span class="sxs-lookup"><span data-stu-id="f67c9-124">To configure the integration of Amazon Web Services (AWS) into Azure AD, you need to add Amazon Web Services (AWS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f67c9-125">**若要從資源庫新增 Amazon Web Services (AWS)，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f67c9-125">**To add Amazon Web Services (AWS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f67c9-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f67c9-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f67c9-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f67c9-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f67c9-131">按一下對話方塊頂端的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f67c9-131">Click **Add** button on the top of the dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f67c9-133">在搜尋方塊中，輸入 **Amazon Web Services (AWS)**。</span><span class="sxs-lookup"><span data-stu-id="f67c9-133">In the search box, type **Amazon Web Services (AWS)**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="f67c9-135">在結果窗格中，選取 [Amazon Web Services (AWS)]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f67c9-135">In the results panel, select **Amazon Web Services (AWS)**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f67c9-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f67c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f67c9-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Amazon Web Services (AWS) 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f67c9-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f67c9-139">若要讓單一登入運作，Azure AD 必須知道 Amazon Web Services (AWS) 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f67c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Amazon Web Services (AWS) is to a user in Azure AD.</span></span> <span data-ttu-id="f67c9-140">換句話說，必須在 Azure AD 使用者和 Amazon Web Services (AWS) 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f67c9-140">In other words, a link relationship between an Azure AD user and the related user in Amazon Web Services (AWS) needs to be established.</span></span>

<span data-ttu-id="f67c9-141">建立此連結關聯性的方法是將 Azure AD 中**使用者名稱**的值指定為 Amazon Web Services (AWS) 中 **Username** 的值。</span><span class="sxs-lookup"><span data-stu-id="f67c9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="f67c9-142">若要使用 Amazon Web Services (AWS) 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="f67c9-142">To configure and test Azure AD single sign-on with Amazon Web Services (AWS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f67c9-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f67c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f67c9-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f67c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f67c9-145">**[建立 Amazon Web Services 測試使用者](#creating-an-amazon-web-services-test-user)** - 使 Amazon Web Services (AWS) 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="f67c9-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - to have a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f67c9-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f67c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f67c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f67c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f67c9-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f67c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f67c9-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Amazon Web Services (AWS) 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f67c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="f67c9-150">**若要使用 Amazon Web Services (AWS) 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f67c9-150">**To configure Azure AD single sign-on with Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="f67c9-151">在 Azure 入口網站的 [Amazon Web Services (AWS)] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-151">In the Azure Portal, on the **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f67c9-153">在 [單一登入] 對話方塊上，選取 [以 SAML 為基礎的登入] 作為 [模式]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f67c9-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="f67c9-155">在 [Amazon Web Services (AWS) 網域和 URL] 區段中，使用者不需要執行任何步驟，因為應用程式已經與 Azure 預先整合。</span><span class="sxs-lookup"><span data-stu-id="f67c9-155">On the **Amazon Web Services (AWS) Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="f67c9-157">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f67c9-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="f67c9-159">Amazon Web Services (AWS) 軟體應用程式預期要有特定格式的 SAML 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="f67c9-159">The Amazon Web Services (AWS) Software application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="f67c9-160">請設定此應用程式的下列宣告。</span><span class="sxs-lookup"><span data-stu-id="f67c9-160">Please configure the following claims for this application.</span></span> <span data-ttu-id="f67c9-161">您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f67c9-161">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="f67c9-162">以下螢幕擷取畫面顯示上述的範例。</span><span class="sxs-lookup"><span data-stu-id="f67c9-162">The following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="f67c9-164">在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如上圖所示設定 SAML 權杖屬性，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f67c9-164">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="f67c9-165">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="f67c9-165">Attribute Name</span></span>  | <span data-ttu-id="f67c9-166">屬性值</span><span class="sxs-lookup"><span data-stu-id="f67c9-166">Attribute Value</span></span> | <span data-ttu-id="f67c9-167">命名空間</span><span class="sxs-lookup"><span data-stu-id="f67c9-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="f67c9-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="f67c9-168">RoleSessionName</span></span> | <span data-ttu-id="f67c9-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="f67c9-169">user.userprincipalname</span></span> | <span data-ttu-id="f67c9-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="f67c9-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="f67c9-171">角色</span><span class="sxs-lookup"><span data-stu-id="f67c9-171">Role</span></span>            | <span data-ttu-id="f67c9-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="f67c9-172">user.assignedroles</span></span> |  <span data-ttu-id="f67c9-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="f67c9-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="f67c9-174">您需要設定在 Azure AD 中的使用者佈建，以從 AWS 主控台擷取所有角色。</span><span class="sxs-lookup"><span data-stu-id="f67c9-174">You need to configure the user provisioning in Azure AD to fetch all the roles from AWS Console.</span></span> <span data-ttu-id="f67c9-175">請參閱下面的佈建步驟。</span><span class="sxs-lookup"><span data-stu-id="f67c9-175">Please refer the provisioning steps below.</span></span>

    <span data-ttu-id="f67c9-176">a.</span><span class="sxs-lookup"><span data-stu-id="f67c9-176">a.</span></span> <span data-ttu-id="f67c9-177">按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f67c9-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="f67c9-179">b.</span><span class="sxs-lookup"><span data-stu-id="f67c9-179">b.</span></span> <span data-ttu-id="f67c9-180">在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="f67c9-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f67c9-182">c.</span><span class="sxs-lookup"><span data-stu-id="f67c9-182">c.</span></span> <span data-ttu-id="f67c9-183">在 [值] 清單中，選取該列所顯示的值。</span><span class="sxs-lookup"><span data-stu-id="f67c9-183">From the **Value** list, type the attribute value shown for that row.</span></span> <span data-ttu-id="f67c9-184">如上所述新增 [命名空間] 值。</span><span class="sxs-lookup"><span data-stu-id="f67c9-184">Add the Namespace value as given above.</span></span>
    
    <span data-ttu-id="f67c9-185">d.</span><span class="sxs-lookup"><span data-stu-id="f67c9-185">d.</span></span> <span data-ttu-id="f67c9-186">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f67c9-186">Click **Ok**.</span></span>

7. <span data-ttu-id="f67c9-187">按一下 [儲存] 按鈕以在 Azure 上儲存設定。</span><span class="sxs-lookup"><span data-stu-id="f67c9-187">Click **Save** button to save the settings on Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="f67c9-189">在不同的瀏覽器視窗中，以系統管理員身分登入您的 Amazon Web Services (AWS) 公司網站。</span><span class="sxs-lookup"><span data-stu-id="f67c9-189">In a different browser window, sign-on to your Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="f67c9-190">按一下 [主控台首頁] 。</span><span class="sxs-lookup"><span data-stu-id="f67c9-190">Click **Console Home**.</span></span>
   
    ![設定單一登入][11]

10. <span data-ttu-id="f67c9-192">從 [安全性、身分識別與合規性] 服務按一下 [IAM]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![設定單一登入][12]

11. <span data-ttu-id="f67c9-194">按一下 [識別提供者]，然後按一下 [建立提供者]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![設定單一登入][13]

12. <span data-ttu-id="f67c9-196">在 [設定提供者]  對話方塊頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f67c9-196">On the **Configure Provider** dialog page, perform the following steps:</span></span>
   
    ![設定單一登入][14]
 
    <span data-ttu-id="f67c9-198">a.</span><span class="sxs-lookup"><span data-stu-id="f67c9-198">a.</span></span> <span data-ttu-id="f67c9-199">針對 [提供者類型]，選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="f67c9-200">b.</span><span class="sxs-lookup"><span data-stu-id="f67c9-200">b.</span></span> <span data-ttu-id="f67c9-201">在 [提供者名稱] 文字方塊中，輸入提供者名稱 (例如：*WAAD*)。</span><span class="sxs-lookup"><span data-stu-id="f67c9-201">In the **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="f67c9-202">c.</span><span class="sxs-lookup"><span data-stu-id="f67c9-202">c.</span></span> <span data-ttu-id="f67c9-203">若要上傳您下載的中繼資料檔，請按一下 [選擇檔案]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-203">To upload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="f67c9-204">d.</span><span class="sxs-lookup"><span data-stu-id="f67c9-204">d.</span></span> <span data-ttu-id="f67c9-205">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f67c9-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="f67c9-206">在 [驗證提供者資訊] 對話方塊頁面上，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-206">On the **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![設定單一登入][15]

14. <span data-ttu-id="f67c9-208">按一下 [角色]，然後按一下 [建立新角色]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![設定單一登入][16]

15. <span data-ttu-id="f67c9-210">在 [設定角色名稱]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f67c9-210">On the **Set Role Name** dialog, perform the following steps:</span></span> 
    
    ![設定單一登入][17] 

    <span data-ttu-id="f67c9-212">a.</span><span class="sxs-lookup"><span data-stu-id="f67c9-212">a.</span></span> <span data-ttu-id="f67c9-213">在 [角色名稱] 文字方塊中，輸入角色名稱 (例如：*TestUser*)。</span><span class="sxs-lookup"><span data-stu-id="f67c9-213">In the **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="f67c9-214">b.</span><span class="sxs-lookup"><span data-stu-id="f67c9-214">b.</span></span> <span data-ttu-id="f67c9-215">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f67c9-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="f67c9-216">在 [選取角色類型]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f67c9-216">On the **Select Role Type** dialog, perform the following steps:</span></span> 
    
    ![設定單一登入][18] 

    <span data-ttu-id="f67c9-218">a.</span><span class="sxs-lookup"><span data-stu-id="f67c9-218">a.</span></span> <span data-ttu-id="f67c9-219">選取 [識別提供者存取的角色]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="f67c9-220">b.</span><span class="sxs-lookup"><span data-stu-id="f67c9-220">b.</span></span> <span data-ttu-id="f67c9-221">在 [授與 SAML 提供者的 Web 單一登入 (WebSSO) 存取] 區段中，按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-221">In the **Grant Web Single Sign-On (WebSSO) access to SAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="f67c9-222">在 [建立信任]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f67c9-222">On the **Establish Trust** dialog, perform the following steps:</span></span>  
    
    ![設定單一登入][19] 

    <span data-ttu-id="f67c9-224">a.</span><span class="sxs-lookup"><span data-stu-id="f67c9-224">a.</span></span> <span data-ttu-id="f67c9-225">針對 SAML 提供者，請選取您先前建立的 SAML 提供者 (例如：WAAD)</span><span class="sxs-lookup"><span data-stu-id="f67c9-225">As SAML provider, select the SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="f67c9-226">b.</span><span class="sxs-lookup"><span data-stu-id="f67c9-226">b.</span></span> <span data-ttu-id="f67c9-227">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f67c9-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="f67c9-228">在 [確認角色信任] 對話方塊上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-228">On the **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![設定單一登入][32]

19. <span data-ttu-id="f67c9-230">在 [附加原則] 對話方塊上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-230">On the **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![設定單一登入][33]

20. <span data-ttu-id="f67c9-232">在 [檢閱]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f67c9-232">On the **Review** dialog, perform the following steps:</span></span>
    
    ![設定單一登入][34]
 
    <span data-ttu-id="f67c9-234">a.</span><span class="sxs-lookup"><span data-stu-id="f67c9-234">a.</span></span> <span data-ttu-id="f67c9-235">按一下 [建立角色]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-235">Click **Create Role**.</span></span>

    <span data-ttu-id="f67c9-236">b.</span><span class="sxs-lookup"><span data-stu-id="f67c9-236">b.</span></span> <span data-ttu-id="f67c9-237">建立所需數量的角色，並將它們對應至識別提供者。</span><span class="sxs-lookup"><span data-stu-id="f67c9-237">Create as many roles as needed and map them to the Identity Provider.</span></span>

21. <span data-ttu-id="f67c9-238">立即設定使用者佈建，以從 AWS 擷取所有角色。</span><span class="sxs-lookup"><span data-stu-id="f67c9-238">Now configure the user provisioning to fetch all the roles from AWS</span></span>

    <span data-ttu-id="f67c9-239">a.</span><span class="sxs-lookup"><span data-stu-id="f67c9-239">a.</span></span> <span data-ttu-id="f67c9-240">在 AWS 主控台中使用您的根帳戶登入</span><span class="sxs-lookup"><span data-stu-id="f67c9-240">In the AWS Console login with your root account</span></span>

    <span data-ttu-id="f67c9-241">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f67c9-241">b.</span></span> <span data-ttu-id="f67c9-242">在右上角按一下您的名稱，然後按一下 [我的安全性認證] 選項。</span><span class="sxs-lookup"><span data-stu-id="f67c9-242">In the top right corner click your name and then click the **My Security Credentials** option.</span></span> <span data-ttu-id="f67c9-243">這會開啟一個畫面顯示警告訊息。</span><span class="sxs-lookup"><span data-stu-id="f67c9-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="f67c9-244">按一下 [安全性認證] 按鈕以通過此畫面。</span><span class="sxs-lookup"><span data-stu-id="f67c9-244">Click the button **Security Credentials** button to pass the screen.</span></span>
        
       ![設定單一登入][36]

       ![設定單一登入][37]

    <span data-ttu-id="f67c9-247">c.</span><span class="sxs-lookup"><span data-stu-id="f67c9-247">c.</span></span> <span data-ttu-id="f67c9-248">在 [存取金鑰] 區段中按一下 [建立新的存取金鑰] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f67c9-248">In the Access Keys section click the **Create New Access Key** button.</span></span> <span data-ttu-id="f67c9-249">這會產生存取金鑰識別碼和權杖值。</span><span class="sxs-lookup"><span data-stu-id="f67c9-249">This generates the Access Key ID and a token value.</span></span>
    
       ![設定單一登入][38]

    <span data-ttu-id="f67c9-251">d.</span><span class="sxs-lookup"><span data-stu-id="f67c9-251">d.</span></span> <span data-ttu-id="f67c9-252">複製這兩個值，同時加以下載，您才不會遺失它。</span><span class="sxs-lookup"><span data-stu-id="f67c9-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="f67c9-253">e.</span><span class="sxs-lookup"><span data-stu-id="f67c9-253">e.</span></span> <span data-ttu-id="f67c9-254">在 Azure 入口網站的 [Amazon Web Services (AWS)] 應用程式整合頁面上，按一下 [佈建]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-254">In the Azure Portal, on the Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![設定單一登入][35]

    <span data-ttu-id="f67c9-256">f.</span><span class="sxs-lookup"><span data-stu-id="f67c9-256">f.</span></span> <span data-ttu-id="f67c9-257">將 [佈建模式] 設定為 [自動]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-257">Set the Provisioning mode to **Automatic**</span></span>
        
       ![設定單一登入][39]

    <span data-ttu-id="f67c9-259">g.</span><span class="sxs-lookup"><span data-stu-id="f67c9-259">g.</span></span> <span data-ttu-id="f67c9-260">現在於 [clientsecret] 和 [祕密權杖] 中，貼上您從 AWS 主控台複製的對應值。</span><span class="sxs-lookup"><span data-stu-id="f67c9-260">Now in the **clientsecret** and **Secret Token** paste the corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="f67c9-261">h.</span><span class="sxs-lookup"><span data-stu-id="f67c9-261">h.</span></span> <span data-ttu-id="f67c9-262">您可以按一下 [測試連線] 按鈕來測試連線能力。</span><span class="sxs-lookup"><span data-stu-id="f67c9-262">You can click the **Test Connection** button to test the connectivity.</span></span> <span data-ttu-id="f67c9-263">一旦成功，您就可以啟動佈建連接器。</span><span class="sxs-lookup"><span data-stu-id="f67c9-263">Once that is successful then you can start the provisioning connector.</span></span>
       
       ![設定單一登入][40]

    <span data-ttu-id="f67c9-265">i.</span><span class="sxs-lookup"><span data-stu-id="f67c9-265">i.</span></span> <span data-ttu-id="f67c9-266">現在讓 [佈建狀態] 設定為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-266">Now enable the Provisioning Status to **On**.</span></span> <span data-ttu-id="f67c9-267">這會開始從應用程式擷取角色。</span><span class="sxs-lookup"><span data-stu-id="f67c9-267">This starts fetching the roles from the application.</span></span>

       ![設定單一登入][41]

    > [!NOTE]
    > <span data-ttu-id="f67c9-269">Azure AD 佈建服務會每隔一段時間執行一次，以從 AWS 同步處理角色。</span><span class="sxs-lookup"><span data-stu-id="f67c9-269">Azure AD Provisioning service runs every after some time to sync the roles from AWS.</span></span> <span data-ttu-id="f67c9-270">您應該會看到 Azure AD 中所有識別提供者附加的 AWS 角色，而且您可以在將應用程式指派給使用者或群組時使用這些角色。</span><span class="sxs-lookup"><span data-stu-id="f67c9-270">You should see all the Identity Provider attached AWS roles into Azure AD and you can use them while assigning the application to users or groups.</span></span>

<!--### Next steps

To ensure users can sign-in to Amazon Web Services (AWS) after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Amazon Web Services (AWS) in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f67c9-271">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f67c9-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="f67c9-272">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f67c9-272">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f67c9-274">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f67c9-274">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f67c9-275">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f67c9-275">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f67c9-277">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="f67c9-277">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f67c9-279">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f67c9-279">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f67c9-281">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f67c9-281">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f67c9-283">a.</span><span class="sxs-lookup"><span data-stu-id="f67c9-283">a.</span></span> <span data-ttu-id="f67c9-284">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f67c9-284">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f67c9-285">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f67c9-285">b.</span></span> <span data-ttu-id="f67c9-286">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f67c9-286">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f67c9-287">c.</span><span class="sxs-lookup"><span data-stu-id="f67c9-287">c.</span></span> <span data-ttu-id="f67c9-288">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f67c9-288">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f67c9-289">d.</span><span class="sxs-lookup"><span data-stu-id="f67c9-289">d.</span></span> <span data-ttu-id="f67c9-290">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f67c9-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="f67c9-291">建立 Amazon Web Services 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f67c9-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="f67c9-292">若要讓 Azure AD 使用者能夠登入 Amazon Web Services (AWS)，必須將他們佈建到 Amazon Web Services (AWS) 中。</span><span class="sxs-lookup"><span data-stu-id="f67c9-292">In order to enable Azure AD users to log in to Amazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="f67c9-293">Amazon Web Services (AWS) 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="f67c9-293">In the case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="f67c9-294">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f67c9-294">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f67c9-295">以系統管理員身分登入您的 **Amazon Web Services (AWS)** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="f67c9-295">Log in to your **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="f67c9-296">按一下 [主控台首頁]  圖示。</span><span class="sxs-lookup"><span data-stu-id="f67c9-296">Click the **Console Home** icon.</span></span> 
   
    ![設定單一登入][11]

3. <span data-ttu-id="f67c9-298">按一下 [身分識別與存取管理]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-298">Click Identity and Access Management.</span></span> 
   
    ![設定單一登入][28]

4. <span data-ttu-id="f67c9-300">在儀表板中，按一下 [使用者]，然後按一下 [建立新使用者]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-300">In the Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![設定單一登入][29]

5. <span data-ttu-id="f67c9-302">在 [建立使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f67c9-302">On the Create User dialog, perform the following steps:</span></span> 
   
    ![設定單一登入][30]   
    
    <span data-ttu-id="f67c9-304">a.</span><span class="sxs-lookup"><span data-stu-id="f67c9-304">a.</span></span> <span data-ttu-id="f67c9-305">在 [輸入使用者名稱] 文字方塊中，輸入 Brita Simon 在 Azure AD 中的使用者名稱 (userprincipalname)。</span><span class="sxs-lookup"><span data-stu-id="f67c9-305">In the **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="f67c9-306">b.</span><span class="sxs-lookup"><span data-stu-id="f67c9-306">b.</span></span> <span data-ttu-id="f67c9-307">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-307">Click **Create.**</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f67c9-308">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f67c9-308">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f67c9-309">在本節中，您會將 Amazon Web Services (AWS) 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f67c9-309">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Amazon Web Services (AWS).</span></span>

![指派使用者][200] 

<span data-ttu-id="f67c9-311">**若要將 Britta Simon 指派給 Amazon Web Services (AWS)，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f67c9-311">**To assign Britta Simon to Amazon Web Services (AWS), perform the following steps:**</span></span>

1. <span data-ttu-id="f67c9-312">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-312">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f67c9-314">在應用程式清單中，選取 [Amazon Web Services (AWS)] 。</span><span class="sxs-lookup"><span data-stu-id="f67c9-314">In the applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="f67c9-316">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-316">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f67c9-318">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f67c9-318">Click **Add** button.</span></span> <span data-ttu-id="f67c9-319">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f67c9-321">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f67c9-321">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f67c9-322">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f67c9-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f67c9-323">在 [選取角色] 索引標籤上，為使用者選取適當的角色。</span><span class="sxs-lookup"><span data-stu-id="f67c9-323">On **Select Role** tab, select the appropriate role for the user.</span></span> <span data-ttu-id="f67c9-324">所有角色都會以角色名稱和識別提供者名稱顯示。</span><span class="sxs-lookup"><span data-stu-id="f67c9-324">All these roles are shown with the role name and identity provider name.</span></span> <span data-ttu-id="f67c9-325">如此一來，您可以輕鬆地從 AWS 識別角色。</span><span class="sxs-lookup"><span data-stu-id="f67c9-325">This way you can easily identify the roles from AWS.</span></span>

8. <span data-ttu-id="f67c9-326">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f67c9-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f67c9-327">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f67c9-327">Testing single sign-on</span></span>

<span data-ttu-id="f67c9-328">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="f67c9-328">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f67c9-329">當您在存取面板中按一下 [Amazon Web Services (AWS)] 圖格時，應該會自動登入您的 Amazon Web 服務 (AWS) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f67c9-329">When you click the Amazon Web Services (AWS) tile in the Access Panel, you should get automatically signed-on to your Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f67c9-330">其他資源</span><span class="sxs-lookup"><span data-stu-id="f67c9-330">Additional resources</span></span>

* [<span data-ttu-id="f67c9-331">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f67c9-331">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f67c9-332">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f67c9-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
