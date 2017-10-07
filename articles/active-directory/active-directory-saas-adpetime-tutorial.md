---
title: "教學課程：Azure Active Directory 與 ADP eTime 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和 ADP eTime 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="98d88-103">教學課程：Azure Active Directory 與 ADP eTime 整合</span><span class="sxs-lookup"><span data-stu-id="98d88-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="98d88-104">在此教學課程中，您學會如何 toointegrate ADP eTime 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="98d88-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98d88-105">與 Azure AD 整合 ADP eTime 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="98d88-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="98d88-106">您可以控制存取 tooADP eTime Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="98d88-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="98d88-107">您可以啟用您的使用者 tooautomatically get 登入 tooADP eTime （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="98d88-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="98d88-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="98d88-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="98d88-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="98d88-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98d88-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="98d88-110">Prerequisites</span></span>

<span data-ttu-id="98d88-111">tooconfigure ADP eTime 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="98d88-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="98d88-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="98d88-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98d88-113">已啟用 ADP eTime 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="98d88-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98d88-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="98d88-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="98d88-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="98d88-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98d88-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="98d88-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98d88-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="98d88-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98d88-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="98d88-118">Scenario description</span></span>
<span data-ttu-id="98d88-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="98d88-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98d88-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="98d88-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98d88-121">從 hello 圖庫加入 ADP eTime</span><span class="sxs-lookup"><span data-stu-id="98d88-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="98d88-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="98d88-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="98d88-123">從 hello 圖庫加入 ADP eTime</span><span class="sxs-lookup"><span data-stu-id="98d88-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="98d88-124">tooconfigure hello 整合 ADP eTime 到 Azure AD，您需要 tooadd ADP eTime hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98d88-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="98d88-125">**tooadd ADP eTime 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="98d88-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="98d88-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="98d88-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="98d88-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="98d88-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="98d88-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="98d88-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="98d88-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="98d88-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="98d88-133">在 [hello] 搜尋方塊中，輸入**ADP eTime**。</span><span class="sxs-lookup"><span data-stu-id="98d88-133">In hello search box, type **ADP eTime**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="98d88-135">在 hello 結果 窗格中，選取  **ADP eTime**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98d88-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="98d88-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="98d88-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="98d88-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ADP eTime 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="98d88-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="98d88-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 ADP eTime 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="98d88-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="98d88-140">換句話說，Azure AD 使用者和 ADP eTime 中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="98d88-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="98d88-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** ADP eTime 中。</span><span class="sxs-lookup"><span data-stu-id="98d88-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="98d88-142">tooconfigure 和 ADP eTime 與 Azure AD 單一登入的測試，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="98d88-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="98d88-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="98d88-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="98d88-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="98d88-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="98d88-145">**[建立 ADP eTime 測試使用者](#creating-an-adp-etime-test-user)** -toohave 是連結的 toohello Azure AD 使用者表示法的 ADP eTime 的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="98d88-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="98d88-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="98d88-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="98d88-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="98d88-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="98d88-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="98d88-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="98d88-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 ADP eTime 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="98d88-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="98d88-150">**tooconfigure Azure AD 單一登入與 ADP eTime，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="98d88-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="98d88-151">在 Azure 入口網站上 hello hello **ADP eTime**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="98d88-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="98d88-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="98d88-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="98d88-155">在 hello **ADP eTime 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="98d88-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="98d88-157">a.</span><span class="sxs-lookup"><span data-stu-id="98d88-157">a.</span></span> <span data-ttu-id="98d88-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="98d88-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="98d88-159">b.</span><span class="sxs-lookup"><span data-stu-id="98d88-159">b.</span></span> <span data-ttu-id="98d88-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="98d88-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="98d88-161">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="98d88-161">These values are not hello real.</span></span> <span data-ttu-id="98d88-162">更新這些值與 hello 實際的回覆 URL 和識別碼。</span><span class="sxs-lookup"><span data-stu-id="98d88-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="98d88-163">請連絡[ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="98d88-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="98d88-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="98d88-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="98d88-166">hello ADP eTime 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="98d88-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="98d88-167">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="98d88-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="98d88-168">hello 宣告名稱一定會**"PersonImmutableID"**和 hello 值其中我們已對應包含 tooExtensionAttribute2 hello EmployeeID 的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="98d88-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="98d88-169">這裡 hello EmployeeID 會完成從 Azure AD tooADP eTime hello 使用者對應，但是您可以對應也會根據您的應用程式設定這個 tooa 不同值。</span><span class="sxs-lookup"><span data-stu-id="98d88-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="98d88-170">工作，因此請與[ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)第一個 toouse hello 正確的識別項的使用者，並將對應與 hello 該值**"PersonImmutableID"**宣告。</span><span class="sxs-lookup"><span data-stu-id="98d88-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="98d88-172">在 hello**使用者屬性**hello 區段**單一登入** 對話方塊中，hello 映像中所示設定 SAML 權杖屬性並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="98d88-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="98d88-173">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="98d88-173">Attribute Name</span></span> | <span data-ttu-id="98d88-174">屬性值</span><span class="sxs-lookup"><span data-stu-id="98d88-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="98d88-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="98d88-175">PersonImmutableID</span></span> | <span data-ttu-id="98d88-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="98d88-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="98d88-177">a.</span><span class="sxs-lookup"><span data-stu-id="98d88-177">a.</span></span> <span data-ttu-id="98d88-178">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="98d88-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="98d88-181">b.</span><span class="sxs-lookup"><span data-stu-id="98d88-181">b.</span></span> <span data-ttu-id="98d88-182">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="98d88-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="98d88-183">c.</span><span class="sxs-lookup"><span data-stu-id="98d88-183">c.</span></span> <span data-ttu-id="98d88-184">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="98d88-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="98d88-185">d.</span><span class="sxs-lookup"><span data-stu-id="98d88-185">d.</span></span> <span data-ttu-id="98d88-186">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="98d88-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="98d88-187">您可以設定 hello SAML 判斷提示之前，您需要 toocontact 您[ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)並要求您的租用戶 hello hello 唯一識別碼屬性值。</span><span class="sxs-lookup"><span data-stu-id="98d88-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="98d88-188">您需要此值 tooconfigure hello 自訂宣告您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="98d88-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="98d88-189">在 hello **ADP eTime 組態**區段中，按一下**設定 ADP eTime** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="98d88-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="98d88-191">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="98d88-191">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="98d88-193">tooconfigure 單一登入上**ADP eTime**端，您需要下載 toosend hello**中繼資料 XML**太[ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)。</span><span class="sxs-lookup"><span data-stu-id="98d88-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="98d88-194">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="98d88-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="98d88-195">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="98d88-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="98d88-196">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="98d88-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="98d88-197">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="98d88-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="98d88-198">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="98d88-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="98d88-200">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="98d88-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="98d88-201">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="98d88-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="98d88-203">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="98d88-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="98d88-205">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="98d88-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="98d88-207">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="98d88-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="98d88-209">a.</span><span class="sxs-lookup"><span data-stu-id="98d88-209">a.</span></span> <span data-ttu-id="98d88-210">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="98d88-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98d88-211">b.</span><span class="sxs-lookup"><span data-stu-id="98d88-211">b.</span></span> <span data-ttu-id="98d88-212">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="98d88-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="98d88-213">c.</span><span class="sxs-lookup"><span data-stu-id="98d88-213">c.</span></span> <span data-ttu-id="98d88-214">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="98d88-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="98d88-215">d.</span><span class="sxs-lookup"><span data-stu-id="98d88-215">d.</span></span> <span data-ttu-id="98d88-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="98d88-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="98d88-217">建立 ADP eTime 測試使用者</span><span class="sxs-lookup"><span data-stu-id="98d88-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="98d88-218">hello 本節目標在於 toocreate ADP eTime 中呼叫許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="98d88-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="98d88-219">使用[ADP eTime 支援小組](https://www.adp.com/contact-us/overview.aspx)tooadd hello hello ADP eTime 帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="98d88-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="98d88-220">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="98d88-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="98d88-221">在本節中，您可以授與存取 tooADP eTime 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="98d88-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![指派使用者][200] 

<span data-ttu-id="98d88-223">**tooassign 許 Simon tooADP eTime，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="98d88-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="98d88-224">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="98d88-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="98d88-226">在 [hello] 應用程式清單中，選取**ADP eTime**。</span><span class="sxs-lookup"><span data-stu-id="98d88-226">In hello applications list, select **ADP eTime**.</span></span>

    ![設定單一登入](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="98d88-228">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="98d88-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="98d88-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="98d88-230">Click **Add** button.</span></span> <span data-ttu-id="98d88-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="98d88-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="98d88-233">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="98d88-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="98d88-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="98d88-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="98d88-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="98d88-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="98d88-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="98d88-236">Testing single sign-on</span></span>

<span data-ttu-id="98d88-237">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="98d88-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="98d88-238">當您按一下 hello 存取面板中的 hello ADP eTime 磚時，您應該取得自動登入 tooyour ADP eTime 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98d88-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="98d88-239">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="98d88-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="98d88-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="98d88-240">Additional resources</span></span>

* [<span data-ttu-id="98d88-241">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98d88-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="98d88-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="98d88-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

