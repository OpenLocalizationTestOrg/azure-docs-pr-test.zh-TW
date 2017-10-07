---
title: "教學課程：Azure Active Directory 與 BenefitHub 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 BenefitHub 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="673f8-103">教學課程：Azure Active Directory 與 BenefitHub 整合</span><span class="sxs-lookup"><span data-stu-id="673f8-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="673f8-104">在此教學課程中，您學會如何 toointegrate BenefitHub 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="673f8-104">In this tutorial, you learn how toointegrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="673f8-105">與 Azure AD 整合 BenefitHub 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="673f8-105">Integrating BenefitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="673f8-106">您可以控制存取 tooBenefitHub Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="673f8-106">You can control in Azure AD who has access tooBenefitHub</span></span>
- <span data-ttu-id="673f8-107">您可以啟用您的使用者 tooautomatically get 登入 tooBenefitHub （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="673f8-107">You can enable your users tooautomatically get signed-on tooBenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="673f8-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="673f8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="673f8-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="673f8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="673f8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="673f8-110">Prerequisites</span></span>

<span data-ttu-id="673f8-111">tooconfigure BenefitHub 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="673f8-111">tooconfigure Azure AD integration with BenefitHub, you need hello following items:</span></span>

- <span data-ttu-id="673f8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="673f8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="673f8-113">已啟用 BenefitHub 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="673f8-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="673f8-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="673f8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="673f8-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="673f8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="673f8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="673f8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="673f8-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="673f8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="673f8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="673f8-118">Scenario description</span></span>
<span data-ttu-id="673f8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="673f8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="673f8-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="673f8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="673f8-121">從 hello 圖庫加入 BenefitHub</span><span class="sxs-lookup"><span data-stu-id="673f8-121">Adding BenefitHub from hello gallery</span></span>
2. <span data-ttu-id="673f8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="673f8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-hello-gallery"></a><span data-ttu-id="673f8-123">從 hello 圖庫加入 BenefitHub</span><span class="sxs-lookup"><span data-stu-id="673f8-123">Adding BenefitHub from hello gallery</span></span>
<span data-ttu-id="673f8-124">tooconfigure hello 整合 BenefitHub 到 Azure AD，您需要 tooadd BenefitHub hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="673f8-124">tooconfigure hello integration of BenefitHub into Azure AD, you need tooadd BenefitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="673f8-125">**tooadd BenefitHub 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="673f8-125">**tooadd BenefitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="673f8-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="673f8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="673f8-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="673f8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="673f8-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="673f8-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="673f8-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="673f8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="673f8-133">在 [hello] 搜尋方塊中，輸入**BenefitHub**。</span><span class="sxs-lookup"><span data-stu-id="673f8-133">In hello search box, type **BenefitHub**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="673f8-135">在 hello 結果 窗格中，選取  **BenefitHub**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="673f8-135">In hello results panel, select **BenefitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="673f8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="673f8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="673f8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 BenefitHub 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="673f8-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="673f8-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 BenefitHub 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="673f8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenefitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="673f8-140">換句話說，Azure AD 使用者與 hello BenefitHub 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="673f8-140">In other words, a link relationship between an Azure AD user and hello related user in BenefitHub needs toobe established.</span></span>

<span data-ttu-id="673f8-141">BenefitHub 中, 指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="673f8-141">In BenefitHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="673f8-142">tooconfigure 及 BenefitHub 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="673f8-142">tooconfigure and test Azure AD single sign-on with BenefitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="673f8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="673f8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="673f8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="673f8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="673f8-145">**[建立測試使用者 BenefitHub](#creating-a-benefithub-test-user)**  -toohave 許 Simon BenefitHub 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="673f8-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - toohave a counterpart of Britta Simon in BenefitHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="673f8-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="673f8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="673f8-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="673f8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="673f8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="673f8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="673f8-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 BenefitHub 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="673f8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="673f8-150">**tooconfigure Azure AD 單一登入與 BenefitHub，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="673f8-150">**tooconfigure Azure AD single sign-on with BenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="673f8-151">在 Azure 入口網站上 hello hello **BenefitHub**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="673f8-151">In hello Azure portal, on hello **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="673f8-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="673f8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="673f8-155">在 hello **BenefitHub 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="673f8-155">On hello **BenefitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="673f8-157">a.</span><span class="sxs-lookup"><span data-stu-id="673f8-157">a.</span></span> <span data-ttu-id="673f8-158">在 hello**識別碼**文字方塊中，輸入：`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="673f8-158">In hello **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="673f8-159">b.</span><span class="sxs-lookup"><span data-stu-id="673f8-159">b.</span></span> <span data-ttu-id="673f8-160">在 hello**回覆 URL**文字方塊中，輸入：`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="673f8-160">In hello **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="673f8-161">hello BenefitHub 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="673f8-161">hello BenefitHub application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="673f8-162">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="673f8-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="673f8-163">您可以從 hello 管理 hello 這些屬性的值"**使用者屬性**」 一節，在應用程式整合頁面上。</span><span class="sxs-lookup"><span data-stu-id="673f8-163">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![設定單一登入](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="673f8-165">在 hello**使用者屬性**hello 區段**單一登入** 對話方塊中，hello 上述影像中所示設定 SAML 權杖屬性和執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="673f8-165">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="673f8-166">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="673f8-166">Attribute Name</span></span> | <span data-ttu-id="673f8-167">屬性值</span><span class="sxs-lookup"><span data-stu-id="673f8-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="673f8-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="673f8-168">organizationid</span></span> | <span data-ttu-id="673f8-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="673f8-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="673f8-170">這不是真正的屬性值。</span><span class="sxs-lookup"><span data-stu-id="673f8-170">This attribute value is not real.</span></span> <span data-ttu-id="673f8-171">請使用實際的 organizationid 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="673f8-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="673f8-172">請連絡[BenefitHub 支援小組](https://www.benefithub.com/Home/ContactUs)tooget hello 實際 organizationid。</span><span class="sxs-lookup"><span data-stu-id="673f8-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) tooget hello actual organizationid.</span></span>
    
    <span data-ttu-id="673f8-173">a.</span><span class="sxs-lookup"><span data-stu-id="673f8-173">a.</span></span> <span data-ttu-id="673f8-174">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="673f8-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="673f8-177">b.</span><span class="sxs-lookup"><span data-stu-id="673f8-177">b.</span></span> <span data-ttu-id="673f8-178">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="673f8-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="673f8-179">c.</span><span class="sxs-lookup"><span data-stu-id="673f8-179">c.</span></span> <span data-ttu-id="673f8-180">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="673f8-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="673f8-181">d.</span><span class="sxs-lookup"><span data-stu-id="673f8-181">d.</span></span> <span data-ttu-id="673f8-182">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="673f8-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="673f8-183">您可以設定 hello SAML 判斷提示之前，您需要 toocontact 您[BenefitHub 支援](https://www.benefithub.com/Home/ContactUs)並要求您的租用戶 hello hello 唯一識別碼屬性值。</span><span class="sxs-lookup"><span data-stu-id="673f8-183">Before you can configure hello SAML assertion, you need toocontact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="673f8-184">您需要此值 tooconfigure hello 自訂宣告您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="673f8-184">You need this value tooconfigure hello custom claim for your application.</span></span>

6. <span data-ttu-id="673f8-185">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="673f8-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="673f8-187">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="673f8-187">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="673f8-189">tooconfigure 單一登入上**BenefitHub**端，您需要下載 toosend hello**中繼資料 XML**太[BenefitHub 支援小組](https://www.benefithub.com/Home/ContactUs)。</span><span class="sxs-lookup"><span data-stu-id="673f8-189">tooconfigure single sign-on on **BenefitHub** side, you need toosend hello downloaded **Metadata XML** too[BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="673f8-190">設定此設定 toohave hello SAML SSO 連線兩端上正確設定這些欄位。</span><span class="sxs-lookup"><span data-stu-id="673f8-190">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="673f8-191">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="673f8-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="673f8-192">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="673f8-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="673f8-193">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="673f8-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="673f8-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="673f8-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="673f8-195">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="673f8-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="673f8-197">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="673f8-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="673f8-198">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="673f8-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="673f8-200">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="673f8-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="673f8-202">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="673f8-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="673f8-204">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="673f8-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="673f8-206">a.</span><span class="sxs-lookup"><span data-stu-id="673f8-206">a.</span></span> <span data-ttu-id="673f8-207">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="673f8-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="673f8-208">b.</span><span class="sxs-lookup"><span data-stu-id="673f8-208">b.</span></span> <span data-ttu-id="673f8-209">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="673f8-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="673f8-210">c.</span><span class="sxs-lookup"><span data-stu-id="673f8-210">c.</span></span> <span data-ttu-id="673f8-211">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="673f8-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="673f8-212">d.</span><span class="sxs-lookup"><span data-stu-id="673f8-212">d.</span></span> <span data-ttu-id="673f8-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="673f8-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="673f8-214">建立 BenefitHub 測試使用者</span><span class="sxs-lookup"><span data-stu-id="673f8-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="673f8-215">在本節中，您會在 BenefitHub 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="673f8-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="673f8-216">使用[BenefitHub 支援小組](https://www.benefithub.com/Home/ContactUs)hello BenefitHub 平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="673f8-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add hello users in hello BenefitHub platform.</span></span> <span data-ttu-id="673f8-217">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="673f8-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="673f8-218">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="673f8-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="673f8-219">在本節中，您可以授與存取 tooBenefitHub 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="673f8-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenefitHub.</span></span>

![指派使用者][200] 

<span data-ttu-id="673f8-221">**tooassign 許 Simon tooBenefitHub，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="673f8-221">**tooassign Britta Simon tooBenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="673f8-222">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="673f8-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="673f8-224">在 [hello] 應用程式清單中，選取**BenefitHub**。</span><span class="sxs-lookup"><span data-stu-id="673f8-224">In hello applications list, select **BenefitHub**.</span></span>

    ![設定單一登入](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="673f8-226">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="673f8-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="673f8-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="673f8-228">Click **Add** button.</span></span> <span data-ttu-id="673f8-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="673f8-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="673f8-231">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="673f8-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="673f8-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="673f8-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="673f8-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="673f8-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="673f8-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="673f8-234">Testing single sign-on</span></span>

<span data-ttu-id="673f8-235">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="673f8-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="673f8-236">當您按一下 hello BenefitHub 磚 hello 存取面板中的時，您應該取得自動登入 tooyour BenefitHub 應用程式。</span><span class="sxs-lookup"><span data-stu-id="673f8-236">When you click hello BenefitHub tile in hello Access Panel, you should get automatically signed-on tooyour BenefitHub application.</span></span>
<span data-ttu-id="673f8-237">如需存取面板的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="673f8-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="673f8-238">其他資源</span><span class="sxs-lookup"><span data-stu-id="673f8-238">Additional resources</span></span>

* [<span data-ttu-id="673f8-239">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="673f8-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="673f8-240">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="673f8-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

