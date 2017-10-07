---
title: "教學課程：Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 整合 | Microsoft Docs"
description: "了解如何 tooconfigure 單一登入 Azure Active Directory 之間，以及 SAP HANA 雲端平台身分識別驗證。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="c854a-103">教學課程：Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 整合</span><span class="sxs-lookup"><span data-stu-id="c854a-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="c854a-104">在此教學課程中，您學習如何 toointegrate SAP HANA 雲端平台與 Azure Active Directory (Azure AD) 的身分識別驗證。</span><span class="sxs-lookup"><span data-stu-id="c854a-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c854a-105">SAP HANA 雲端平台身分識別驗證做為 proxy IdP tooaccess SAP 應用程式使用 Azure AD 作為 hello 主要 IdP。</span><span class="sxs-lookup"><span data-stu-id="c854a-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="c854a-106">SAP HANA 雲端平台身分識別驗證整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="c854a-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c854a-107">您可以控制存取 tooSAP 應用程式的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="c854a-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="c854a-108">您可以啟用您的使用者 tooautomatically get tooSAP 已登入的應用程式單一登入 (SSO) 與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="c854a-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="c854a-109">您可以管理您的帳戶，在單一中央位置-hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="c854a-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="c854a-110">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="c854a-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c854a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="c854a-111">Prerequisites</span></span>

<span data-ttu-id="c854a-112">tooconfigure 與 SAP HANA 雲端平台身分識別驗證的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c854a-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="c854a-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c854a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="c854a-114">已啟用 SSO 的 **SAP HANA Cloud Platform Identity Authentication** 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c854a-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="c854a-115">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="c854a-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="c854a-116">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="c854a-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c854a-117">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="c854a-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c854a-118">如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="c854a-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c854a-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="c854a-119">Scenario description</span></span>
<span data-ttu-id="c854a-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c854a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="c854a-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="c854a-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c854a-122">加入 SAP HANA 雲端平台身分識別驗證從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="c854a-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="c854a-123">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c854a-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="c854a-124">一頭栽進 hello 技術詳細資料之前, 有您要在 toolook 重要 toounderstand hello 概念。</span><span class="sxs-lookup"><span data-stu-id="c854a-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="c854a-125">hello SAP HANA 雲端平台識別身分驗證與 Azure Active Directory 的同盟可讓您跨應用程式或服務受到 AAD （做為 IdP) SAP 應用程式與服務保護的 SAP HANA 雲端平台識別 tooimplement SSO驗證。</span><span class="sxs-lookup"><span data-stu-id="c854a-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="c854a-126">目前，SAP HANA 雲端平台身分識別驗證會做為 Proxy 身分識別提供者的 tooSAP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c854a-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="c854a-127">Azure Active Directory 輪流做為前置身分識別提供者在此安裝程式中的 hello。</span><span class="sxs-lookup"><span data-stu-id="c854a-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="c854a-128">hello 下列圖表將說明這點：</span><span class="sxs-lookup"><span data-stu-id="c854a-128">hello following diagram illustrates this:</span></span>    

![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="c854a-130">透過此設定，您的 SAP HANA Cloud Platform Identity Authentication 租用戶會設定為 Azure Active Directory 中信任的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c854a-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="c854a-131">後續 hello SAP HANA 雲端平台身分識別驗證管理主控台中設定所有的 SAP 應用程式和您想要透過這種方式 tooprotect 服務 ！</span><span class="sxs-lookup"><span data-stu-id="c854a-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="c854a-132">這表示該授權授與存取 tooSAP 應用程式，並服務需求 tootake 置於 SAP HANA 雲端平台身分識別驗證 （做為 Azure Active Directory 中的相對於的 tooconfiguring 授權） 這類安裝程式。</span><span class="sxs-lookup"><span data-stu-id="c854a-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="c854a-133">藉由設定為透過 hello Azure Active Directory Marketplace 應用程式的 SAP HANA 雲端平台身分識別驗證，您不需要設定所需的個別宣告 care of tootake / 需要 tooproduce SAML 判斷提示和轉換SAP 應用程式的有效驗證 token。</span><span class="sxs-lookup"><span data-stu-id="c854a-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="c854a-134">Web SSO 目前只經過這兩個合作夥伴測試。</span><span class="sxs-lookup"><span data-stu-id="c854a-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="c854a-135">應用程式對 API 或 API 對 API 通訊所需的流程應能運作，但尚未經過測試。</span><span class="sxs-lookup"><span data-stu-id="c854a-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="c854a-136">它們會在後續活動中進行測試。</span><span class="sxs-lookup"><span data-stu-id="c854a-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="c854a-137">從 hello 圖庫新增 SAP HANA 雲端平台身分識別驗證</span><span class="sxs-lookup"><span data-stu-id="c854a-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="c854a-138">tooconfigure hello 整合 SAP HANA 雲端平台身分識別驗證至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SAP HANA 雲端平台身分識別驗證。</span><span class="sxs-lookup"><span data-stu-id="c854a-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c854a-139">**tooadd SAP HANA 雲端平台身分識別驗證從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c854a-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c854a-140">在 [hello [ **Azure 管理入口網站**](https://portal.azure.com)，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c854a-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c854a-142">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c854a-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c854a-143">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c854a-143">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="c854a-145">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="c854a-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="c854a-147">在 [hello] 搜尋方塊中，輸入**SAP HANA 雲端平台身分識別驗證**。</span><span class="sxs-lookup"><span data-stu-id="c854a-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="c854a-149">在 [hello [結果] 窗格中，選取 [ **SAP HANA 雲端平台身分識別驗證**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c854a-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c854a-151">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="c854a-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c854a-152">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP HANA Cloud Platform Identity Authentication 設定及測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="c854a-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c854a-153">SSO toowork Azure AD 需要 tooknow hello 對應項目在 SAP HANA 雲端平台身分識別驗證的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="c854a-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="c854a-154">換句話說，Azure AD 使用者與 SAP HANA 雲端平台身分識別驗證中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="c854a-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="c854a-155">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**在 SAP HANA 雲端平台身分識別驗證。</span><span class="sxs-lookup"><span data-stu-id="c854a-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="c854a-156">tooconfigure 及測試與 SAP HANA 雲端平台身分識別驗證 Azure AD SSO，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="c854a-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c854a-157">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="c854a-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c854a-158">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="c854a-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c854a-159">**[建立 SAP HANA 雲端平台身分識別驗證測試使用者](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** -toohave 許 Simon SAP HANA 雲端平台身分識別的驗證連結的 toohello Azure AD 的她的表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="c854a-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c854a-160">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c854a-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c854a-161">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="c854a-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="c854a-162">設定 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c854a-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="c854a-163">在本節中，您可以 hello Azure 管理入口網站中啟用 Azure AD SSO，並設定單一登入 SAP HANA 雲端平台身分識別驗證應用程式中。</span><span class="sxs-lookup"><span data-stu-id="c854a-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="c854a-164">SAP HANA 雲端平台身分識別驗證應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="c854a-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c854a-165">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="c854a-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="c854a-166">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="c854a-166">hello following screenshot shows an example for this.</span></span>

![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="c854a-168">**tooconfigure 與 SAP HANA 雲端平台身分識別驗證，Azure AD SSO 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="c854a-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="c854a-169">在 hello Azure 管理入口網站上 hello **SAP HANA 雲端平台身分識別驗證**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="c854a-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="c854a-171">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="c854a-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入][5]

3. <span data-ttu-id="c854a-173">在 [hello**使用者屬性**區段 hello**單一登入**] 對話方塊中，如果您的 SAP 應用程式預期的屬性，例如"firstName"。</span><span class="sxs-lookup"><span data-stu-id="c854a-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="c854a-174">在 hello SAML token 屬性對話方塊中，加入 hello"firstName"屬性。</span><span class="sxs-lookup"><span data-stu-id="c854a-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="c854a-175">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c854a-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![設定單一登入][6]

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="c854a-178">在 [hello**屬性名稱**文字方塊中，型別 hello 屬性名稱"firstName"。</span><span class="sxs-lookup"><span data-stu-id="c854a-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="c854a-179">從 hello**屬性值**清單，選取 hello"user.givenname"的屬性值。</span><span class="sxs-lookup"><span data-stu-id="c854a-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="c854a-180">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c854a-180">Click **Ok**.</span></span>

4. <span data-ttu-id="c854a-181">在 [hello **SAP HANA 雲端平台識別身分驗證網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c854a-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="c854a-183">在 [hello**登入 URL**文字方塊中，輸入 hello 登入 URL hello SAP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c854a-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="c854a-184">在 [hello**識別碼**文字方塊中，類型 hello 值下列模式：`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="c854a-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="c854a-185">如果您不知道此值，請遵循 hello SAP HANA 雲端平台身分識別驗證文件[SAML 2.0 設定租用戶](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html)。</span><span class="sxs-lookup"><span data-stu-id="c854a-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="c854a-186">在 [hello **SAP HANA 雲端平台身分識別驗證組態**區段中，按一下**設定 SAP HANA 雲端平台身分識別驗證**tooopen**設定登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c854a-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="c854a-187">然後按一下 [上**SAML XML 中繼資料**將 hello 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c854a-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="c854a-190">設定應用程式的 SSO tooget 移 tooSAP HANA 雲端平台身分識別驗證管理主控台。</span><span class="sxs-lookup"><span data-stu-id="c854a-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="c854a-191">hello URL 具有下列模式的 hello:`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="c854a-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="c854a-192">然後，遵循 hello 文件上 SAP HANA 雲端平台身分識別驗證太[設定 Microsoft Azure AD 成為公司身分識別提供者，在 SAP HANA 雲端平台身分識別驗證](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html)。</span><span class="sxs-lookup"><span data-stu-id="c854a-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="c854a-193">在 [hello Azure 管理入口網站中，按一下 [**儲存**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c854a-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="c854a-194">繼續執行下列步驟，只有當您想 tooadd，並針對另一個的 SAP 應用程式啟用 SSO 的 hello。</span><span class="sxs-lookup"><span data-stu-id="c854a-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="c854a-195">重複步驟 hello > 一節 「 加入 SAP HANA 雲端平台身分識別驗證從 hello 組件庫 」 tooadd SAP HANA 雲端平台身分識別驗證的另一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="c854a-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="c854a-196">在 hello Azure 管理入口網站上 hello **SAP HANA 雲端平台身分識別驗證**應用程式整合頁面上，按一下 [**連結登入**。</span><span class="sxs-lookup"><span data-stu-id="c854a-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![設定連結的登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="c854a-198">然後，儲存 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="c854a-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="c854a-199">hello 新應用程式將會利用 hello 舊版 SAP 應用程式的 hello SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="c854a-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="c854a-200">請確定您使用 hello hello SAP HANA 雲端平台身分識別驗證管理主控台中相同公司身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="c854a-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c854a-201">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c854a-201">Create an Azure AD test user</span></span>
<span data-ttu-id="c854a-202">本節 hello 目標是 toocreate 測試使用者呼叫許 Simon hello 新入口網站中。</span><span class="sxs-lookup"><span data-stu-id="c854a-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="c854a-204">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c854a-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c854a-205">在 [hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="c854a-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c854a-207">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="c854a-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c854a-209">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="c854a-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c854a-211">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="c854a-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="c854a-213">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="c854a-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="c854a-214">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="c854a-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="c854a-215">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="c854a-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="c854a-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c854a-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="c854a-217">建立 SAP HANA Cloud Platform Identity Authentication 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c854a-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="c854a-218">您不需要 toocreate 上 SAP HANA 雲端平台身分識別驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="c854a-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="c854a-219">Hello Azure AD 使用者存放區中的使用者可以使用 hello SSO 功能。</span><span class="sxs-lookup"><span data-stu-id="c854a-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="c854a-220">SAP HANA 雲端平台身分識別驗證支援 hello 識別身分同盟選項。</span><span class="sxs-lookup"><span data-stu-id="c854a-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="c854a-221">這個選項允許 hello 應用程式 toocheck hello hello 公司身分識別提供者所驗證的使用者有在 hello 使用者存放區的 SAP HANA 雲端平台身分識別驗證。</span><span class="sxs-lookup"><span data-stu-id="c854a-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="c854a-222">Hello 預設設定，在 hello 識別身分同盟選項已停用。</span><span class="sxs-lookup"><span data-stu-id="c854a-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="c854a-223">如果已啟用識別身分同盟，只有 hello 會匯入 SAP HANA 雲端平台身分識別驗證的使用者都能 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c854a-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="c854a-224">如需有關如何在 tooenable 或停用識別身分同盟與 SAP HANA 雲端平台身分識別驗證，請參閱啟用識別身分同盟與 SAP HANA 雲端平台身分識別驗證中[設定識別身分同盟以 hello 使用者存放區的 SAP HANA 雲端平台身分識別驗證。](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="c854a-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="c854a-225">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="c854a-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="c854a-226">在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooSAP HANA 雲端平台身分識別驗證。</span><span class="sxs-lookup"><span data-stu-id="c854a-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![指派使用者][200] 

<span data-ttu-id="c854a-228">**tooassign 許 Simon tooSAP HANA 雲端平台身分識別驗證，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="c854a-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="c854a-229">在 [hello Azure 管理入口網站中，開啟 [hello 應用程式] 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="c854a-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="c854a-231">在 [hello] 應用程式清單中，選取**SAP HANA 雲端平台身分識別驗證**。</span><span class="sxs-lookup"><span data-stu-id="c854a-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="c854a-233">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="c854a-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="c854a-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c854a-235">Click **Add** button.</span></span> <span data-ttu-id="c854a-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="c854a-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="c854a-238">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="c854a-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c854a-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c854a-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c854a-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c854a-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="c854a-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="c854a-241">Test single sign-on</span></span>

<span data-ttu-id="c854a-242">本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="c854a-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c854a-243">當您按一下 hello SAP HANA 雲端平台身分識別驗證磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 SAP HANA 雲端平台身分識別驗證應用程式。</span><span class="sxs-lookup"><span data-stu-id="c854a-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c854a-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="c854a-244">Additional resources</span></span>

* [<span data-ttu-id="c854a-245">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c854a-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c854a-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="c854a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png