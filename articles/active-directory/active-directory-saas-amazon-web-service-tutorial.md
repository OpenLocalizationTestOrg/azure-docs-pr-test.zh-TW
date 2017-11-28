---
title: "教學課程：Azure Active Directory 與 Amazon Web Services (AWS) 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Amazon Web Services (AWS) 之間。"
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
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a><span data-ttu-id="4627e-103">教學課程：Azure Active Directory 與 Amazon Web Services (AWS) 整合</span><span class="sxs-lookup"><span data-stu-id="4627e-103">Tutorial: Azure Active Directory integration with Amazon Web Services (AWS)</span></span>

<span data-ttu-id="4627e-104">在此教學課程中，您學會如何 toointegrate Amazon Web Services (AWS) 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4627e-104">In this tutorial, you learn how toointegrate Amazon Web Services (AWS) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4627e-105">與 Azure AD 整合 Amazon Web Services (AWS) 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-105">Integrating Amazon Web Services (AWS) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4627e-106">您可以控制存取 tooAmazon Web Services (AWS) 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="4627e-106">You can control in Azure AD who has access tooAmazon Web Services (AWS)</span></span>
- <span data-ttu-id="4627e-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooAmazon Web Services (AWS) （單一登入）</span><span class="sxs-lookup"><span data-stu-id="4627e-107">You can enable your users tooautomatically get signed-on tooAmazon Web Services (AWS) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4627e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4627e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4627e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4627e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="4627e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4627e-110">Prerequisites</span></span>

<span data-ttu-id="4627e-111">tooconfigure Azure AD 整合與 Amazon Web Services (AWS)，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-111">tooconfigure Azure AD integration with Amazon Web Services (AWS), you need hello following items:</span></span>

- <span data-ttu-id="4627e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4627e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4627e-113">已啟用 Amazon Web Services (AWS) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4627e-113">Amazon Web Services (AWS) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4627e-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="4627e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4627e-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4627e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4627e-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="4627e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="4627e-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="4627e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4627e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4627e-118">Scenario description</span></span>
<span data-ttu-id="4627e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4627e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4627e-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="4627e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4627e-121">新增 Amazon Web Services (AWS) 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="4627e-121">Adding Amazon Web Services (AWS) from hello gallery</span></span>
2. <span data-ttu-id="4627e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4627e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a><span data-ttu-id="4627e-123">新增 Amazon Web Services (AWS) 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="4627e-123">Adding Amazon Web Services (AWS) from hello gallery</span></span>
<span data-ttu-id="4627e-124">tooconfigure hello 整合 Amazon Web Services (AWS) 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Amazon Web Services (AWS)。</span><span class="sxs-lookup"><span data-stu-id="4627e-124">tooconfigure hello integration of Amazon Web Services (AWS) into Azure AD, you need tooadd Amazon Web Services (AWS) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4627e-125">**tooadd Amazon Web Services (AWS) 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4627e-125">**tooadd Amazon Web Services (AWS) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4627e-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4627e-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4627e-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4627e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4627e-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4627e-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="4627e-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4627e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="4627e-133">在 [hello] 搜尋方塊中，輸入**Amazon Web Services (AWS)**。</span><span class="sxs-lookup"><span data-stu-id="4627e-133">In hello search box, type **Amazon Web Services (AWS)**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. <span data-ttu-id="4627e-135">在 [hello [結果] 窗格中，選取 [ **Amazon Web Services (AWS)**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627e-135">In hello results panel, select **Amazon Web Services (AWS)**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4627e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4627e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4627e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Amazon Web Services (AWS) 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4627e-138">In this section, you configure and test Azure AD single sign-on with Amazon Web Services (AWS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4627e-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 Amazon Web Services (AWS) 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="4627e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Amazon Web Services (AWS) is tooa user in Azure AD.</span></span> <span data-ttu-id="4627e-140">換句話說，Azure AD 使用者與 hello 相關的使用者在 Amazon Web Services (AWS) 之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="4627e-140">In other words, a link relationship between an Azure AD user and hello related user in Amazon Web Services (AWS) needs toobe established.</span></span>

<span data-ttu-id="4627e-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Amazon Web Services (AWS)。</span><span class="sxs-lookup"><span data-stu-id="4627e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Amazon Web Services (AWS).</span></span>

<span data-ttu-id="4627e-142">tooconfigure 及 Amazon Web Services (AWS) 與 Azure AD 單一登入測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-142">tooconfigure and test Azure AD single sign-on with Amazon Web Services (AWS), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4627e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="4627e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4627e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="4627e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4627e-145">**[建立測試使用者 Amazon Web Services](#creating-an-amazon-web-services-test-user) ** -toohave 許 Simon 在 Amazon Web Services (AWS) 是連結的 toohello Azure AD 的她的表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="4627e-145">**[Creating an Amazon Web Services test user](#creating-an-amazon-web-services-test-user)** - toohave a counterpart of Britta Simon in Amazon Web Services (AWS) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="4627e-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4627e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4627e-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="4627e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4627e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4627e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4627e-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並在 Amazon Web Services (AWS) 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="4627e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Amazon Web Services (AWS) application.</span></span>

<span data-ttu-id="4627e-150">**tooconfigure Azure AD 單一登入與 Amazon Web Services (AWS) 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4627e-150">**tooconfigure Azure AD single sign-on with Amazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="4627e-151">在 hello Azure 網站上 hello **Amazon Web Services (AWS)**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="4627e-151">In hello Azure Portal, on hello **Amazon Web Services (AWS)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="4627e-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4627e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. <span data-ttu-id="4627e-155">在 [hello **Amazon Web Services (AWS) 網域和 Url**區段中，hello 使用者沒有 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627e-155">On hello **Amazon Web Services (AWS) Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. <span data-ttu-id="4627e-157">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="4627e-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. <span data-ttu-id="4627e-159">hello Amazon Web Services (AWS) 的軟體應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="4627e-159">hello Amazon Web Services (AWS) Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="4627e-160">請設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="4627e-160">Please configure hello following claims for this application.</span></span> <span data-ttu-id="4627e-161">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="4627e-161">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="4627e-162">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="4627e-162">hello following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. <span data-ttu-id="4627e-164">在 hello**使用者屬性**區段 hello**單一登入**] 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-164">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="4627e-165">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="4627e-165">Attribute Name</span></span>  | <span data-ttu-id="4627e-166">屬性值</span><span class="sxs-lookup"><span data-stu-id="4627e-166">Attribute Value</span></span> | <span data-ttu-id="4627e-167">命名空間</span><span class="sxs-lookup"><span data-stu-id="4627e-167">Namespace</span></span> |
    | --------------- | --------------- | --------------- |
    | <span data-ttu-id="4627e-168">RoleSessionName</span><span class="sxs-lookup"><span data-stu-id="4627e-168">RoleSessionName</span></span> | <span data-ttu-id="4627e-169">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="4627e-169">user.userprincipalname</span></span> | <span data-ttu-id="4627e-170">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="4627e-170">https://aws.amazon.com/SAML/Attributes</span></span> |
    | <span data-ttu-id="4627e-171">角色</span><span class="sxs-lookup"><span data-stu-id="4627e-171">Role</span></span>            | <span data-ttu-id="4627e-172">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="4627e-172">user.assignedroles</span></span> |  <span data-ttu-id="4627e-173">https://aws.amazon.com/SAML/Attributes</span><span class="sxs-lookup"><span data-stu-id="4627e-173">https://aws.amazon.com/SAML/Attributes</span></span> |
    
    >[!TIP]
    ><span data-ttu-id="4627e-174">您需要 tooconfigure hello 使用者佈建在 Azure AD toofetch AWS 主控台全部 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="4627e-174">You need tooconfigure hello user provisioning in Azure AD toofetch all hello roles from AWS Console.</span></span> <span data-ttu-id="4627e-175">請參閱 hello 佈建步驟。</span><span class="sxs-lookup"><span data-stu-id="4627e-175">Please refer hello provisioning steps below.</span></span>

    <span data-ttu-id="4627e-176">a.</span><span class="sxs-lookup"><span data-stu-id="4627e-176">a.</span></span> <span data-ttu-id="4627e-177">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4627e-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="4627e-179">b.</span><span class="sxs-lookup"><span data-stu-id="4627e-179">b.</span></span> <span data-ttu-id="4627e-180">在 [hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="4627e-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4627e-182">c.</span><span class="sxs-lookup"><span data-stu-id="4627e-182">c.</span></span> <span data-ttu-id="4627e-183">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="4627e-183">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="4627e-184">指定上方加入 hello 命名空間值。</span><span class="sxs-lookup"><span data-stu-id="4627e-184">Add hello Namespace value as given above.</span></span>
    
    <span data-ttu-id="4627e-185">d.</span><span class="sxs-lookup"><span data-stu-id="4627e-185">d.</span></span> <span data-ttu-id="4627e-186">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4627e-186">Click **Ok**.</span></span>

7. <span data-ttu-id="4627e-187">按一下**儲存**toosave hello 設定在 Azure 上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4627e-187">Click **Save** button toosave hello settings on Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4627e-189">在不同的瀏覽器視窗中，以系統管理員身分登入 tooyour Amazon Web Services (AWS) 公司網站。</span><span class="sxs-lookup"><span data-stu-id="4627e-189">In a different browser window, sign-on tooyour Amazon Web Services (AWS) company site as administrator.</span></span>

9. <span data-ttu-id="4627e-190">按一下 [主控台首頁] 。</span><span class="sxs-lookup"><span data-stu-id="4627e-190">Click **Console Home**.</span></span>
   
    ![設定單一登入][11]

10. <span data-ttu-id="4627e-192">從 [安全性、身分識別與合規性] 服務按一下 [IAM]。</span><span class="sxs-lookup"><span data-stu-id="4627e-192">Click **IAM** from **Security, Identity & Compliance** service.</span></span>
   
    ![設定單一登入][12]

11. <span data-ttu-id="4627e-194">按一下 [識別提供者]，然後按一下 [建立提供者]。</span><span class="sxs-lookup"><span data-stu-id="4627e-194">Click **Identity Providers**, and then click **Create Provider**.</span></span>
   
    ![設定單一登入][13]

12. <span data-ttu-id="4627e-196">在 [hello**設定提供者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-196">On hello **Configure Provider** dialog page, perform hello following steps:</span></span>
   
    ![設定單一登入][14]
 
    <span data-ttu-id="4627e-198">a.</span><span class="sxs-lookup"><span data-stu-id="4627e-198">a.</span></span> <span data-ttu-id="4627e-199">針對 [提供者類型]，選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="4627e-199">As **Provider Type**, select **SAML**.</span></span>

    <span data-ttu-id="4627e-200">b.</span><span class="sxs-lookup"><span data-stu-id="4627e-200">b.</span></span> <span data-ttu-id="4627e-201">在 [hello**提供者名稱**文字方塊中，輸入提供者名稱 (例如： *WAAD*)。</span><span class="sxs-lookup"><span data-stu-id="4627e-201">In hello **Provider Name** textbox, type a provider name (e.g.: *WAAD*).</span></span>

    <span data-ttu-id="4627e-202">c.</span><span class="sxs-lookup"><span data-stu-id="4627e-202">c.</span></span> <span data-ttu-id="4627e-203">tooupload 您下載的中繼資料檔案中，按一下 [**選擇檔案**。</span><span class="sxs-lookup"><span data-stu-id="4627e-203">tooupload your downloaded metadata file, click **Choose File**.</span></span>

    <span data-ttu-id="4627e-204">d.</span><span class="sxs-lookup"><span data-stu-id="4627e-204">d.</span></span> <span data-ttu-id="4627e-205">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="4627e-205">Click **Next Step**.</span></span>

13. <span data-ttu-id="4627e-206">在 [hello**驗證提供者資訊**對話方塊頁面上，按一下 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="4627e-206">On hello **Verify Provider Information** dialog page, click **Create**.</span></span> 
    
    ![設定單一登入][15]

14. <span data-ttu-id="4627e-208">按一下 [角色]，然後按一下 [建立新角色]。</span><span class="sxs-lookup"><span data-stu-id="4627e-208">Click **Roles**, and then click **Create New Role**.</span></span> 
    
    ![設定單一登入][16]

15. <span data-ttu-id="4627e-210">在 [hello**設定角色名稱**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-210">On hello **Set Role Name** dialog, perform hello following steps:</span></span> 
    
    ![設定單一登入][17] 

    <span data-ttu-id="4627e-212">a.</span><span class="sxs-lookup"><span data-stu-id="4627e-212">a.</span></span> <span data-ttu-id="4627e-213">在 [hello**角色名稱**文字方塊中，輸入角色名稱 (例如： *TestUser*)。</span><span class="sxs-lookup"><span data-stu-id="4627e-213">In hello **Role Name** textbox, type a role name (e.g.: *TestUser*).</span></span> 

    <span data-ttu-id="4627e-214">b.</span><span class="sxs-lookup"><span data-stu-id="4627e-214">b.</span></span> <span data-ttu-id="4627e-215">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="4627e-215">Click **Next Step**.</span></span>

16. <span data-ttu-id="4627e-216">在 [hello**選取角色類型**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-216">On hello **Select Role Type** dialog, perform hello following steps:</span></span> 
    
    ![設定單一登入][18] 

    <span data-ttu-id="4627e-218">a.</span><span class="sxs-lookup"><span data-stu-id="4627e-218">a.</span></span> <span data-ttu-id="4627e-219">選取 [識別提供者存取的角色]。</span><span class="sxs-lookup"><span data-stu-id="4627e-219">Select **Role For Identity Provider Access**.</span></span> 

    <span data-ttu-id="4627e-220">b.</span><span class="sxs-lookup"><span data-stu-id="4627e-220">b.</span></span> <span data-ttu-id="4627e-221">在 [hello**授與網頁單一登入 (WebSSO) 存取 tooSAML 提供者**區段中，按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="4627e-221">In hello **Grant Web Single Sign-On (WebSSO) access tooSAML providers** section, click **Select**.</span></span>

17. <span data-ttu-id="4627e-222">在 [hello**建立信任**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-222">On hello **Establish Trust** dialog, perform hello following steps:</span></span>  
    
    ![設定單一登入][19] 

    <span data-ttu-id="4627e-224">a.</span><span class="sxs-lookup"><span data-stu-id="4627e-224">a.</span></span> <span data-ttu-id="4627e-225">為 SAML 提供者中，選取您先前建立的 hello SAML 提供者 (例如： *WAAD*)</span><span class="sxs-lookup"><span data-stu-id="4627e-225">As SAML provider, select hello SAML provider you have created previously (e.g.: *WAAD*)</span></span>
  
    <span data-ttu-id="4627e-226">b.</span><span class="sxs-lookup"><span data-stu-id="4627e-226">b.</span></span> <span data-ttu-id="4627e-227">按一下頁面底部的 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="4627e-227">Click **Next Step**.</span></span>

18. <span data-ttu-id="4627e-228">在 [hello**確認角色信任**] 對話方塊中，按一下**下一個步驟**。</span><span class="sxs-lookup"><span data-stu-id="4627e-228">On hello **Verify Role Trust** dialog, click **Next Step**.</span></span>
    
    ![設定單一登入][32]

19. <span data-ttu-id="4627e-230">在 [hello**附加原則**] 對話方塊中，按一下 [**下一個步驟**。</span><span class="sxs-lookup"><span data-stu-id="4627e-230">On hello **Attach Policy** dialog, click **Next Step**.</span></span>
    
    ![設定單一登入][33]

20. <span data-ttu-id="4627e-232">在 [hello**檢閱**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-232">On hello **Review** dialog, perform hello following steps:</span></span>
    
    ![設定單一登入][34]
 
    <span data-ttu-id="4627e-234">a.</span><span class="sxs-lookup"><span data-stu-id="4627e-234">a.</span></span> <span data-ttu-id="4627e-235">按一下 [建立角色]。</span><span class="sxs-lookup"><span data-stu-id="4627e-235">Click **Create Role**.</span></span>

    <span data-ttu-id="4627e-236">b.</span><span class="sxs-lookup"><span data-stu-id="4627e-236">b.</span></span> <span data-ttu-id="4627e-237">建立所需的角色，並將它們對應 toohello 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="4627e-237">Create as many roles as needed and map them toohello Identity Provider.</span></span>

21. <span data-ttu-id="4627e-238">現在設定 hello 使用者佈建 toofetch AWS 全部 hello 角色</span><span class="sxs-lookup"><span data-stu-id="4627e-238">Now configure hello user provisioning toofetch all hello roles from AWS</span></span>

    <span data-ttu-id="4627e-239">a.</span><span class="sxs-lookup"><span data-stu-id="4627e-239">a.</span></span> <span data-ttu-id="4627e-240">使用根帳號的 hello AWS 主控台登入</span><span class="sxs-lookup"><span data-stu-id="4627e-240">In hello AWS Console login with your root account</span></span>

    <span data-ttu-id="4627e-241">b.</span><span class="sxs-lookup"><span data-stu-id="4627e-241">b.</span></span> <span data-ttu-id="4627e-242">在右下角的 hello 頂端按一下您名稱，然後按一下 [hello**我的安全性認證**選項。</span><span class="sxs-lookup"><span data-stu-id="4627e-242">In hello top right corner click your name and then click hello **My Security Credentials** option.</span></span> <span data-ttu-id="4627e-243">這會開啟一個畫面顯示警告訊息。</span><span class="sxs-lookup"><span data-stu-id="4627e-243">This will open up a screen as a warning message.</span></span> <span data-ttu-id="4627e-244">按一下 [hello] 按鈕**安全性認證**按鈕 toopass hello 螢幕。</span><span class="sxs-lookup"><span data-stu-id="4627e-244">Click hello button **Security Credentials** button toopass hello screen.</span></span>
        
       ![設定單一登入][36]

       ![設定單一登入][37]

    <span data-ttu-id="4627e-247">c.</span><span class="sxs-lookup"><span data-stu-id="4627e-247">c.</span></span> <span data-ttu-id="4627e-248">在 [hello 便捷鍵區段按一下 hello**建立新的存取金鑰**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4627e-248">In hello Access Keys section click hello **Create New Access Key** button.</span></span> <span data-ttu-id="4627e-249">這會產生存取金鑰識別碼 hello 和語彙基元的值。</span><span class="sxs-lookup"><span data-stu-id="4627e-249">This generates hello Access Key ID and a token value.</span></span>
    
       ![設定單一登入][38]

    <span data-ttu-id="4627e-251">d.</span><span class="sxs-lookup"><span data-stu-id="4627e-251">d.</span></span> <span data-ttu-id="4627e-252">複製這兩個值，同時加以下載，您才不會遺失它。</span><span class="sxs-lookup"><span data-stu-id="4627e-252">Copy both these values and also download it, so that you don't lose it.</span></span>

    <span data-ttu-id="4627e-253">e.</span><span class="sxs-lookup"><span data-stu-id="4627e-253">e.</span></span> <span data-ttu-id="4627e-254">在 [hello Azure 入口網站中，在 hello Amazon Web Services (AWS) 應用程式整合頁面上，按一下 [**佈建**。</span><span class="sxs-lookup"><span data-stu-id="4627e-254">In hello Azure Portal, on hello Amazon Web Services (AWS) application integration page, click **Provisioning**.</span></span>
        
       ![設定單一登入][35]

    <span data-ttu-id="4627e-256">f.</span><span class="sxs-lookup"><span data-stu-id="4627e-256">f.</span></span> <span data-ttu-id="4627e-257">Hello 佈建模式設定太**自動**</span><span class="sxs-lookup"><span data-stu-id="4627e-257">Set hello Provisioning mode too**Automatic**</span></span>
        
       ![設定單一登入][39]

    <span data-ttu-id="4627e-259">g.</span><span class="sxs-lookup"><span data-stu-id="4627e-259">g.</span></span> <span data-ttu-id="4627e-260">現在在 hello **clientsecret**和**密碼語彙基元**hello 對應值，您從 AWS 主控台] 複製貼上。</span><span class="sxs-lookup"><span data-stu-id="4627e-260">Now in hello **clientsecret** and **Secret Token** paste hello corresponding values, which you have copied from AWS Console.</span></span>
    
    <span data-ttu-id="4627e-261">h.</span><span class="sxs-lookup"><span data-stu-id="4627e-261">h.</span></span> <span data-ttu-id="4627e-262">您可以按一下 hello**測試連接**按鈕 tootest hello 連線。</span><span class="sxs-lookup"><span data-stu-id="4627e-262">You can click hello **Test Connection** button tootest hello connectivity.</span></span> <span data-ttu-id="4627e-263">一旦成功，就可以開始佈建連接器 hello。</span><span class="sxs-lookup"><span data-stu-id="4627e-263">Once that is successful then you can start hello provisioning connector.</span></span>
       
       ![設定單一登入][40]

    <span data-ttu-id="4627e-265">i.</span><span class="sxs-lookup"><span data-stu-id="4627e-265">i.</span></span> <span data-ttu-id="4627e-266">現在啟用 hello 佈建狀態太**上**。</span><span class="sxs-lookup"><span data-stu-id="4627e-266">Now enable hello Provisioning Status too**On**.</span></span> <span data-ttu-id="4627e-267">這樣會啟動擷取 hello 角色從 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627e-267">This starts fetching hello roles from hello application.</span></span>

       ![設定單一登入][41]

    > [!NOTE]
    > <span data-ttu-id="4627e-269">執行 azure AD 佈建服務每個從 AWS 某些時間 toosync hello 角色之後。</span><span class="sxs-lookup"><span data-stu-id="4627e-269">Azure AD Provisioning service runs every after some time toosync hello roles from AWS.</span></span> <span data-ttu-id="4627e-270">您應該會看到所有 hello 身分識別提供者都連接至 Azure AD AWS 角色，而且您可以指派 hello 應用程式 toousers 或群組時使用它們。</span><span class="sxs-lookup"><span data-stu-id="4627e-270">You should see all hello Identity Provider attached AWS roles into Azure AD and you can use them while assigning hello application toousers or groups.</span></span>

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4627e-271">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4627e-271">Creating an Azure AD test user</span></span>
<span data-ttu-id="4627e-272">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4627e-272">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="4627e-274">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4627e-274">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4627e-275">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4627e-275">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4627e-277">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="4627e-277">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4627e-279">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4627e-279">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4627e-281">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-281">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4627e-283">a.</span><span class="sxs-lookup"><span data-stu-id="4627e-283">a.</span></span> <span data-ttu-id="4627e-284">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4627e-284">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4627e-285">b.</span><span class="sxs-lookup"><span data-stu-id="4627e-285">b.</span></span> <span data-ttu-id="4627e-286">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="4627e-286">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4627e-287">c.</span><span class="sxs-lookup"><span data-stu-id="4627e-287">c.</span></span> <span data-ttu-id="4627e-288">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="4627e-288">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4627e-289">d.</span><span class="sxs-lookup"><span data-stu-id="4627e-289">d.</span></span> <span data-ttu-id="4627e-290">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4627e-290">Click **Create**.</span></span>
 
### <a name="creating-an-amazon-web-services-test-user"></a><span data-ttu-id="4627e-291">建立 Amazon Web Services 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4627e-291">Creating an Amazon Web Services test user</span></span>

<span data-ttu-id="4627e-292">在訂單 tooenable Azure AD 使用者 toolog tooAmazon Web Services (AWS) 中，它們必須佈建到 Amazon Web Services (AWS)。</span><span class="sxs-lookup"><span data-stu-id="4627e-292">In order tooenable Azure AD users toolog in tooAmazon Web Services (AWS), they must be provisioned into Amazon Web Services (AWS).</span></span> <span data-ttu-id="4627e-293">在 hello 案例 Amazon Web Services (AWS) 中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="4627e-293">In hello case of Amazon Web Services (AWS), provisioning is a manual task.</span></span>

<span data-ttu-id="4627e-294">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4627e-294">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4627e-295">登入 tooyour **Amazon Web Services (AWS)**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="4627e-295">Log in tooyour **Amazon Web Services (AWS)** company site as administrator.</span></span>

2. <span data-ttu-id="4627e-296">按一下 hello**主控台首頁**圖示。</span><span class="sxs-lookup"><span data-stu-id="4627e-296">Click hello **Console Home** icon.</span></span> 
   
    ![設定單一登入][11]

3. <span data-ttu-id="4627e-298">按一下 [身分識別與存取管理]。</span><span class="sxs-lookup"><span data-stu-id="4627e-298">Click Identity and Access Management.</span></span> 
   
    ![設定單一登入][28]

4. <span data-ttu-id="4627e-300">在 [hello 儀表板，按一下 [**使用者**，然後按一下 [**建立新的使用者**。</span><span class="sxs-lookup"><span data-stu-id="4627e-300">In hello Dashboard, click **Users**, and then click **Create New Users**.</span></span> 
   
    ![設定單一登入][29]

5. <span data-ttu-id="4627e-302">Hello 建立使用者在對話方塊上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4627e-302">On hello Create User dialog, perform hello following steps:</span></span> 
   
    ![設定單一登入][30]   
    
    <span data-ttu-id="4627e-304">a.</span><span class="sxs-lookup"><span data-stu-id="4627e-304">a.</span></span> <span data-ttu-id="4627e-305">在 [hello**輸入使用者名稱**等文字方塊中，輸入 Brita Simon 的使用者名稱 (userprincipalname) 在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="4627e-305">In hello **Enter User Names** textboxes, type Brita Simon's user name (userprincipalname) in Azure AD.</span></span>

    <span data-ttu-id="4627e-306">b.</span><span class="sxs-lookup"><span data-stu-id="4627e-306">b.</span></span> <span data-ttu-id="4627e-307">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="4627e-307">Click **Create.**</span></span>
        
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4627e-308">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="4627e-308">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4627e-309">在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooAmazon Web Services (AWS)。</span><span class="sxs-lookup"><span data-stu-id="4627e-309">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooAmazon Web Services (AWS).</span></span>

![指派使用者][200] 

<span data-ttu-id="4627e-311">**tooassign 許 Simon tooAmazon Web Services (AWS)，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4627e-311">**tooassign Britta Simon tooAmazon Web Services (AWS), perform hello following steps:**</span></span>

1. <span data-ttu-id="4627e-312">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4627e-312">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4627e-314">在 [hello] 應用程式清單中，選取**Amazon Web Services (AWS)**。</span><span class="sxs-lookup"><span data-stu-id="4627e-314">In hello applications list, select **Amazon Web Services (AWS)**.</span></span>

    ![設定單一登入](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. <span data-ttu-id="4627e-316">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="4627e-316">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="4627e-318">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4627e-318">Click **Add** button.</span></span> <span data-ttu-id="4627e-319">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4627e-319">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="4627e-321">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="4627e-321">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4627e-322">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4627e-322">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4627e-323">在**選取角色**索引標籤，選取 hello hello 使用者適當的角色。</span><span class="sxs-lookup"><span data-stu-id="4627e-323">On **Select Role** tab, select hello appropriate role for hello user.</span></span> <span data-ttu-id="4627e-324">所有這些角色會顯示 hello 角色名稱以及身分識別提供者名稱。</span><span class="sxs-lookup"><span data-stu-id="4627e-324">All these roles are shown with hello role name and identity provider name.</span></span> <span data-ttu-id="4627e-325">如此一來，您可以輕鬆地識別 AWS hello 角色。</span><span class="sxs-lookup"><span data-stu-id="4627e-325">This way you can easily identify hello roles from AWS.</span></span>

8. <span data-ttu-id="4627e-326">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4627e-326">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4627e-327">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4627e-327">Testing single sign-on</span></span>

<span data-ttu-id="4627e-328">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="4627e-328">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4627e-329">當您按一下的 hello Amazon Web Services (AWS) 磚 hello 存取面板中時，您應該取得自動登入 tooyour Amazon Web Services (AWS) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627e-329">When you click hello Amazon Web Services (AWS) tile in hello Access Panel, you should get automatically signed-on tooyour Amazon Web Services (AWS) application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4627e-330">其他資源</span><span class="sxs-lookup"><span data-stu-id="4627e-330">Additional resources</span></span>

* [<span data-ttu-id="4627e-331">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4627e-331">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4627e-332">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4627e-332">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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
