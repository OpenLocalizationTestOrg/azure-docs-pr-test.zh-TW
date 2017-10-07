---
title: "教學課程：Azure Active Directory 與 eKincare 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 eKincare 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 16129e3384132bb34744aadf088bb65f07ed7a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="4b11d-103">教學課程：Azure Active Directory 與 eKincare 整合</span><span class="sxs-lookup"><span data-stu-id="4b11d-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="4b11d-104">在此教學課程中，您學會如何 toointegrate eKincare 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4b11d-104">In this tutorial, you learn how toointegrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b11d-105">與 Azure AD 整合 eKincare 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="4b11d-105">Integrating eKincare with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b11d-106">您可以控制存取 tooeKincare Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="4b11d-106">You can control in Azure AD who has access tooeKincare</span></span>
- <span data-ttu-id="4b11d-107">您可以啟用您的使用者 tooautomatically get 登入 tooeKincare （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="4b11d-107">You can enable your users tooautomatically get signed-on tooeKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4b11d-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4b11d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4b11d-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4b11d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b11d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4b11d-110">Prerequisites</span></span>

<span data-ttu-id="4b11d-111">tooconfigure eKincare 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="4b11d-111">tooconfigure Azure AD integration with eKincare, you need hello following items:</span></span>

- <span data-ttu-id="4b11d-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4b11d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b11d-113">啟用 eKincare 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4b11d-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b11d-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="4b11d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b11d-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4b11d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b11d-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4b11d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b11d-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="4b11d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b11d-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4b11d-118">Scenario description</span></span>
<span data-ttu-id="4b11d-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b11d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b11d-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="4b11d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b11d-121">從 hello 圖庫加入 eKincare</span><span class="sxs-lookup"><span data-stu-id="4b11d-121">Adding eKincare from hello gallery</span></span>
2. <span data-ttu-id="4b11d-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b11d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-hello-gallery"></a><span data-ttu-id="4b11d-123">從 hello 圖庫加入 eKincare</span><span class="sxs-lookup"><span data-stu-id="4b11d-123">Adding eKincare from hello gallery</span></span>
<span data-ttu-id="4b11d-124">tooconfigure hello 整合 eKincare 到 Azure AD，您需要 tooadd eKincare hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b11d-124">tooconfigure hello integration of eKincare into Azure AD, you need tooadd eKincare from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b11d-125">**tooadd eKincare 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4b11d-125">**tooadd eKincare from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b11d-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4b11d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4b11d-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b11d-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="4b11d-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b11d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="4b11d-133">在 [hello] 搜尋方塊中，輸入**eKincare**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-133">In hello search box, type **eKincare**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="4b11d-135">在 [hello [結果] 窗格中，選取 [ **eKincare**，然後按一下 [**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b11d-135">In hello results panel, select **eKincare**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4b11d-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b11d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4b11d-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 eKincare 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b11d-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4b11d-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 eKincare 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="4b11d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eKincare is tooa user in Azure AD.</span></span> <span data-ttu-id="4b11d-140">換句話說，Azure AD 使用者與 hello eKincare 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="4b11d-140">In other words, a link relationship between an Azure AD user and hello related user in eKincare needs toobe established.</span></span>

<span data-ttu-id="4b11d-141">EKincare 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4b11d-141">In eKincare, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b11d-142">tooconfigure 及 eKincare 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="4b11d-142">tooconfigure and test Azure AD single sign-on with eKincare, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b11d-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="4b11d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b11d-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="4b11d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b11d-145">**[建立測試使用者 eKincare](#creating-a-ekincare-test-user) ** -toohave 是連結的 toohello Azure AD 使用者表示法的 eKincare 的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="4b11d-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - toohave a counterpart of Britta Simon in eKincare that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b11d-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b11d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b11d-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="4b11d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4b11d-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b11d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4b11d-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 eKincare 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b11d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="4b11d-150">**tooconfigure Azure AD 單一登入與 eKincare，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4b11d-150">**tooconfigure Azure AD single sign-on with eKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b11d-151">在 Azure 入口網站上 hello hello **eKincare**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-151">In hello Azure portal, on hello **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="4b11d-153">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b11d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="4b11d-155">在 [hello **eKincare 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4b11d-155">On hello **eKincare Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="4b11d-157">a.</span><span class="sxs-lookup"><span data-stu-id="4b11d-157">a.</span></span> <span data-ttu-id="4b11d-158">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="4b11d-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="4b11d-159">b.</span><span class="sxs-lookup"><span data-stu-id="4b11d-159">b.</span></span> <span data-ttu-id="4b11d-160">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="4b11d-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4b11d-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="4b11d-161">These values are not real.</span></span> <span data-ttu-id="4b11d-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="4b11d-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="4b11d-163">請連絡[eKincare 支援小組](mailto:tech@ekincare.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="4b11d-163">Contact [eKincare support team](mailto:tech@ekincare.com) tooget these values.</span></span>
 
4. <span data-ttu-id="4b11d-164">eKincare 應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="4b11d-164">eKincare application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="4b11d-165">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="4b11d-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="4b11d-166">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="4b11d-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="4b11d-167">hello 下列螢幕擷取畫面顯示此組態範例。</span><span class="sxs-lookup"><span data-stu-id="4b11d-167">hello following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="4b11d-168">hello 宣告名稱一定會**"employeeid"**和其中我們有對應的 toouser.extensionattribute1 包含 hello employeeid 的 hello 使用者 hello 值。</span><span class="sxs-lookup"><span data-stu-id="4b11d-168">hello claim name will always be **"employeeid"** and hello value of which we have mapped toouser.extensionattribute1, that contains hello employeeid of hello user.</span></span> <span data-ttu-id="4b11d-169">hello 其他兩個宣告的名稱也就是</span><span class="sxs-lookup"><span data-stu-id="4b11d-169">hello other two claims' name i.e</span></span> <span data-ttu-id="4b11d-170">**「 organizationid"**和**"organizationname"**一定會是相同，而且其值分別包含 hello hello 組織 hello 使用者的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4b11d-170">**"organizationid"** and **"organizationname"** will always be same and their values contain hello details of hello organization of hello user respectively.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="4b11d-172">在 hello**使用者屬性**區段 hello**單一登入**] 對話方塊中，上述 hello 映像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4b11d-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="4b11d-173">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="4b11d-173">Attribute Name</span></span> | <span data-ttu-id="4b11d-174">屬性值</span><span class="sxs-lookup"><span data-stu-id="4b11d-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="4b11d-175">employeeid</span><span class="sxs-lookup"><span data-stu-id="4b11d-175">employeeid</span></span> | <span data-ttu-id="4b11d-176">*user.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="4b11d-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="4b11d-177">organizationid</span><span class="sxs-lookup"><span data-stu-id="4b11d-177">organizationid</span></span> | <span data-ttu-id="4b11d-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="4b11d-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="4b11d-179">organizationname</span><span class="sxs-lookup"><span data-stu-id="4b11d-179">organizationname</span></span> | <span data-ttu-id="4b11d-180">*user.companyname*</span><span class="sxs-lookup"><span data-stu-id="4b11d-180">*user.companyname*</span></span> |

    <span data-ttu-id="4b11d-181">a.</span><span class="sxs-lookup"><span data-stu-id="4b11d-181">a.</span></span> <span data-ttu-id="4b11d-182">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4b11d-182">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![設定單一登入](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="4b11d-185">b.</span><span class="sxs-lookup"><span data-stu-id="4b11d-185">b.</span></span> <span data-ttu-id="4b11d-186">在 [hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="4b11d-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="4b11d-187">c.</span><span class="sxs-lookup"><span data-stu-id="4b11d-187">c.</span></span> <span data-ttu-id="4b11d-188">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="4b11d-188">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="4b11d-189">d.</span><span class="sxs-lookup"><span data-stu-id="4b11d-189">d.</span></span> <span data-ttu-id="4b11d-190">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4b11d-190">Click **Ok**</span></span>

6. <span data-ttu-id="4b11d-191">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="4b11d-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="4b11d-193">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b11d-193">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4b11d-195">tooconfigure 單一登入上**eKincare**端，您需要下載 toosend hello**中繼資料 XML**太[eKincare 支援小組](mailto:tech@ekincare.com)。</span><span class="sxs-lookup"><span data-stu-id="4b11d-195">tooconfigure single sign-on on **eKincare** side, you need toosend hello downloaded **Metadata XML** too[eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="4b11d-196">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="4b11d-196">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4b11d-197">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="4b11d-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b11d-198">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="4b11d-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b11d-199">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b11d-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4b11d-200">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b11d-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="4b11d-201">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4b11d-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="4b11d-203">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4b11d-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b11d-204">在 [hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="4b11d-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4b11d-206">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4b11d-208">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="4b11d-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4b11d-210">在 [hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4b11d-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4b11d-212">a.</span><span class="sxs-lookup"><span data-stu-id="4b11d-212">a.</span></span> <span data-ttu-id="4b11d-213">在 [hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b11d-214">b.</span><span class="sxs-lookup"><span data-stu-id="4b11d-214">b.</span></span> <span data-ttu-id="4b11d-215">在 [hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="4b11d-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4b11d-216">c.</span><span class="sxs-lookup"><span data-stu-id="4b11d-216">c.</span></span> <span data-ttu-id="4b11d-217">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4b11d-218">d.</span><span class="sxs-lookup"><span data-stu-id="4b11d-218">d.</span></span> <span data-ttu-id="4b11d-219">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4b11d-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="4b11d-220">建立 eKincare 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b11d-220">Creating a eKincare test user</span></span>

<span data-ttu-id="4b11d-221">應用程式支援恰好在即時使用者佈建，以及之後驗證使用者會自動建立 hello 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="4b11d-221">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4b11d-222">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b11d-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4b11d-223">在本節中，您可以授與存取 tooeKincare 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b11d-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeKincare.</span></span>

![指派使用者][200] 

<span data-ttu-id="4b11d-225">**tooassign 許 Simon tooeKincare，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="4b11d-225">**tooassign Britta Simon tooeKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b11d-226">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4b11d-228">在 [hello] 應用程式清單中，選取**eKincare**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-228">In hello applications list, select **eKincare**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="4b11d-230">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="4b11d-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="4b11d-232">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b11d-232">Click **Add** button.</span></span> <span data-ttu-id="4b11d-233">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4b11d-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="4b11d-235">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="4b11d-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b11d-236">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b11d-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b11d-237">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b11d-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4b11d-238">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4b11d-238">Testing single sign-on</span></span>

<span data-ttu-id="4b11d-239">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="4b11d-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b11d-240">當您按一下 hello eKincare 磚 hello 存取面板中的時，您應該取得自動登入 tooyour eKincare 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b11d-240">When you click hello eKincare tile in hello Access Panel, you should get automatically signed-on tooyour eKincare application.</span></span>
<span data-ttu-id="4b11d-241">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="4b11d-241">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b11d-242">其他資源</span><span class="sxs-lookup"><span data-stu-id="4b11d-242">Additional resources</span></span>

* [<span data-ttu-id="4b11d-243">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b11d-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b11d-244">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4b11d-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

