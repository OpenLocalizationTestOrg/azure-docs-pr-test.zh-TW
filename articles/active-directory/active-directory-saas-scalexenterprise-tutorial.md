---
title: "教學課程：Azure Active Directory 與 ScaleX Enterprise 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ScaleX 企業之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a><span data-ttu-id="0da5a-103">教學課程：Azure Active Directory 與 ScaleX Enterprise 整合</span><span class="sxs-lookup"><span data-stu-id="0da5a-103">Tutorial: Azure Active Directory integration with ScaleX Enterprise</span></span>

<span data-ttu-id="0da5a-104">在此教學課程中，您學會如何 toointegrate ScaleX 企業與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0da5a-104">In this tutorial, you learn how toointegrate ScaleX Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0da5a-105">使用 Azure AD 整合 ScaleX Enterprise 可以提供下列優點的 hello:</span><span class="sxs-lookup"><span data-stu-id="0da5a-105">Integrating ScaleX Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0da5a-106">您可以控制存取 tooScaleX Enterprise 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="0da5a-106">You can control in Azure AD who has access tooScaleX Enterprise</span></span>
- <span data-ttu-id="0da5a-107">您可以啟用您的使用者 tooautomatically get 登入 tooScaleX （單一登入） 的企業使用其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="0da5a-107">You can enable your users tooautomatically get signed-on tooScaleX Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0da5a-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0da5a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0da5a-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。</span><span class="sxs-lookup"><span data-stu-id="0da5a-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="0da5a-110">什麼是搭配 [Azure Active Directory](active-directory-appssoaccess-whatis.md) 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0da5a-110">What is application access and single sign-on with [Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0da5a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="0da5a-111">Prerequisites</span></span>

<span data-ttu-id="0da5a-112">tooconfigure ScaleX 企業與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="0da5a-112">tooconfigure Azure AD integration with ScaleX Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="0da5a-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0da5a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0da5a-114">已啟用 ScaleX Enterprise 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0da5a-114">A ScaleX Enterprise single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0da5a-115">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0da5a-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0da5a-116">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0da5a-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0da5a-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0da5a-117">Do not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0da5a-118">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0da5a-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0da5a-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="0da5a-119">Scenario description</span></span>
<span data-ttu-id="0da5a-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0da5a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0da5a-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0da5a-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0da5a-122">從 hello 圖庫加入 ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="0da5a-122">Adding ScaleX Enterprise from hello gallery</span></span>
2. <span data-ttu-id="0da5a-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0da5a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-scalex-enterprise-from-hello-gallery"></a><span data-ttu-id="0da5a-124">從 hello 圖庫加入 ScaleX Enterprise</span><span class="sxs-lookup"><span data-stu-id="0da5a-124">Adding ScaleX Enterprise from hello gallery</span></span>
<span data-ttu-id="0da5a-125">tooconfigure hello 整合 ScaleX 企業 tooAzure AD 中的，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd ScaleX 企業。</span><span class="sxs-lookup"><span data-stu-id="0da5a-125">tooconfigure hello integration of ScaleX Enterprise in tooAzure AD, you need tooadd ScaleX Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0da5a-126">**tooadd ScaleX 企業 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0da5a-126">**tooadd ScaleX Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0da5a-127">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0da5a-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0da5a-129">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0da5a-130">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-130">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0da5a-132">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0da5a-132">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0da5a-134">在 [hello] 搜尋方塊中，輸入**ScaleX 企業**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-134">In hello search box, type **ScaleX Enterprise**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. <span data-ttu-id="0da5a-136">在 hello 結果 窗格中，選取  **ScaleX 企業**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0da5a-136">In hello results panel, select **ScaleX Enterprise**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0da5a-138">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0da5a-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0da5a-139">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 ScaleX Enterprise 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0da5a-139">In this section, you configure and test Azure AD single sign-on with ScaleX Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0da5a-140">單一登入 toowork，Azure AD 需要 tooknow ScaleX 企業中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0da5a-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScaleX Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="0da5a-141">換句話說，Azure AD 使用者與 hello ScaleX 企業中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="0da5a-141">In other words, a link relationship between an Azure AD user and hello related user in ScaleX Enterprise needs toobe established.</span></span>

<span data-ttu-id="0da5a-142">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** ScaleX 企業中。</span><span class="sxs-lookup"><span data-stu-id="0da5a-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ScaleX Enterprise.</span></span>

<span data-ttu-id="0da5a-143">tooconfigure 及 ScaleX 企業與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="0da5a-143">tooconfigure and test Azure AD single sign-on with ScaleX Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0da5a-144">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="0da5a-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0da5a-145">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="0da5a-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0da5a-146">**[建立測試使用者 ScaleX 企業](#creating-a-scalex-enterprise-test-user)** -toohave 許 Simon ScaleX Enterprise 是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="0da5a-146">**[Creating a ScaleX Enterprise test user](#creating-a-scalex-enterprise-test-user)** - toohave a counterpart of Britta Simon in ScaleX Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0da5a-147">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0da5a-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0da5a-148">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="0da5a-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0da5a-149">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0da5a-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0da5a-150">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 ScaleX 企業應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0da5a-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScaleX Enterprise application.</span></span>

<span data-ttu-id="0da5a-151">**tooconfigure Azure AD 單一登入使用 ScaleX Enterprise，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0da5a-151">**tooconfigure Azure AD single sign-on with ScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="0da5a-152">在 Azure 入口網站上 hello hello **ScaleX 企業**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-152">In hello Azure portal, on hello **ScaleX Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0da5a-154">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0da5a-154">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. <span data-ttu-id="0da5a-156">在 hello **ScaleX 企業網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="0da5a-156">On hello **ScaleX Enterprise Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    <span data-ttu-id="0da5a-158">a.</span><span class="sxs-lookup"><span data-stu-id="0da5a-158">a.</span></span> <span data-ttu-id="0da5a-159">在 hello**識別碼**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://platform.rescale.com/saml2/<company id>/`</span><span class="sxs-lookup"><span data-stu-id="0da5a-159">In hello **Identifier** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/`</span></span>

    <span data-ttu-id="0da5a-160">b.</span><span class="sxs-lookup"><span data-stu-id="0da5a-160">b.</span></span> <span data-ttu-id="0da5a-161">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://platform.rescale.com/saml2/<company id>/acs/`</span><span class="sxs-lookup"><span data-stu-id="0da5a-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://platform.rescale.com/saml2/<company id>/acs/`</span></span>

4. <span data-ttu-id="0da5a-162">請檢查**顯示進階的 URL 設定**，如果您想 tooconfigure hello 應用程式中的**SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="0da5a-162">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    <span data-ttu-id="0da5a-164">在 hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://platform.rescale.com/saml2/<company id>/sso/`</span><span class="sxs-lookup"><span data-stu-id="0da5a-164">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://platform.rescale.com/saml2/<company id>/sso/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0da5a-165">這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="0da5a-165">These are not hello real values.</span></span> <span data-ttu-id="0da5a-166">更新這些值以 hello 實際的識別項 」、 「 回覆 URL 或 「 登入 URL。</span><span class="sxs-lookup"><span data-stu-id="0da5a-166">Update these values with hello actual Identifier, Reply URL or Sign-On URL.</span></span> <span data-ttu-id="0da5a-167">請連絡[ScaleX 企業用戶端支援小組](http://info.rescale.com/contact_sales)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="0da5a-167">Contact [ScaleX Enterprise Client support team](http://info.rescale.com/contact_sales) tooget these values.</span></span> 

5. <span data-ttu-id="0da5a-168">ScaleX 應用程式預期 hello SAML 判斷提示，以特定格式，這需要您 toomodify 自訂屬性對應 tooyour SAML token 屬性設定。</span><span class="sxs-lookup"><span data-stu-id="0da5a-168">Your ScaleX application expects hello SAML assertions in a specific format, which requires you toomodify custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="0da5a-169">按一下**檢視和編輯所有其他使用者屬性**核取方塊 tooopen hello 自訂屬性的設定。</span><span class="sxs-lookup"><span data-stu-id="0da5a-169">Click **View and edit all other user attributes** checkbox tooopen hello custom attributes settings.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    <span data-ttu-id="0da5a-171">a.</span><span class="sxs-lookup"><span data-stu-id="0da5a-171">a.</span></span> <span data-ttu-id="0da5a-172">以滑鼠右鍵按一下 hello 屬性**名稱**並按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="0da5a-172">Right click hello attribute **name** and click delete.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    <span data-ttu-id="0da5a-174">b.</span><span class="sxs-lookup"><span data-stu-id="0da5a-174">b.</span></span> <span data-ttu-id="0da5a-175">按一下**emailaddress**屬性 tooopen hello 編輯屬性 視窗。</span><span class="sxs-lookup"><span data-stu-id="0da5a-175">Click **emailaddress** attribute tooopen hello Edit Attribute window.</span></span> <span data-ttu-id="0da5a-176">變更其值從**user.mail**太**user.userprincipalname**按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0da5a-176">Change its value from **user.mail** too**user.userprincipalname** and click Ok.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. <span data-ttu-id="0da5a-178">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="0da5a-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. <span data-ttu-id="0da5a-180">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0da5a-180">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="0da5a-182">在 hello **ScaleX 企業設定**區段中，按一下**設定 ScaleX 企業**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="0da5a-182">On hello **ScaleX Enterprise Configuration** section, click **Configure ScaleX Enterprise** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0da5a-183">複製 hello **SAML 實體識別碼**和**SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="0da5a-183">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. <span data-ttu-id="0da5a-185">tooconfigure 單一登入上**ScaleX 企業**側邊，以系統管理員身分登入 toohello ScaleX Enterprise 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0da5a-185">tooconfigure single sign-on on **ScaleX Enterprise** side, login toohello ScaleX Enterprise company website as an administrator.</span></span>

9. <span data-ttu-id="0da5a-186">右按一下上方的 hello hello 功能表，然後選取**Contoso 管理**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-186">Click hello menu in hello upper right and select **Contoso Administration**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0da5a-187">Contoso 只是一個範例。</span><span class="sxs-lookup"><span data-stu-id="0da5a-187">Contoso is just an example.</span></span> <span data-ttu-id="0da5a-188">這應該是您實際的公司名稱。</span><span class="sxs-lookup"><span data-stu-id="0da5a-188">This should be your actual Company Name.</span></span> 

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. <span data-ttu-id="0da5a-190">選取**整合**hello 最上層功能表，然後選取從**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-190">Select **Integrations** from hello top menu and select **Single Sign-On**.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. <span data-ttu-id="0da5a-192">完成 hello 表單，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0da5a-192">Complete hello form as follows:</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    <span data-ttu-id="0da5a-194">a.</span><span class="sxs-lookup"><span data-stu-id="0da5a-194">a.</span></span> <span data-ttu-id="0da5a-195">選取 [建立可驗證 SSO 的任何使用者]。</span><span class="sxs-lookup"><span data-stu-id="0da5a-195">Select **“Create any user who can authenticate with SSO.”**</span></span>

    <span data-ttu-id="0da5a-196">b.</span><span class="sxs-lookup"><span data-stu-id="0da5a-196">b.</span></span> <span data-ttu-id="0da5a-197">**服務提供者 saml**: hello 值貼上***urn: oasis： 名稱： tc: SAML:2.0:nameid-格式： 持續性***</span><span class="sxs-lookup"><span data-stu-id="0da5a-197">**Service Provider saml**: Paste hello value ***urn:oasis:names:tc:SAML:2.0:nameid-format:persistent***</span></span>

    <span data-ttu-id="0da5a-198">c.</span><span class="sxs-lookup"><span data-stu-id="0da5a-198">c.</span></span> <span data-ttu-id="0da5a-199">**ACS 的回應中的身分識別提供者電子郵件欄位名稱**: hello 值貼上`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span><span class="sxs-lookup"><span data-stu-id="0da5a-199">**Name of Identity Provider email field in ACS response**: Paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>

    <span data-ttu-id="0da5a-200">d.</span><span class="sxs-lookup"><span data-stu-id="0da5a-200">d.</span></span> <span data-ttu-id="0da5a-201">**身分識別提供者 EntityDescriptor 實體識別碼：**貼上 hello **SAML 實體識別碼**從 hello Azure 入口網站複製的值。</span><span class="sxs-lookup"><span data-stu-id="0da5a-201">**Identity Provider EntityDescriptor Entity ID:** Paste hello **SAML Entity ID** value copied from hello Azure portal.</span></span>

    <span data-ttu-id="0da5a-202">e.</span><span class="sxs-lookup"><span data-stu-id="0da5a-202">e.</span></span> <span data-ttu-id="0da5a-203">**身分識別提供者 SingleSignOnService URL:**貼上 hello **SAML 單一登入服務 URL**從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0da5a-203">**Identity Provider SingleSignOnService URL:** Paste hello **SAML Single Sign-On Service URL** from hello Azure portal.</span></span>

    <span data-ttu-id="0da5a-204">f.</span><span class="sxs-lookup"><span data-stu-id="0da5a-204">f.</span></span> <span data-ttu-id="0da5a-205">**身分識別提供者公開 X509 憑證：**從 記事本 和 貼上此方塊中的 hello 內容中的 hello Azure 下載開啟 hello X509 憑證。</span><span class="sxs-lookup"><span data-stu-id="0da5a-205">**Identity Provider public X509 certificate:** Open hello X509 certificate downloaded from hello Azure in notepad and paste hello contents in this box.</span></span> <span data-ttu-id="0da5a-206">請確認有無分行符號 hello hello 憑證內容的中間。</span><span class="sxs-lookup"><span data-stu-id="0da5a-206">Ensure there are no line breaks in hello middle of hello certificate contents.</span></span>
    
    <span data-ttu-id="0da5a-207">g.</span><span class="sxs-lookup"><span data-stu-id="0da5a-207">g.</span></span> <span data-ttu-id="0da5a-208">請檢查下列核取方塊的 hello:**已啟用、 加密 NameID 和符號 AuthnRequests。**</span><span class="sxs-lookup"><span data-stu-id="0da5a-208">Check hello following checkboxes: **Enabled, Encrypt NameID and Sign AuthnRequests.**</span></span>

    <span data-ttu-id="0da5a-209">h.</span><span class="sxs-lookup"><span data-stu-id="0da5a-209">h.</span></span> <span data-ttu-id="0da5a-210">按一下**更新 SSO 設定**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="0da5a-210">Click **Update SSO Settings** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="0da5a-211">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="0da5a-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0da5a-212">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="0da5a-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0da5a-213">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0da5a-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0da5a-214">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0da5a-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="0da5a-215">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0da5a-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0da5a-217">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0da5a-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0da5a-218">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0da5a-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0da5a-220">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="0da5a-220">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0da5a-222">在 hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0da5a-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0da5a-224">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0da5a-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0da5a-226">a.</span><span class="sxs-lookup"><span data-stu-id="0da5a-226">a.</span></span> <span data-ttu-id="0da5a-227">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0da5a-228">b.</span><span class="sxs-lookup"><span data-stu-id="0da5a-228">b.</span></span> <span data-ttu-id="0da5a-229">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="0da5a-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0da5a-230">c.</span><span class="sxs-lookup"><span data-stu-id="0da5a-230">c.</span></span> <span data-ttu-id="0da5a-231">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0da5a-232">d.</span><span class="sxs-lookup"><span data-stu-id="0da5a-232">d.</span></span> <span data-ttu-id="0da5a-233">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0da5a-233">Click **Create**.</span></span>
 
### <a name="creating-a-scalex-enterprise-test-user"></a><span data-ttu-id="0da5a-234">建立 ScaleX Enterprise 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0da5a-234">Creating a ScaleX Enterprise test user</span></span>

<span data-ttu-id="0da5a-235">tooenable Azure AD 使用者 toolog 中 tooScaleX 企業，必須將他們佈建 tooScaleX 企業中。</span><span class="sxs-lookup"><span data-stu-id="0da5a-235">tooenable Azure AD users toolog in tooScaleX Enterprise, they must be provisioned in tooScaleX Enterprise.</span></span> <span data-ttu-id="0da5a-236">在 ScaleX 企業的 hello 案例中，佈建是自動的工作而不需要任何手動步驟。</span><span class="sxs-lookup"><span data-stu-id="0da5a-236">In hello case of ScaleX Enterprise, provisioning is an automatic task and no manual steps are required.</span></span> <span data-ttu-id="0da5a-237">將在 hello ScaleX 端上自動佈建任何使用者都可以成功驗證的登入認證。</span><span class="sxs-lookup"><span data-stu-id="0da5a-237">Any user who can successfully authenticate with SSO credentials will be automatically provisioned on hello ScaleX side.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0da5a-238">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="0da5a-238">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0da5a-239">在本節中，您可以授與使用者存取 tooScaleX 企業啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0da5a-239">In this section, you enable Britta Simon toouse Azure single sign-on by granting user access tooScaleX Enterprise.</span></span>

![指派使用者][200] 

<span data-ttu-id="0da5a-241">**tooassign 許 Simon tooScaleX 企業中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0da5a-241">**tooassign Britta Simon tooScaleX Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="0da5a-242">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-242">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0da5a-244">在 [hello] 應用程式清單中，選取**ScaleX 企業**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-244">In hello applications list, select **ScaleX Enterprise**.</span></span>

    ![設定單一登入](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. <span data-ttu-id="0da5a-246">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="0da5a-246">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0da5a-248">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0da5a-248">Click **Add** button.</span></span> <span data-ttu-id="0da5a-249">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0da5a-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0da5a-251">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="0da5a-251">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0da5a-252">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0da5a-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0da5a-253">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0da5a-253">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="0da5a-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0da5a-254">Testing single sign-on</span></span>

<span data-ttu-id="0da5a-255">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="0da5a-255">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0da5a-256">按一下的 hello ScaleX 企業磚 hello 存取面板中就會自動登入 tooyour ScaleX 企業應用程式。</span><span class="sxs-lookup"><span data-stu-id="0da5a-256">Click hello ScaleX Enterprise tile in hello Access Panel, you will get automatically signed-on tooyour ScaleX Enterprise application.</span></span> <span data-ttu-id="0da5a-257">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="0da5a-257">For more information about hello Access Panel, see [Introduction toohello Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0da5a-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="0da5a-258">Additional resources</span></span>

* [<span data-ttu-id="0da5a-259">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0da5a-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0da5a-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0da5a-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

